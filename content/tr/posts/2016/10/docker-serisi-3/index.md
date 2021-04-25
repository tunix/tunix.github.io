---
title: "Docker Serisi #3 -- Docker Engine Bölüm 2"
date: 2016-10-13
slug: docker-serisi-3
tags:
    - yazılım
    - docker
    - docker serisi
    - container
    - sanallaştırma
    - linux
    - devops
---

Docker Serisi’nin 3. bölümüne hoşgeldiniz! [İlk bölümde]({{< ref "docker-serisi-1" >}}) sanallaştırmanın ne olduğundan, 
container teknolojisinden ve temel Docker kavramlarından; [ikinci bölümde]({{< ref "docker-serisi-2" >}}) Docker Engine 
ve Docker komutlarından bahsetmiştim. Bu bölümdeyse özetle şu konulara değineceğim:

* [Kalıcı Veri Depolama]({{< ref "#kalıcı-veri-depolama" >}})
* [Çevresel Değişkenler]({{< ref "#çevresel-değişkenler" >}})
* [Bağlantı Noktaları]({{< ref "#bağlantı-noktaları" >}})
* [Dockerfile]({{< ref "#dockerfile" >}})
* [Kendi İmajınızı Hazırlamak]({{< ref "#kendi-imajınızı-hazırlamak" >}})
* [Docker Store & Registry]({{< ref "#docker-store--registry" >}})
* [Kendi Docker Registry’nizi Kurun]({{< ref "#kendi-docker-registrynizi-kurun" >}})

Hızlıca başlayalım! 🙂

---

### Kalıcı Veri Depolama

