---
title: "Docker Serisi #2 -- Docker Engine Bölüm 1"
date: 2016-09-26
slug: docker-serisi-2
tags:
    - yazılım
    - docker
    - docker serisi
    - container
    - sanallaştırma
    - linux
    - devops
---

Docker Serisi’nin [ilk bölümünde]({{< ref "docker-serisi-1" >}}) sanallaştırmanın ne olduğundan, container 
teknolojisinden ve temel Docker kavramlarından bahsetmiştim. Serinin bu bölümünde temel Docker komutlarının 
kullanılmasından bahsedeceğim. Hazırsanız başlayalım! 🙂

### docker \<cmd\> ...

Öncelikle tüm docker komutları **docker** kelimesiyle başlıyor. Serinin sonraki bölümlerinde bahsedeceğim eklentiler 
ise **docker-** ön ekiyle _(docker-compose, docker-swarm gibi..)_ başlıyorlar. Hiç bir parametre vermeden yalnızca bu 
komutları yazacak olursanız ilgili komuta ait yardım metinleri ekranınıza çıkacaktır. Dolayısıyla docker’ı ya da 
eklentilerini kurduktan sonra, kurulumunuzun başarılı olduğunu anlamak için ilk yapmanız gereken şey herhangi bir 
parametre vermeden çalıştırdığınızda yardım metinlerini görüp göremediğiniz olmalı.

Docker komutları `info`, `build`, `exec`, `ps`, `rm`, `run` gibi kelimelerden oluşuyor ve bir üst paragrafta 
bahsettiğim yardım metinlerinde tam listesini görebilirsiniz. Bu komutların yardım metinlerine ise

> `docker help build` ya da
> `docker build -h` ya da
> `docker build --help`

yazarak ulaşabilirsiniz. Üçü de aynı çıktıyı verecektir. Her komutu kullanmadan önce başka neler yapabileceğinizi 
anlamak/öğrenmek için bu komutları yazarak denemeler yapmanız faydalı olacaktır. Serinin tüm yazılarında yalnızca sık 
kullanılan parametreleri anlatıyor olacağım.

Devam etmeden önce docker kurulumunuzun başarılı olduğundan ve çalıştığından emin olmak için `docker info` komutunu 
verin:

{{< figure src="docker_info_ciktisi.png" caption="`docker info` komutunu verdiğinizde buna benzer bir çıktı almalısınız" >}}

### docker ps

{{< figure src="docker_ps_a_ciktisi.png" caption="`docker ps -a` komut çıktısı" >}}

Docker Engine üstünde bulunan container’ları listeleyen komut. Öntanımlı olarak kapalı ya da bir sebepten dolayı 
durmuş olan container’lar gösterilmez. Hepsini görebilmek için bu komuta `-a` ya da `--all` parametresini vermelisiniz. 
Şimdi gelin bu komuttaki kolonları adım adım inceleyelim:

#### CONTAINER ID

İlgili container’a atanmış benzersiz bir tanımlayıcı. Docker komutlarını kullanırken (örneğin silme işlemi için) 
container’a referans vermek için container adını kullanabileceğiniz gibi bu ID’yi de kullanabilirsiniz.

#### IMAGE

Container’ın hangi imajdan türediğini belirtir. `:6.2-slim` gibi belirteçler, o imajın sürüm numarasını belirtir. 
Sürüm numarası belirtilmemiş imajlar ise öntanımlı olarak `:latest` yani en güncel sürüm olarak kullanılmış demek 
oluyor.

#### COMMAND

[Bir önceki bölümde]({{< ref "docker-serisi-1" >}}) bahsettiğim gibi container’lar içlerinde tek bir süreç (process) 
çalıştırmak üzere tasarlanıyorlar. İlgili container’ı çalıştırmak için hangi komutun kullanıldığını bu bölümden 
görebilirsiniz. Terminal penceresine sığabilmesi için kısaltılmış formda gösterilen bu komutların tam halini görmek 
için `--no-trunc` parametresini (`docker ps -a --no-trunc`) kullanabilirsiniz.

#### CREATED

Container’ın yaratıldığı anı şimdiki zamanı baz alarak belirtir.

#### STATUS

Container açıksa ne kadar süredir çalıştığını şimdiki zamanı baz alarak belirtir ya da eğer kapalıysa varsa çıkış 
koduyla birlikte yine şimdiki zamanı baz alarak kapanış zamanını belirtir.

#### PORTS

Container’ın açmak istediği erişim noktalarını (port) gösterir. Her yönlendirmedeki ilk kısım ev sahibi makinedeki 
(host), ikinci kısım ise container’ın içindeki erişim noktasını gösterir. Ekran görüntüsünde görüleceği üzere ilk 
container’da herhangi bir port yönlendirmesi bulunmuyor. İkincisinde ise ev sahibi makinenin tüm iletişim 
arabirimlerinden (interface) gelecek trafiğe açık olacak şekilde 32769 numaralı erişim noktasına, container’ın 80. 
erişim noktasına; 32768 numaralı erişim noktası ise container’ın 443. erişim noktasına yönlendirilmiş.

#### NAMES

Container’ın ismi. Container’la ilgili bir komut vereceğinizde bu isimle referans verebilirsiniz. İsim atanmayanlara 
Docker tarafından otomatik olarak rastgele bir isim atanır.

Eğer Mac ve Docker 1.11.x sürümünü kullanıyorsanız, Docker’ı Virtualbox ya da VMWare gibi bir hypervisor içinde 
kullanıyor olma ihtimaliniz yüksek. Virtualbox kullandığınızı varsayarsam, yukarıdaki erişim noktası yönlendirmesinde 
ev sahibi makine sizin makineniz değil, Virtualbox içinde çalışan makinedir. Bu durumda yukarıdaki örnekte çalışan 
nginx’e, makinenizin IP adresiyle değil, Virtualbox’ta açık olan sanal makinenin IP adresiyle (genelde 192.168.99.100) 
bağlanmalısınız.

> İpucu: Dilerseniz sanal makinenin IP adresini docker.local adıyla /etc/hosts dosyasına ekleyerek IP adresi girme 
> zahmetinden kurtulabilirsiniz.

Henüz Docker 1.12'yi yüklemediyseniz mutlaka yükleyin. Bu sayede macOS’un dahili sanallaştırma özelliklerinden 
faydalanıyor; dolayısıyla da daha verimli ve daha az güç tüketerek Docker ile çalışabiliyor olacaksınız. Bu sürümle 
birlikte gelen bir çok özellikten serinin bir sonraki yazısında bahsediyor olacağım. **Bir üst paragraftan farklı 
olarak; 1.12 sürümünü yüklediğiniz takdirde, çalıştıracağınız tüm servisler doğrudan localhost ya da 127.0.0.1 
üstünden erişilebilir olacaktır.**

### docker images

{{< figure src="docker_images_ciktisi.png" caption="`docker images` komut çıktısı" >}}

Docker Engine içerisine indirilmiş (bknz: [docker pull]({{< ref "#docker-pull-tomcat8-jre8" >}})) imajların listesini 
döner. Bu imajlar Docker Hub’dan indirilmiş ya da ev sahibi makine üstünde oluşturulmuş 
(bknz: [docker build]({{< ref "#docker-build--t-registrygitlabcomtunixalperkanat105-" >}})) olabilir. Yeni 
başlattığınız container’ların imajları ve onların baz aldığı disk imajları burada listelenecektir. Container 
oluşturulurken ya da başlatılırken baz alınan bir imaj bu listede bulunmuyorsa öncelikle indirilecektir.

### docker search tomcat