[İkinci bölümün docker run komutuyla ilgili olan kısmında]({{< ref "docker-serisi-2#docker-run-" >}}) container’lara 
dışarıdan dosya ve dizin bağlanabileceğinden bahsetmiştim. Normalde, ölçeklenebilirliğin ön planda olduğu gerçek ortam 
container’ları dışarıdan bağımsız çalışabilecek şekilde tasarlanmalıdır. Aslında bakarsanız ölçeklenebilirliğin 
maksimize edilmesi için uygulamanızın, [12 Faktör prensibine](https://12factor.net/) uygun tasarlanmış olması gerekir. 
Bu prensiplere uyarak örneğin uygulamanızdan N tane container başlatarak ölçeklenebilirliği rahatlıkla 
sağlayabilirsiniz.

Ölçeklenebilirliğin çok sorun olmadığı durumlarda ya da geliştirme/test ortamlarında dosya/dizin bağlamak size büyük 
kolaylık sağlar. Örneğin uygulama kayıtlarınızı (log) merkezi bir servis yerine yerel dosya sistemine yazıyorsanız, 
ilgili dizini ev sahibi makineye bağlamak akılcı olacaktır. Ya da uygulamalarınızı Tomcat’e dizin açarak yüklüyorsanız 
`webapps` dizinini ev sahibi makineye bağlamak isteyebilirsiniz.

Container’larda kalıcı veri depolama (persistence) söz konusu olduğunda 3 tip depolamadan bahsetmek mümkün:

#### Ev sahibi makineden dizin/dosya bağlayarak depolamak

Bu yöntemde ev sahibi makineyi paylaşımlı dizin gibi düşünebiliriz. Bir kaç örnek senaryo sayarsam:

* nginx kurarken `/etc/nginx/nginx.conf`’u ev sahibi makineden bağlayarak üzerinde değişiklik yapmayı kolaylaştırmak
* nginx imajında hiç bir değişiklik yapmaksızın ev sahibi makinede tuttuğum statik web uygulamamın dizinini 
  `/var/www/html` dizinine bağlayarak doğrudan sunmak
* Ev sahibi makinede tuttuğum, PHP ile geliştirdiğim kod tabanımı container ile paylaşarak yaptığım değişikliklerin 
  sonucunu container üstünden anında görmek
* Ev sahibi makinede bulunan bir dizindeki tüm dosyaları, container’ın içinde çalışacak bir program ile işleyip aynı 
  dizine yeniden yazmak
* Ev sahibi makinede çalışan Docker Engine’in çalışma dizinini, container’a bağlayarak Docker Engine’de bazı işlemler 
  yapmak (ör: [docker-cleanup](https://github.com/meltwater/docker-cleanup))

Peki dosya ya da dizinleri nasıl bağlıyoruz? Yukarıdaki bir kaç örneği gerçekleyelim:

**Dışarıdan /etc/nginx/nginx.conf’u bağlamak:**

```
docker run -d --name nginx1 -v /home/alper/nginx/nginx.conf:/etc/nginx/nginx.conf -p 8000:80 nginx
```

**Dışarıdan statik web uygulamasının dizinini bağlamak:**

```
docker run -d --name nginx2 -v /home/alper/web:/var/www/html -p 8001:80 nginx
```

**Dışarıdan dizin bağlayıp içindeki dosyaları işlemek:**

```
docker run --rm -v /home/alper/test:/test ubuntu sed ‘/kanat/d’ /test/deneme.txt
```

#### Depolayıcı container’lar kullanmak

Kalıcı veri depolamanın Docker’ca yolu, depolayıcı container’lar kullanmaktan geçiyor. Depolayıcı container’ların 
avantajları kabaca şöyle:

* İlgili alanı birden fazla container ile paylaşabilirsiniz.
* Bir container’a birden fazla depolayıcı container bağlayabilirsiniz.
* Depolayıcı container’lar, beraber çalıştıkları container’lar ölse dahi silinmez; tekrar tekrar kullanılabilirler.

Depolayıcı container yaratmak için;

```
docker create -v /dbdata --name dbstore training/postgres /bin/true
```

Depolayıcı container’ı bağlamak için;

```
docker run -d --volumes-from dbstore --name db1 training/postgres
```

yazabilirsiniz. Bu sayede `db1` adındaki container’ınızın içindeki `/dbdata` dizini, aslında `dbstore` container’ından 
bağlanmış olacaktır. Diyelim ki; disk alanını yedeklemek istiyoruz. Yeni bir container ile aynı depolayıcı container’ı 
bağlayarak bu işlemi gerçekleştirebiliriz:

```
docker run --rm --volumes-from dbstore -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
```

Bu komutun yaptıklarını kısaca özetlersek;

* Çalıştıktan sonra silinecek şekilde, Ubuntu imajından yeni bir container yarat (`docker run --rm`)
* Bu container’a dbstore adlı depolayıcı container’ından dışarı açılan dizinleri bağla (`--volumes-from dbstore`)
* Ev sahibi makine üstünde bulunduğum dizini, container içerisindeki `/backup` dizinine bağla. (`-v $(pwd):/backup`)
* Container üstündeki `/dbdata` dizinini sıkıştırarak ev sahibi makine üstünde `/backup/backup.tar` olarak kaydet.

#### Paylaşımlı Disk Alanları Kullanmak

Docker, 1.8.0 sürümünden itibaren disk alanları için sürücü desteğiyle beraber geliyor. Az sonra bahsedeceğim komutlara 
ek olarak; Azure, Google Compute Engine, NFS vb. sürücüleri parametre olarak geçerek (ör: `--volume-driver=flocker`) 
farklı servislerden disk alanlarını da container’larınıza 
[bağlayabilirsiniz](https://docs.docker.com/engine/tutorials/dockervolumes/). Herhangi bir sürücü belirtmezseniz 
öntanımlı olan yerel disk sürücüsü (`--volume-driver=local`) kullanılır ve disk alanı makinenizde oluşturulur.

Yerel disk alanı yaratmak için:

```
docker volume create --name=shared-disk
```

[Yükledikten sonra] [flocker](https://clusterhq.com/flocker/introduction/) sürücüsü ile yaratmak için:

```
docker volume create -d flocker -o size=20GB --name=shared-disk
```

Oluşturduğunuz disk alanını container’daki bir bölüme bağlamak için:

```
docker run -d --name=t1 -v shared-disk:/usr/local/tomcat/webapps -P tomcat
docker run -d --name=t2 -v shared-disk:/usr/local/tomcat/webapps -P tomcat
```

Yukarıdaki şekilde 2 tane Tomcat sunucusu başlatıp aynı disk alanını ikisine birden bağlayabiliyoruz.

### Çevresel Değişkenler

İster web uygulaması olsun, ister bir API uygulaması; bir uygulamanın en önemli kısımlarından biri yapılandırma 
kısmıdır. Bazen bu yapılandırma, uygulamada kullanılan 3. parti servislerin erişim bilgileridir, bazense uygulamanın 
nasıl davranacağını belirleyen kritik roldeki bir anahtardır. Yalnızca bir anahtarın değerini değiştirerek gerçek bir 
veritabanı yerine örnek verilerle çalışmasını sağlayabilir ya da uygulama içindeki bir özelliği komple açıp 
kapatabilirsiniz.

Eski tip yazılım paketleme yöntemlerinde; uygulama içerisinde tutulan yapılandırma dosyalarının değerleriyle oynayıp 
birden fazla paket çıkarmak oldukça yaygın. Docker’da ise imajınızı gerçek ortama göre hazırlayıp dışarıdan vereceğiniz 
çevresel değişkenlerle her şeyi yönetebilirsiniz.

Tanımlayacağınız çevresel değişkenler, container içerisinde işletim sistemi seviyesinde ve tüm uygulamalarda 
erişilebilir durumda olacaktır. Bu sayede yapılandırma dosyalarında ya da çalıştırma betiklerinde çevresel 
değişkenlerinizi kullanabilirsiniz. Bu sayede son derece esnek imajlar yaratmanız mümkün.

Çevresel değişkenlerle ilgili serinin ilerleyen bölümlerinde gerçekçi örnekler vereceğim için şimdilik Tomcat ve MySQL 
özelinde 2 örnekle bu kısmı noktalıyorum:

#### Tomcat Manager Uygulaması Şifresini Belirlemek

```
docker run -d -p 8080:8080 -e TOMCAT_PASS=”mypass” tutum/tomcat
```

> Burada tutum’un imajını kullanma sebebim; orjinal Tomcat imajlarında çevresel değişkenler ile şifre belirleme 
> özelliğinin bulunmuyor oluşundan kaynaklanıyor.

#### MySQL Yönetici Şifresini Belirlemek

```
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql
```

Docker Hub’dan (yeni adıyla Docker Store) indirdiğiniz imajların hangi çevresel değişkenleri kullandığını anlamak için 
ilgili sayfalarına bakabilirsiniz. Maalesef bazı imajlarda bu detaylar yeterince belgelendirilmediği için imajların 
kaynak kodlarındaki [Dockerfile](https://medium.com/commencis/docker-serisi-3-docker-engine-bolum-2-a7c6c5f50851#6aea) 
dosyalarını incelemeniz gerekebilir.

### Bağlantı Noktaları

Bağlantı noktaları (port) dış dünya ile container’larınızın iletişimini sağlar. Bir web uygulaması geliştirdiğimizi 
varsayarsak, container’daki 80. bağlantı noktasını ev sahibi makinedeki herhangi bir bağlantı noktasına bağlamadan 
uygulamamıza erişemeyiz.

Docker, çalışma zamanında özellikle belirtmediğiniz sürece, öntanımlı olarak herhangi bir bağlantı noktasını dışarıya 
açmayacaktır. İmaj hazırlanırken bağlantı noktalarının tanımları da [Dockerfile]({{< ref "#dockerfile" >}}) içine 
yazılır. Ancak yine de container’ı çalıştırırken, `-p` ya da `-P` ile ev sahibi makineye bağlamazsanız dışarıdan 
erişilmez olacaktır.

Container’ın tanımladığı bağlantı noktalarını `docker ps` komutuyla görebilirsiniz: `0.0.0.0:80->80/tcp`, `443/tcp` Bu 
çıktıya baktığımızda 80. bağlantı noktasının ev sahibi makinedeki tüm ağlara bağlandığını, 443. bağlantı noktasının 
ise bağlanmadığını görüyoruz. Sadece bağlanmış olanları görmek için `docker port container_adi` (örnek: 
`docker port nginx`) komutunu da kullanabiliriz.

#### 80 (HTTP) ve 443 (HTTPS) Bağlantı Noktalarını Bağlayalım

Aşağıdaki komutla ev sahibi makinenin 80. ve 443. bağlantı noktalarını, container’daki 80. ve 443. bağlantı noktalarına 
bağlayabiliriz:

```
docker run -d --name nginx -p 80:80 -p 443:443 nginx
```

#### Bağlantı Noktalarını Rastgele Bağlayalım

Java ile yazılmış bir Spring Boot uygulamanız olduğunu varsayalım. Spring Boot’un avantajlarından biri, Tomcat’i 
uygulamayla birlikte JAR olarak paketleyebiliyorsunuz. Şimdi uygulamamızı Docker imajı haline getirdiğimizi ve 
yukarıdaki yöntemle başlattığımızı düşünelim. _**Aynı ev sahibi makine üstünde bir bağlantı noktasını yalnızca bir 
container kullanabilir**_. Bu nedenle yeniden yukarıdaki yöntemi kullanmak isterseniz yalnızca `-p 81:80 -p 444:443` 
yazarak başlatabilirsiniz.

Ölçeklendirilebilirliğin önemli olduğu durumlarda bağlantı noktasını sürekli elle artırarak yeni container açmak pek 
kabul edilebilir bir yöntem değil. Bu nedenle doğru olan yöntem `-P` parametresini kullanarak container’da tanımlanmış 
tüm bağlantı noktalarının ev sahibi makinedeki rastgele bağlantı noktalarına atanmasını sağlamaktır. Serinin ileriki 
bölümlerinden "Günlük Kullanım Bölüm 1" içerisinde bu yöntemden daha detaylı bahsedeceğim.

Rastgele bağlantı noktası ataması için aşağıdaki komutu kullanabilirsiniz:

```
docker run -d --name nginx -P nginx
```

### Dockerfile

Dockerfile ile ilgili en detaylı ve güncel bilgiyi [kendi sitesinde](https://docs.docker.com/engine/reference/builder/) 
bulabilirsiniz. Bu kısımda kısaca Dockerfile’ı neden ve nasıl kullanmanız gerektiğini anlatmaya çalışacağım. 
Dockerfile, özetle bir Docker imajını tarif eder. Hangi imajı baz alacağımızı, baz aldığımız imajın üstünde 
çalıştıracağımız komutları, oluşturacağımız dizinleri, dış kullanıma açılabilecek çevresel değişkenleri, bağlantı 
noktalarını ve disk alanlarını bu dosyada belirtiyoruz. Yine bir örnek üstünden ilerleyelim:

{{< gist tunix ce6ad7fc6c8c075ab20ee7877307cb23 >}}

Her Dockerfile, `FROM` satırıyla başlar. İmajımızı, `node:6.2-slim` imajını baz alarak yaratacağız. `-slim`’i imajı 
mümkün olduğunca küçültmek amacıyla kullanıyorum. İmajı ilk inşa ettiğimiz noktada ne kadar küçükten başlatabilirsek o 
kadar iyi. Bu nedenle [Alpine Linux](https://alpinelinux.org/), 
[*-slim](https://store.docker.com/images/e6658267-cc55-421e-b5be-5e69460fb0d1) vb. seçenekleriniz varsa mutlaka 
kullanın. Örneğin Java’yla yazılmış uygulamanızı Debian ya da Ubuntu imajını baz alıp üstüne Java kurarak oluşturmak 
yerine, doğrudan [java](https://store.docker.com/images/199a18b1-511b-47fd-b287-a41555fafb9f) imajlarını tercih 
etmelisiniz.

Zorunlu olmasa da, [Docker Store](https://store.docker.com/) vb. yerlerde sorgulanabilmesi ve sorumlunun açıkça 
görülebilmesi açısından `MAINTAINER` satırını kullanmanız iyi olur.

`ADD` komutuyla, bulunduğum dizini container'ın `/srv` dizinine kopyalıyorum. Uygulamamı bu dizinde tutuyor olacağım. 
Bu tercih tamamen size kalmış. İsterseniz `/app` vb. bir dizin de kullanabilirsiniz. Ya da Tomcat imajını baz 
alıyorsanız doğrudan uygulamanızı `/usr/share/tomcat/webapps` gibi bir dizin altına da kopyalayabilirsiniz. Bir sonraki 
satırda (`WORKDIR`) ise bundan sonraki komutların çalıştırılacağı dizini `/srv` olarak belirtiyorum.

> Dockerfile’daki her satır diğer komutlardan bağımsız çalışır. `WORKDIR /srv` yerine `cd /srv` yazarsanız bu sonraki 
> komutların yine `/` dizininde çalışmasına sebep olacaktır.

Serinin ilk bölümündeki "[İmaj ne demek?]({{< ref "docker-serisi-1#imaj-ne-demek" >}})" kısmında bahsettiğim gibi, 
Docker imajları katmanlardan oluşur. Dockerfile’da yazdığınız, imaja bir şey ekleyen (`ADD`, `COPY`, `RUN` vb.) her 
satır, imaja yeni bir katman ekler; dolayısıyla boyutunu artırır. Bu nedenle, dosyanın yukarıdan aşağıya doğru 
okunduğunu unutmayarak, değişmeyecek kısımları mümkün olduğunca yukarıya eklemeli ve komutları zincirlemelisiniz. 8. 
satırdaki `apt` komutlarının zincirlenmesi, işletim sistemi güncellemelerinin tek bir katmanda yer almasını sağlıyor.

9–12. satırlar arasında uygulamanın çalışması için gereken bağımlılıkları kurup (`RUN`), uygulamayı derliyoruz.

14. satırda `NODE_ENV` adında bir çevresel değişken tanımlayıp (`NODE_ENV`) öntanımlı değerini `production` yapıyoruz. 
Bu, yukarıda bahsettiğim gerçek ortama yönelik imaj oluşturma prensibiyle de örtüşüyor. Çalışma zamanında 
`-e NODE_ENV=development` parametresiyle öntanımlı değeri ezebiliyoruz.

15. satırda, 3000. bağlantı noktasının dışarıdan kullanılabileceğini (`EXPOSE`) belirtiyorum. Yukarıda belirttiğim 
gibi, çalışma zamanında `-p 3000:3000` ya da `-P` gibi bir parametreyle bu bağlantı noktasını ev sahibi makineye 
bağlamam gerekiyor.

Son olarak 17. satırdaki `CMD` komutuyla öntanımlı olarak, daha önce `WORKDIR` ile belirlediğimiz dizindeki (`/srv`) 
`app.js` dosyasının çalıştırılacağını belirtiyoruz. Bu satırda `CMD` yerine `ENTRYPOINT` kullanarak da aynı işi 
yapabilirdik ama CMD daha esnek olduğundan onu tercih edebiliriz. Serinin 
[ikinci bölümünde]({{< ref "docker-serisi-2#docker-run-" >}}) bahsettiğim gibi `docker run` komutlarının sonunda `cat` 
vb. terminal komutlarını çağırabiliyoruz. Bunu `CMD`’e borçluyuz. `ENTRYPOINT` kullanıyor olsaydık, imaj için 
belirlenen komut dışında bir komutu çağıramıyor olacaktık.

Dockerfile’la ilgili bu kısmı diğer kullanışlı bazı komutları açıklayarak kapatayım:

#### LABEL

Oluşturulacak imajın sahip olacağı öntanımlı etiketleri belirler. Ölçeklenebilirliğin önemli olduğu durumlarda 
`docker run` ile etiket vermektense bu şekilde etiketler tanımlamak daha mantıklı ve kolay.

```
LABEL type="node" purpose="api" role="core" description="REST API"
```

#### VOLUME

Yukarıdaki [Kalıcı Veri Depolama]({{< ref "#kalıcı-veri-depolama" >}}) kısmında bahsettiğim gibi container’lara 
dışarıdan disk alanları bağlayabiliyoruz. Dockerfile’a ekleyeceğiniz `VOLUME` komutlarıyla container içindeki disk 
alanlarının dışarıdan bağlanabileceğini belirtmiş oluyorsunuz.

```
VOLUME [“/data”]
VOLUME /data
```

#### USER

Container içinde çalışan süreçler siz aksini belirtmediğiniz sürece `root` kullanıcısıyla çalıştırılır. Bu da 
Docker’daki olası bir açığın kötüye kullanılmasıyla istenmeyen sonuçlara sebebiyet verebilir. Bu tip durumların önüne 
geçmek için özellikle proje bağımlılıklarını kurmadan önce `USER` komutunu vermiş olmanız iyi olur. Bu sayede 
bağımlılıkların dosya/dizin sahipliği de bu kullanıcıya ait olur.

#### ARG

Çevresel durumların yetişmediği bazı durumlarda imajlarınızı parametrik üretmek isterseniz `ARG` komutuyla değişkenler 
ve öntanımlı değerlerini tanımlayabilirsiniz. Bu tanımlar `docker build` komutunda, imajınız yaratılırken kullanılır.

```
ARG user1=someuser
ARG buildno=1
```

şeklinde değişkenler tanımladığınızı varsayarsak; örneğin buildno’yu imaj oluşturulurken değiştirmek isterseniz:

```
docker build --build-arg buildno=2 -t tunix/alperkan.at .
```

şeklinde yapabilirsiniz.

#### HEALTHCHECK

Docker 1.12 ile eklenen [bu özellik](https://docs.docker.com/engine/reference/builder/#/healthcheck) sayesinde 
container’ın olması gerektiği gibi çalışıp çalışmadığını kontrol eden bir komutun belirli sıklıkta ve belirli zaman 
dilimlerinde çalışmasını sağlayabilirsiniz. Bu metrikleri takip eden başka servislerle yeni bir container 
başlatılmasını, mevcut container’ın yeniden başlatılmasını sağlayabilir ya da çeşitli alarm sistemlerini 
tetikleyebilirsiniz.

```
HEALTHCHECK --interval=5m --timeout=3s \
CMD curl -f http://localhost/ || exit 1
```

### Kendi İmajınızı Hazırlamak

Diyelim ki elinizde, Docker’laştırmak istediğiniz bir projeniz var; ne yapmalısınız? Bu sorunun cevabını vermek için
[Monitise MEA](https://medium.com/u/f570294a852c?source=post_page-----a7c6c5f50851--------------------------------)’da 
açık kaynak olarak GitHub’a koyduğumuz 
[Gerrit Dashboard Server](https://github.com/monitise-mea/gerrit-dashboard-server) projesini örnek olarak kullanacağım.

Projeyi kendi makinenize indirdikten sonra;

```
npm install
gulp
```

komutlarıyla bağımlılıkları kurup projeyi derleyin. Son komutla, [Node.js](https://nodejs.org/en/) ile yazılmış 
projenin derlenmiş hali `dist` dizinine yerleştiriliyor. Bu dizini, 
[node](https://store.docker.com/images/e6658267-cc55-421e-b5be-5e69460fb0d1) imajlarından birini baz alan bir 
container’ın içine kopyalayıp çalıştırmalıyım. 
[Dockerfile](https://github.com/monitise-mea/gerrit-dashboard-server/blob/master/Dockerfile)’a bakarsak;

{{< gist tunix b8e1e76ffbfd6a0f2408dea843411e1f >}}

Gerrit Dashboard Server projesinden Docker imajı üretme işini Travis CI üstünde 
[yapıyoruz](https://travis-ci.org/monitise-mea/gerrit-dashboard-server). Öncelikle imajın doğru şekilde üretildiğinden 
emin olmak için kendi makinemizde kurulu olan Docker Engine üstünde deneyelim:

```
docker build -t gerrit-dashboard-server:1.0.2 .
```

İşlem başarılı bir şekilde sonuçlandığında `docker images` komutunu verdiğinizde imajın oluşturulduğunu 
doğrulayabilmelisiniz.

> İmajı dağıtıma çıkarmadan önce kullanılabilecek parametrelerle birlikte doğru şekilde çalıştığından emin olun.

Oluşturduğunuz imajı başka bir makineye kopyalamak için 2 seçeneğiniz var:

* Docker Engine’den arşivlenmiş şekilde dışa aktarmak
* Docker Store benzeri bir servise yüklemek

Docker Engine’den arşivlenmiş şekilde dışa aktarmak için;

```
docker save -o ~/Desktop/gerritdashboard-1.0.2.tar \
    gerrit-dashboard-server:1.0.2
```

komutunu kullanabilirsiniz. Oluşan tar dosyasını diğer makineye kopyaladıktan sonra yeniden içeri aktarım yapmak içinse;

```
docker load -i gerritdashboard-1.0.2.tar
```

komutunu kullanabilirsiniz.

### Docker Store & Registry

Docker imajlarını saklamanın en kolay yollarından birisi [Docker Store](https://store.docker.com/)’a yüklemek. 
Çoğunlukla baz imajları indirmek için en temel kaynak olarak kullandığımız [Docker Hub](https://hub.docker.com/) (yeni 
adıyla [Docker Store](https://store.docker.com/)) aslında kendi imajlarımıza da ev sahipliği yapabilecek bir depo. 
Genele açık imajlarınızı sınırsızca yükleyebileceğiniz servis, özel imajlarınız için 5 adede kadar ücretsiz olanak 
sağlıyor. Sonrası içinse [ücretli üyeliklerden](https://hub.docker.com/billing-plans/) birine geçilmesi gerekiyor.

Eğer oluşturduğunuz imajı herkese açık olarak yüklemenizde bir sakınca yoksa [Docker Hub](https://hub.docker.com/)’a 
ücretsiz olarak yükleyebilirsiniz. Bunun için öncelikle servise kayıt olmalısınız. Kayıt olduktan sonra kullanıcı 
bilgilerinizle giriş yapın ve yeni bir Docker imaj deposu (repository) oluşturun. Bunun için tercih edebileceğiniz 2 
yol var:

#### Manuel Depo

{{< figure src="docker_hub_manuel_repo.png" caption="Docker Hub’da manuel depo oluşturma formu" >}}

Giriş yaptıktan sonra sağ üstteki Create menüsünden Create Repository’e basın. Formdaki alanları doldurduktan sonra 
Create tuşuna basın. Şimdi imajı yükleme zamanı! 🤘🏻

Yükleme yapabilmek için bilgisayarınızdan Docker Hub’a giriş yapmak için;

```
docker login
```

komutunu verin. E-posta adresinizi ve şifrenizi yazıp doğrulamadan geçtikten sonra ev dizininizdeki 
`~/.docker/config.json` dosyasına ilgili servise ait giriş bilgileri (yetki kodu ve e-posta adresiniz) yazılacaktır. 
Bu işlem, aynı servisi kullandığınız sürece tek seferliktir; tekrarlamanız gerekmez.

Yukardaki son [örneğimizden]({{< ref "#kendi-imajınızı-hazırlamak" >}}) devam edelim. İmajımızı 
`gerrit-dashboard-server:1.0.2` adıyla oluşturmuştuk. Docker Engine, imajı uzaktaki bir servise yükleyeceğimizde nereye 
yükleyeceğini imajın adından [buluyor]({{< ref "docker-serisi-2#docker-push-registrygitlabcomtunixalperkanat105" >}}). 
Bu nedenle imajı yeniden oluşturmamıza gerek yok; etiketleri kullanarak işlemi gerçekleştirebiliriz. Docker Hub servisi 
için imajı etiketleyelim:

```
docker tag gerrit-dashboard-server:1.0.2 docker.io/tunix/gerritdashboard-server:1.0.2
```

Artık imajı Docker Hub’a yükleyebiliriz:

```
docker push docker.io/tunix/gerritdashboard-server:1.0.2
```

İşlem node imajını baz alıp üstüne sadece kendi katmanlarımızı eklediğimizden hızlıca tamamlanacaktır. Artık Docker 
Engine yüklü olan herhangi bir makinede;

```
docker pull docker.io/tunix/gerritdashboard-server:1.0.2
```

komutuyla imajı indirip kullanmaya başlayabilirsiniz.

#### Otomatik Depo

{{< figure src="docker_hub_otomatik_depo.png" caption="Docker Hub’da otomatik depo oluşturma formu" >}}

Giriş yaptıktan sonra sağ üstteki Create menüsünden Create Automated Build’a basın. Karşınıza yukarıdaki gibi GitHub 
ya da Bitbucket arasında seçim yapmanız gereken bir ekran gelecek. Seçiminizi yaptığınızda ilgili servisin sitesine 
gidip kod depolarınıza erişim hakkı vermeniz gerekecektir. Bu adımı gerçekleştirdikten sonra kod depolarınızı seçmeniz 
için aşağıdaki gibi bir ekran göreceksiniz:

{{< figure src="docker_hub_repo_secimi.png" caption="GitHub kod depolarını listeleyen sayfadan istediğinizi seçin" >}}

Seçiminizi yaptığınızda karşınıza otomatik depo oluşturmanın son adımı olan form çıkacaktır; formu doldurup Create 
tuşuna bastığınızda deponuz oluşturulacak ve ilk derleme işlemi için beklemeye başlayacaktır. Aslında kod deposu 
seçimini yaptığınızda arkaplanda seçim yaptığınız depoya bir webhook (ağ kancası? 😂) eklenir. Kod deposuna yeni kod 
parçacığı gönderdiğinizde Docker Hub’da otomatik olarak bir derlenme süreci tetiklenecek ve oluşturulan imajınız 
sayfada yer alacaktır.

{{< figure src="docker_hub_proje_sayfasi.png" caption="GitHub’daki digitalocean-dyndns adlı projemin Docker imajları Docker Hub tarafından otomatik oluşturuluyor." >}}

#### Docker Registry

Docker Hub bu servisi verirken arkaplanda [Docker Registry](https://github.com/docker/docker-registry) (yeni adıyla 
[Docker Distribution](https://github.com/docker/distribution)) adı verilen açık kaynak kodlu bir yazılımı kullanıyor. 
Eğer imajlarınızı yüklemek için bir registry’e para vermek istemiyorsanız kendi registry’nizi kurabilirsiniz. Ancak 
böyle bir tercihte bulunacaksanız kurulum yapacağınız sunucunun yönetimini ve maliyetlerini de göz önünde bulundurun. 
Öte yandan proje kodlarını git vb. bir SKS (sürüm kontrol sistemi) üstünde tuttuğunuz sürece geriye dönüp imajı yeniden 
yaratmanız mümkün olabileceğinden riskiniz o kadar da yüksek değil. Yine de kodunuzun o anki hali değilse bile 
bulunduğu ortamın ve bağımlılıkların sıkıntı çıkarabileceğini unutmayın. 🤔

### Kendi Docker Registry'nizi Kurun

[Monitise MEA](https://medium.com/u/f570294a852c?source=post_page-----a7c6c5f50851--------------------------------)’da 
hibrid bir geliştirme ve test ortamımız var. Klasik şekilde bir VM üstüne kurulu Tomcat’e yüklenen sayısız projemiz 
olduğu gibi, yeni projelerimizde Docker’ı kullanma seçeneğini her zaman göz önünde bulunduruyoruz. Gerçek ortamda 
Docker’ı hiç kullanmayan projelerde dahi bazı durumlarda geliştirme ve test ortamı için Docker’ı tercih edebiliyoruz. 
Dolayısıyla bu projelerin Docker imajlarını üretmemiz ve sunucular arasında taşımaya ihtiyacımız var ve Docker Registry 
burada devreye giriyor.

Özetle, Docker Registry bir API’dan ve disk üstünde imaj katmanlarını yöneten bir sistemden oluşuyor. API v1 iken 
[Docker Registry](https://github.com/docker/docker-registry) adını taşırken, v2 ile birlikte 
[Docker Distribution](https://github.com/docker/distribution) adını aldı. Her ikisi de Docker Store’dan 
[indirilebilir durumda](https://store.docker.com/images/d93c7069-a612-4019-ade6-8c3b0a73acd9). Kurmak için;

```
docker run -d -p 5000:5000 --name registry registry:2
```

komutunu vermeniz yeterli. Bu durumda aşağıdaki öntanımlı değerler geçerli olur:

* İmajlarınız container içindeki `/var/lib/registry` dizini altına yazılır. Öntanımlı olarak filesystem sürücüsü 
  kullanılır. Alternatifler [şurada](https://docs.docker.com/registry/storage-drivers/).
* Registry’nize, herhangi bir SSL sertifikasına sahip olmadığından, HTTP üstünden ulaşırsınız.
* Registry’niz herkesin yüklemesine ve indirmesine açık şekilde çalışır; kullanıcıların önce giriş yapmaları gerekmez. 
  Kullandığınız ağın dışarıya açık olmaması durumunda bu şekilde de çalışabilirsiniz.

Registry kurulumuyla ilgili en güncel bilgiyi [şuradan](https://docs.docker.com/registry/deploying/) bulabilirsiniz. 
Benim tavsiyem; registry için ev sahibi makineye ek disk vermeniz ve container’daki `/var/lib/registry` dizinini ev 
sahibi makinedeki `/registry` dizinine bağlamanız yönünde. Ayrıca registry’i kullanan tüm makinelerde ek ayar 
(`--insecure-registry`) yapmamak için sunucuya geçerli bir sertifika kurmanızda fayda var. 
[LetsEncrypt](https://letsencrypt.org/) gibi güzelliklerin olduğu günümüzde yapmazsanız ayıp! 😉 Tabii sertifika işini 
registry’nin önüne bir HTTP sunucusu ([nginx](https://nginx.org/), [Apache](http://httpd.apache.org/) vb.) koyarak da 
çözebilirsiniz. Hatta HTTP sunucusu yerine [https-proxy](https://hub.docker.com/r/yajo/https-proxy/)’i de 
kullanabilirsiniz.

Son durumda registry kurulumu için aşağıdaki gibi bir komuta ihtiyacınız var:

```
docker run -d --name registry \
    -p 5000:5000 \
    --restart=always \
    -v /registry:/var/lib/registry \
    registry:2
```

[https-proxy](https://hub.docker.com/r/yajo/https-proxy/) kullanmak isteyenlere bonus olarak örnek komutu ekleyeyim:

```
docker run -d --name registry-ssl \
    -e KEY=”$(cat registry.key)” \
    -e CERT=”$(cat registry.crt)” \
    -p 443:443 \
    -e PORT=5000 \
    --restart=always \
    --link registry:www \
    yajo/https-proxy
```

> registry container’ını yaratırken kullandığınız ismin, https-proxy’i yaratırken kullandığınız komuttaki --link 
> bölümündeki registry ismiyle aynı olduğundan emin olun.

Diyelim ki; registry’inize ulaştığınız adres `docker.example.com` olsun. Bu durumda imajlarınızı buraya yüklemek için 
`docker.example.com/tunix/alperkan.at:1.0.2` gibi isimlendirmelisiniz. `docker push` komutuyla imajınızı yüklerken, 
Docker Engine otomatik olarak HTTPS protokolünü tercih edecektir. Bu nedenle SSL adımını atladıysanız ve kendi 
makinenizden yükleme yapıyorsanız Docker Engine ayarlarında yeni registry’inizi "Insecure Registries" bölümünden 
ekleyin. Linux’da bu arayüz geliyor mu emin değilim ama [şuradaki adımları](https://docs.docker.com/registry/insecure/) 
takip edebilirsiniz.

{{< figure src="docker_for_mac_advanced_tab.png" >}}

---

Bu bölümünün de sonuna geldik. Bir sonraki bölümde Docker Compose’dan ve özellikle birden fazla parçaya ihtiyaç duyan 
projelerinizi Docker ile nasıl kolayca ayağa kaldırabileceğinizden bahsedeceğim.

Gidişâta göre bu planda zaman zaman değişiklikler yapacak olsam da serinin tüm bölümlerinin planına 
[şuradan](https://www.evernote.com/l/AB7CctYtJkpMUJsae1_3FgzIXgMY5MvFQhU) ulaşabilirsiniz.