[Docker Hub](https://hub.docker.com/)’daki tomcat imajları arasında arama yapmanızı sağlar. Komut çıktısında imajın 
adını, tanımını, kaç yıldız aldığını (popülerliğini), resmi olup olmadığını ve son olarak otomatik derlenip 
derlenmediğini görebilirsiniz.

{{< figure src="docker_search_tomcat_ciktisi.png" caption="`docker search tomcat` komutunun çıktısı" >}}

[Docker Hub](https://hub.docker.com/)’a tüm kullanıcılar imaj atabildikleri için mümkün olduğunca resmi imajları 
kullanıyor olmanız önem taşıyor. Resmi olmayan imajlarda ise otomatik derlenenleri tercih etmeniz daha doğru olacaktır.

### docker pull tomcat:8-jre8

Yeni bir container başlatabilmek için öncelikle o container’ın çalışacağı imaja sahip olmalısınız. Serinin bir önceki 
yazısındaki “[İmaj ne demek?]({{< ref "docker-serisi-1#imaj-ne-demek" >}})” bölümünde bahsettiğim gibi, bir disk imajı 
çeşitli katmanlardan oluşuyor ve imaj değiştikçe yeni katmanlar ekleniyor. Bu bilgiden yola çıkarak; yukarıdaki komut 
ile Tomcat 8.x’in Java 8 ile çalışan son sürümünü tüm katmanlarıyla indiriyoruz. Sondaki, : işaretinden sonraki kısım 
(`8-jre8`), indireceğimiz imajın sürüm kodunu ifade ediyor. Sürüm kodu olarak hiç bir şey yazmamış olsaydık 
(`docker pull tomcat`) öntanımlı olarak `:latest` yazdığımız varsayılacak ve tomcat’in son sürümü indirilecekti.

Diyelim ki; indirdiğiniz zamandan bu yana Tomcat 8 Java 8'de bazı değişiklikler yapıldı. Bu komutu tekrar 
verdiğinizde, Docker yalnızca bilgisayarınızda mevcut olan katmandan sonraki katmanları indirerek işlemin çok daha 
hızlı gerçekleşmesini sağlayacaktır.

Diyelim ki; Tomcat 8 Java 8'i baz alan başka bir imajı indireceksiniz. Bu durumda da Docker yalnızca bilgisayarınızda 
mevcut olan katmandan sonraki katmanları inderecektir.

### docker build -t registry.gitlab.com/tunix/alperkan.at:1.0.5 .

Yeni bir container imajı oluşturmak için bu komutu kullanabilirsiniz. Detaya inmeden belirteyim; bu komutun 
çalışabilmesi için projenin içinde en az bir adet Dockerfile bulunması gerekiyor. Dockerfile’la ilgili detayları bu 
bölümün ilerleyen kısımlarında bulabilirsiniz.

`-t` parametresiyle oluşturduğunuz sürümü etiketlemiş oluyorsunuz. Yani bu durumda oluşturduğum imaj 
`registry.gitlab.com/tunix/alperkan.at:1.0.5` adıyla etiketlenmiş olacak. Sondakinin sürüm numarası olduğunu daha önce 
belirtmiştim. Peki baştaki kısım neyin nesi?

Aslında sadece `alperkan.at:1.0.5` şeklinde de oluşturabilirdim bu imajı. Ve daha sonrasında;

```
docker tag alperkan.at:1.0.5 registry.gitlab.com/tunix/alperkan.at:1.0.5
```

yapabilirdim. Baştan bu şekilde yapmamın ilk sebebi docker tag gibi ikinci bir komut vermemek. Bu şekilde etiketleme 
sebebim ise docker’da bir imajı bir depoya yollayabilmemin tek yolunun, imajın adını o depoyla etiketlemek olması. Bu 
durumda eğer [GitLab Container Registry](https://about.gitlab.com/2016/05/23/gitlab-container-registry/) yerine 
örneğin [Docker Hub](https://hub.docker.com/) kullanacak olsaydım imajımı `docker.io/tunix/alperkan.at:1.0.5` olarak 
etiketlemem gerekecekti.

{{< figure src="docker_build_komutunun_anatomisi.png" caption="`docker build` komutu" >}}

docker build komutunun sonundaki nokta, imajın oluşturulacağı Dockerfile dosyasının yerini belirtir. Noktanın 
karşılığı [Bash](https://www.gnu.org/software/bash/) ve [ZSH](http://zsh.sourceforge.net/) gibi genel geçer kabuklarda 
(shell) “bulunduğum dizin” demektir.

Yine Dockerfile’dan bahsettiğim bölümde anlatacağım ama şimdiden belirtmekte fayda var. Olur da herhangi bir sebepten
dolayı parametrik imaj oluşturmanız gerekirse Dockerfile’da değişken tanımlamanız ve bu değişkenin değerini docker build
komutu içerisinde `--build-arg` parametreleriyle verebileceğinizi belirteyim. Örneğin tek sayfalık web uygulamalarında
(Single Page Application), uygulamanın bağlanacağı ortamı imajı oluştururken verip geliştirme ve test ortamına bağlanan
2 farklı imaj yaratabilirsiniz:

```
docker build -t example.com/web:1.0.0 \
    --build-arg SERVICE_URL=”http://dev.example.com” \
    --build-arg SERVICE_CONFIG=dev .
```

### docker push registry.gitlab.com/tunix/alperkan.at:1.0.5

Bilgisayarınızda oluşturduğunuz imajı uzaktaki depoya yüklemenizi sağlar. Eğer yükleyeceğiniz depo, giriş yapmanızı
gerektiriyorsa, bu komuttan önce:

```
docker login registry.gitlab.com
```

komutuyla giriş yapmanız gerekir. Bu komut, ev dizininizdeki `.docker/config.json` dosyasını yoksa oluşturacak ve giriş
yapmanızı gerektiren komutlarda kullanmanız gereken ayırt edici şifreyi içine kullandığınız depo adresiyle birlikte
yazacaktır.

Kullandığım örneklerde [GitLab Container Registry](https://about.gitlab.com/2016/05/23/gitlab-container-registry/) 
kullandığım için `registry.gitlab.com` adresini kullanıyorum. [Docker Hub](https://hub.docker.com/) ya da farklı bir 
depo ile çalışıyorsanız komutta değişiklik yapmalısınız.

`docker push` komutuyla bilgisayarınızdaki imaj için oluşturulan tüm katmanlar (baz alınan katmanlar depoda yüklüyse 
atlanarak) karşı taraftaki depoya yüklenecektir. Bu sayede imaja ihtiyaç duyan her yerde `docker pull` komutunu 
kullanarak imajı indirebilir ve bu imajdan container’lar oluşturabilirsiniz.

### docker rmi registry.gitlab.com/tunix/alperkan.at:1.0.5

İmaj silmek için bu komutu kullanabilirsiniz. Silinecek imajda sürüm numarası bulunuyorsa özel olarak belirtmelisiniz. 
`latest` olarak etiketlenmiş bir imajı silmek için herhangi bir sürüm belirtmeniz gerekmez.

Bu arada imajın ID’sini biliyorsanız (bknz: [docker images]({{< ref "#docker-images" >}})) doğrudan onu da 
kullanabilirsiniz:

```
docker rmi f24630ebe597
```

### docker run ...

Bilgisayarınıza indirdiğiniz bir imajdan bir adet container çalıştırmanızı sağlar. Çalıştıracağınız yazılıma göre, 
`docker run`’a vereceğiniz parametreler de değişiklik gösterecektir. Gelin, bir kaç örnek üstünden ilerleyelim.

```
docker run -it --rm ubuntu /bin/bash
```

Bu komutla, yukarıda [bahsettiğim]({{< ref "#docker-pull-tomcat8-jre8" >}}) gibi; eğer makinenizde Ubuntu’nun son 
sürümü yoksa indirilecek ve interaktif modda (`-it` sayesinde) Bash kabuğu açılıp sizden komut yazmanızı bekleyecektir. 
Komut satırından çıkış yaptığınızda container otomatik olarak silinecektir. (`--rm` sayesinde) Peki ne işe yarar? 
Aklıma gelen bazı örnekler:

* Makinenize kurmak istemediğiniz ya da kurması zorlu olan yazılımlarla hızlı denemeler/testler yapabilirsiniz. 
  _Örneğin hızlı bir ownCloud denemesi yapabilir ya da elinizdeki veri setini MySQL’e hızlıca aktarıp üstünde işlemler 
  yapıp çıktısını makinenize kaydedip container’ı uçurabilirsiniz._
* Başka bir işletim sisteminde çalışan bir yazılımı sanki yerel bir uygulamaymış gibi çalıştırabilirsiniz. 
  (macOS’de olmayan komut satırı araçlarını çalıştırmak vb.)
* Örneğin Tomcat çalıştırdığınızı varsayarsak (`docker run -it --rm tomcat /bin/bash`) imaj içinde neyin nasıl 
  yapıldığını/yerleştirildiğini inceleyebilir ve denemeler yapabilirsiniz.

```
docker run -d --name deneme --restart=always -p 3000:3000 alperkan.at:1.0.5
```

Sırasıyla parametrelerin üstünden geçersek;

* `-d`: İnteraktif modun aksine container’ın arkaplanda çalışmasını sağlar.
* `--name`: Çalışan container’a istediğiniz bir ismin atanmasını, böylece kolaylıkla ulaşabilmenizi sağlar.
* `--restart=always`: Docker Engine’in ya da container’ın herhangi bir şekilde kapanması sonrasında otomatik olarak 
  yeniden başlatılmasını sağlar. Diğer olası değerler: `no`, `on-failure:5`, `unless-stopped`
* `-p 3000:3000`: Ev sahibi makinedeki 3000. bağlantı noktasını, container içerisindeki 3000. porta yönlendirir. 
  _Alternatif olarak yalnızca -P yazmanız halinde container’ın açılması istenen tüm bağlantı noktaları, ev sahibi 
  üstündeki rastgele bağlantı noktalarına yönlendirilir._

> Pro Tip: Özellikle ölçeklenebilirliğin önemli olduğu durumlarda -P kullanmak daha doğrudur.

Bu komutla beraber kullanılabilecek diğer bazı önemli parametreler ise şöyle:

* `-e`: Container içerisinde çevresel değişkenler tanımlamak için kullanılır. Bu sayede çalışma esnasında uygulamanın 
  davranışını değiştirebilir, kritik parametreleri dışarıdan sağlayabilir ya da örneğin MySQL, Tomcat vb. 
  uygulamaların yetkili kullanıcı adını veya şifresini dışarıdan tanımlayabilirsiniz. Tanımlamak istediğiniz her 
  çevresel değişken için ayrı ayrı -e parametreleri tanımlayabilirsiniz. (ör: `-e MYSQL_ROOT_PASSWORD=test`) 
  **Container imajlarının değiştirilmezlik ilkesini göz önünde bulundurarak; çevresel değişkenlerin en önemli 
  özelliklerden biri olduğunu vurgulamalıyım.** Serinin ilerleyen bölümlerinde gerçek örneklerle nasıl 
  kullanabileceğimizi göreceğiz.
* `-v`: Container içerisindeki bir dizin ya da dosyayı, ev sahibi makine üstündeki bir dizine bağlamak için kullanılır. 
  Bağlamak istediğiniz her dizin ve dosya için ayrı ayrı -v parametresi tanımlayabilirsiniz. 
  (ör: `-v /home/alper/tomcat/webapps:/opt/tomcat/webapps`) **Unutulmaması gereken kısım; bu komutun kullanılması 
  durumunda container’ın dışa bağımlı hale geliyor olması ve imajın değiştirilmezlik ilkesine aslında ters olduğu.** 
* `-l`: Container’a çeşitli etiketler atamanızı sağlar. (ör: `-l TYPE=web -l PRIORITY=1`) Tanımlamak istediğiniz her 
  etiket için ayrı ayrı -l tanımı yapabilirsiniz. Özellikle ölçeklenebilirliğin önemli olduğu durumlarda Docker 
  Engine’in kendisine ve container’lara etiketler atamak oldukça büyük önem arz ediyor.

* `-u`: Çalışacak container’ın hangi kullanıcıyla çalışacağını belirler. Öntanımlı olarak her container root 
  yetkileriyle çalışıyor ve bu durum aslına bakarsanız güvenlik açıklarına sebebiyet verebiliyor. Bu nedenle 
  container’ları mümkünse yetkisiz kullanıcılarla çalıştırmalısınız. _Serinin ilerleyen bölümlerinde bahsedeceğim 
  Dockerfile’lar sayesinde bu adımı çalıştırma esnasında parametre vermeksizin geçiştirebilirsiniz._

docker run komutuna bunların dışında verebileceğiniz daha pek çok parametre bulunuyor. Örneğin; çalıştıracağınız 
container’a ayrılacak CPU ve belleği belirtebileceğiniz gibi disk okuma/yazma hızını ya da hangi ağa erişeceğini 
ayarlayabilirsiniz. Tüm bu detayları bu [yazının başında belirttiğim]({{< ref "#docker-cmd-" >}}) gibi; 
`docker run --help` komutuyla öğrenebilirsiniz.

### docker logs --tail 20 -f alperkan.at

Docker container’ları genellikle yalnızca tek bir süreç çalıştıracak ve temel çıktıya (stdout) bir şeyler basacak 
şekilde tasarlanırlar. Temel çıktıya basılan işlem kayıtlarına bu komutla ulaşabilirsiniz. Örneğin bir nginx 
container’ı başlatırsanız; `access.log`’u bu komutla takip edebilirsiniz.

`--tail`: En son N satırdan itibaren çıktıyı ekrana getirir.
`-f`: Komut iptal edilene kadar (Ctrl-C) çıktıyı takip etmeye devam eder.

### docker exec -it alperkan.at ls -l /srv

Çalışan (hali hazırda çalışmayan bir container’da bu komutu kullanamazsınız) bir container içinde komutlar 
çalıştırmanızı sağlayan bu komutu yalnızca container imajını hazırlarken ya da container’daki sorunları anlamaya 
çalışırken kullanmalısınız.

Bu komutu genellikle docker logs ile takip edemediğiniz farklı log dosyalarını takip etmek ya da kabuk başlatıp daha 
ileri seviye işler yapmak için kullanabilirsiniz. İhtiyacınız olabilecek örnek komutlar:

```
docker exec -it nginx-proxy tail -F /var/log/nginx/error.log
docker exec -it alperkan.at /bin/bash
```

### docker cp ~/Desktop/data.json alperkan.at:/srv/data/me.json

Bilgisayarınızdaki bir dosyayı/dizini container’a ya da container’daki bir dosyayı/dizini bilgisayarınıza 
kopyalamanızı sağlar.

`-L`: Olası sembolik dosya ve dizinlerin de doğru şekilde kopyalanmasını garantiler.

### docker stop alperkan.at

Çalışan bir container’ı durdurmanızı sağlar. Bazen bir container’a daha sonra tekrar ihtiyacınız olabilir. Bu tip 
durumlarda durdurup sonra tekrar [docker start]({{< ref "#docker-start-alperkanat" >}}) komutuyla ayağa 
kaldırabilirsiniz.

`-t`: Container kapanmakta gecikirse bu komutu vererek N saniye geçtikten sonra öldürülmesini sağlayabilirsiniz.

### docker start alperkan.at

[docker stop]({{< ref "#docker-stop-alperkanat" >}}) komutuyla durdurduğunuz bir container’ı yeniden başlatmanızı 
sağlar.

`-a`: Container’ı başlattıktan sonra temel çıktısının bulunduğunuz kabuk oturumuna bağlanmasını sağlar.

### docker inspect alperkan.at

Çalışan container’la ilgili çok detaylı bilgilere ulaşmanızı sağlar. Bu komutla örneğin; container’da çalışan çevresel 
değişkenlere, tanımlanmış bağlantı noktalarına, bağlanmış disk alanlarına ve daha pek çok bilgiye ulaşabilirsiniz.

> Pro Tip: Bu komuta çıktısı içerisinde rahatça dolaşabilmek ve arama yapabilmek için `|less` eklemek isteyebilirsiniz.

---

Serinin bu bölümünün de sonuna geldik. Bir sonraki bölüm olan Docker Engine Bölüm 2'de kalıcı veri depolama, çevresel 
değişkenler, bağlantı noktaları, Dockerfile, kendi imajınızı hazırlamak, Docker Hub & Registry ve son olarak kendi 
özel Docker Hub’ınıza nasıl sahip olabileceğinizden bahsedeceğim.

Gidişâta göre bu planda zaman zaman değişiklikler yapacak olsam da serinin tüm bölümlerinin planına 
[şuradan](https://www.evernote.com/l/AB7CctYtJkpMUJsae1_3FgzIXgMY5MvFQhU) ulaşabilirsiniz.

Katkılarından dolayı Şamil Can’a teşekkürler! Serinin bir sonraki bölümünde görüşmek üzere! ✌️
