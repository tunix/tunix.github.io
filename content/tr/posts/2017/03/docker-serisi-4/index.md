---
title: "Docker Serisi #4 -- Docker Compose"
date: 2017-03-20
slug: docker-serisi-4
tags:
    - yazılım
    - docker
    - docker serisi
    - container
    - sanallaştırma
    - linux
    - devops
---

4. bölüme hoşgeldiniz! 🤘🏻 Serinin önceki bölümlerine ulaşmak için aşağıdaki bağlantıları kullanabilirsiniz:

* [Docker Serisi #1]({{< ref "docker-serisi-1" >}})
* [Docker Serisi #2 — Docker Engine Bölüm 1]({{< ref "docker-serisi-2" >}})
* [Docker Serisi #3 — Docker Engine Bölüm 2]({{< ref "docker-serisi-3" >}})

Daha çok geliştirme üstüne duracak olsam da, [Docker Compose](https://docs.docker.com/compose/)’u test ortamı ya da 
farklı ihtiyaçlar için de kullanabilirsiniz. Özellikle tek bir makine üstünde birden fazla container ile çalışmayı 
düşünüyorsanız [Docker Compose](https://docs.docker.com/compose/) mutlaka incelemeniz gereken bir araç!

**Güncelleme:** Docker 1.13 ile birlikte Docker Compose ile tanımladığınız bir projeyi 
[Swarm](https://docs.docker.com/swarm/) ile birden çok makineye dağıtabiliyorsunuz! 🎉 Seride buna da yer vermek farz 
oldu tabii ki!

Özetle; uygulamanızı, projenize yerleştireceğiniz `docker-compose.yml` adında bir dosya aracılığıyla servisler olarak 
tanımlamanıza olanak tanır ve çalıştırdığınızda ilgili container’ları, disk bölümlerini, ağları vb. her şeyi oluşturup 
işiniz bittiğinde de tamamen kaldırır. O zaman kurulum ile hemen işe koyulalım! 😊

---

### Kurulum

Kurulum için [şuradaki](https://docs.docker.com/compose/install/) dökümanı takip edebilirsiniz. macOS ve brew 
kullanıyorsanız;

```
brew install docker-compose
```

komutuyla kurulumu tamamlayabilirsiniz. Eğer makinenizde Python (pip >= 6.0) kullanıyorsanız;

```
pip install docker-compose
```

komutunu kullanabilirsiniz. Alternatif olarak aşağıdaki komutlar ile de kurulumu gerçekleştirebilirsiniz:

```
# curl -L https://github.com/docker/compose/releases/download/1.9.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
# chmod +x /usr/local/bin/docker-compose
```

Kurulumu başarıyla tamamladıysanız aşağıdaki gibi sürüm numarası çıktısını görebilmelisiniz:

```
$ docker-compose --version
docker-compose version 1.11.2, build dfed245
```

---

> Yazının bundan sonraki bölümünde [şu adreste](https://github.com/tunix/docker-compose-demo) bulabileceğiniz örnek 
> projeyi kullanarak devam edeceğim. Dilerseniz indirip benimle beraber adımları tekrarlayabilir ve denemeler 
> yapabilirsiniz.

---

### docker-compose.yml

Normalde projenizin ana dizinine tek bir `docker-compose.yml` dosyası koymak yeterli olmakla beraber, bir dizin birden 
fazla alt projeye ev sahipliği yapıyorsa bu durumda alt dizinlere de birer tane `docker-compose.yml` dosyası 
yerleştirebilirsiniz. Bu durumda `-f` parametresiyle dosya yolunu belirtmelisiniz.

Dosyanın biçimi, kullanılabilecek anahtar kelimeler vb. için [şuradaki](https://docs.docker.com/compose/compose-file/) 
belgeyi inceleyebilirsiniz. Klasik bir `docker-compose.yml` dosyası yaklaşık olarak aşağıdaki gibidir:

{{< gist tunix 15a0a926b3a16c6acb8ffbd75351fbf0 >}}

YML dosyası yazarken, bu dosya biçimine has yazım kurallarına dikkat etmelisiniz. Kapsamı iyice genişletmemek adına 
yazım kurallarına girmeyeceğim ancak özellikle girintilemeye özen göstermelisiniz.

İlk satır dosyanın biçimlendirmesinde kullanılan tanımlamaların (spec) sürümünü belirtiyor ve ilk satırda olma 
zorunluluğu var. Docker 1.13 öncesinde sürüm numarası olarak yalnızca "2" kullanılırken, artık "3" de kullanılabiliyor. 
Sürüm numarası, dosyanın biçiminde yapılabilecek değişikliklerden etkilenilmemesi için düşünülmüş bir özellik. Yani 
eski bir projenizde sürüm olarak "2" kullanıyorsanız, artık desteklenmeyen bir Docker sürümü kullanmıyorsanız, projeniz 
olduğu gibi çalışacaktır. Yeni bir projeye başladığınızda sürümü "3" olarak belirtmeli ve yazım kurallarını da bu 
sürüme uyacak şekilde uygulamalısınız.

Dosyada tanımlamanız gereken ikinci kısım: servisler. Her bir servisi, ayrı birer container gibi düşünebilirsiniz. 
"services" kelimesinin altında, 1 girintileme ile ayırdığınız her şey bir servistir ve çalışacak container'ın adı 
burada yazdığınız kelimeyle anılacaktır.

İlk servisimiz adından da anlaşılabileceği gibi API hizmeti sunan bir container’dan ibaret. Aynı servisten birden çok 
kez başlatma ihtimaline karşılık Compose, yazdığınız ismi, YML dosyasının bulunduğu dizin adı ve bir rakamla 
harmanlayıp container adı (ör: `dockercomposedemo_api_1`) yaratır. Yalnızca tek bir container başlatacağınızdan 
eminseniz servis tanımlarına

```
container_name: demo-api
```

yazarak bu isimle açılmasını [sağlayabilirsiniz](https://docs.docker.com/compose/compose-file/#containername). Bu 
durumda birden fazla container başlatmaya çalışırsanız hata alırsınız.

Servisimizin adının altında bir kez daha girintileme ile yazdığımız her şey servisi tanımlayan ayarlar olarak 
algılanır. Şimdi gelin; sırasıyla yazdıklarımızı anlamaya çalışalım:

#### build: .

Kısaca imajı oluşturulacak Dockerfile dosyasının yerini (build context) belirtmek için kullanılır. Bizim projemizde 
Dockerfile, YML dosyasıyla aynı dizinde bulunduğu için "." (nokta) ile bu dizini işaret ediyoruz. Dilerseniz farklı bir 
dizindeki Dockerfile’ı işaret edebilir, Dockerfile yerine farklı bir isim kullanıyorsanız ya da imajı yaratabilmek için 
ek parametrelere ihtiyaç duyuyorsanız bunları da bu kısımda belirtebilirsiniz. Detaylar için 
[tık tık](https://docs.docker.com/compose/compose-file/#build).

[Swarm](https://docs.docker.com/swarm/) modunda bu parametre gözardı edilmekte ve bir alttaki image parametresi 
kullanılmaktadır.

#### image: tunix/docker-compose-demo

İmajın derlenmesi sonucunda çıkacak Docker imajının adını bu komutla belirtiyoruz. Hiç bir şey yazmazsanız yine 
bulunduğunuz dizin ve verdiğiniz servis adını harmanlayarak bir isim (ör: `dockercomposedemo_api`) oluşturulacaktır.

#### ports

YML dosya biçiminde "-" ile başlayan kısımlar üstündeki satırı dizi (array) olarak tanımlar. Yani birden fazla "-" ile 
başlayan satır yazarak, ports dizisine birden çok erişim noktası (port) ekleyebilirsiniz. Bizim örneğimiz için 
konuşursak; ev sahibi (host) makinedeki 8080. erişim noktasını, container içerisindeki 8080 numaralı erişim noktasına 
bağlıyoruz.

Bir erişim noktası, ev sahibi makinede yalnızca 1 kez kullanılabilir. Bu nedenle herhangi bir servisi, aynı ev sahibi 
makinede birden fazla kez çalıştırmayı düşünüyorsanız bu kısımda yalnızca container’a ait olan erişim noktasını 
belirtmelisiniz. Bu durumda, Compose container’ınıza ev sahibi makineden rastgele bir erişim noktası atar.

#### links

Altındaki tanımdan anlayacağınız üzere, "links" de bir dizi olup birden çok tanımlama 
[kabul edebilir](https://docs.docker.com/compose/compose-file/#links). Bir container, diğerine erişeceğinde bunun en 
kolay yolu bu container’ları birbirine bağlamaktır. Yazım şekline bakarsak ":" karakterinin solundaki servis adı, 
sağındakiyse takma addır. Container içinden veritabanına ulaşacağımızda bu takma adı kullanıyor olacağız. Bu, bizi 
gereksiz yere IP tanımlamaktan kurtacaktır. Proje içerisindeki 
[application.yml](https://github.com/tunix/docker-compose-demo/blob/master/src/main/resources/application.yml) 
dosyasına bakarsanız MySQL için kullandığımız bağlantı cümlesinde (connection string) takma ad olan `demodb` kelimesini 
kullandığımızı görebilirsiniz. Takma ad kullanmanın avantajı; servis adı değişse bile takma adın değişmemesidir. 
Böylece kodumuzda değişiklik yapmak zorunda kalmıyoruz.

[Swarm](https://docs.docker.com/swarm/) modunda bu parametre gözardı edilmektedir.

#### command

Container başlatılırken çalıştırılacak komutun ne olacağını belirler.

Serinin önceki yazılarında [bahsettiğim]({{< ref "docker-serisi-3" >}}) gibi, bu tanım aslında Dockerfile içinde de 
yapılabiliyor. Burada tekrar yapma sebebim, Compose’un yapısından kaynaklanıyor. Tahmin edebileceğiniz gibi MySQL 
başlayana kadar DB container’ındaki 3306 erişim noktası açık değil. Bu durumda uygulamam ayağa kalkarken bağlanamayıp 
hata verecektir. Bunu engellemek için erişim noktasını sürekli yoklayıp açılınca uygulamayı başlatan 
[wait-for-it.sh](https://github.com/tunix/docker-compose-demo/blob/master/wait-for-it.sh) adında bir betik (script) 
kullanıyorum.

#### environment

İmaj içerisinde tanımlı olan çevresel değişkenleri, yeni bir container başlatırken bu şekilde değiştirebiliyor, 
tanımlayabiliyorsunuz. DB servisi için belirttiğim değişkenler, container ayağa kalktığında çalışan betiğin, benim 
istediğim isimle bir veritabanı yaratmasını ve yine istediğim kullanıcı adı ve şifreyle çalışmasını sağlıyor.

Yalnızca 20 satırlık bu 
[docker-compose.yml](https://github.com/tunix/docker-compose-demo/blob/master/docker-compose.yml) dosyasıyla API 
container’ının imajının yaratılmasını, ondan da bir container ayağa kaldırılmasını ve MySQL imajından DB adında bir 
container yaratılmasını sağlayabiliyorsunuz. Tabii ki yapabilecekleriniz bunlarla sınırlı değil. 
[Ekleyebileceğiniz diğer parametrelerle](https://docs.docker.com/compose/compose-file/) container kayıtlarının nereye 
yazılacağını, container yükleme (deployment) stratejilerinin belirlenmesini, bağlanacak dosya/dizinleri ve daha pek çok 
ayarı yapabilirsiniz.

Serinin ilerleyen bölümlerinde farklı proje örneklerinde Compose’u nasıl kullanabileceğinizi işliyor olacağım.

### Compose ile Çalışmak

YML dosyasını inceledikten sonra sıra geldi container’larımızı çalıştırmaya! Bunun için YML dosyasının bulunduğu dizine 
gidin ve şu komutu çalıştırın:

```
docker-compose up -d
```

Bu komut container’ları yaratacak, servisleri başlatacak ve sonrasında da çıkış yapacak. `-d` ya da uzun haliyle 
`--daemon` parametresi, komutun arka planda (daemon) çalışmasını sağlar. Çalıştıklarını da teyid edelim:

{{< figure src="docker_compose_ps_ciktisi.png" caption="docker-compose ps" >}}

Dikkat ederseniz API servisimizin erişim noktası (8080) dışarıya açık ve erişilebilir durumdayken, DB servisimiz için 
aynı durum geçerli değil. Bunun sebebi, Compose’un YML dosyasında bu erişim noktasını açmamış olmamızdan kaynaklanıyor. 
Eğer veritabanınıza dışarıdan erişebilmek isterseniz dosyayı değiştirip erişim noktasını açmalı ve servisleri yeniden 
ayağa kaldırmalısınız.

Erişim noktası açık olmamasına rağmen, API servisi veritabanına bağlanabiliyor çünkü Compose container’ların kendi 
arasında iletişimi için özel bir ağ yarattı ve yukarıda bahsettiğim gibi, DB servisinin IP adresi `demodb` adıyla API 
servisine ait container tarafından ulaşılabilir durumda.

Compose’un yarattığı bu ağ, servislerin izolasyonu açısından oldukça önemli. Serinin ilerleyen bölümlerinde göreceğimiz 
üzere, YML dosyasında yapacağınız bir takım değişikliklerle birden çok Compose YML dosyasıyla yönettiğiniz servisleri 
aynı ağa bağlamanız mümkün.

Artık servisimiz ayakta olduğuna göre istek atıp üstünde çalışabiliriz:

{{< figure src="servis_istek_ciktisi.png" caption="Spring Boot ile yazılmış HATEOAS REST API, DB’den aldığı sonuçları dönüyor." >}}

```
docker-compose down
```

komutunu vererek tüm servislerin kapatılmasını ve bunlara bağlı olarak yaratılmış ağ ile tüm container’ların 
silinmesini sağlayabilirsiniz:

{{< figure src="docker_compose_down_ciktisi.png" caption="docker-compose down komut çıktısı" >}}

Kolaylık olması açısından oluşturulan imajlar silinmiyor. Bu sayede bir sonraki sefer `docker-compose up -`d komutunu 
verdiğinizde servisleriniz çok daha hızlı ayağa kaldırılır. Eğer imajları da silmek isterseniz;

```
docker-compose down --rmi all
```

komutunu verebilirsiniz.

### İpucu #1

Diyelim ki; Ubuntu bazlı bir Docker imajınız var ve her ayağa kalkışında aşağıdaki komutları çalıştırıyor:

```
apt-get update
apt-get upgrade
```

Daha farklı bir senaryo olarak, container’ınız ayağa kalkarken bir betik çalıştırarak git deponuzdaki kodun son halini 
de alıyor olabilir örneğin. Bu gibi senaryolarda down komutuyla her şeyi kaldırmak yerine;

```
docker-compose stop
```

komutuyla ağı ve tüm servisleri geçici olarak pasifize edebilir, ihtiyacınız olduğunda da;

```
docker-compose start
```

komutuyla yeniden başlatabilirsiniz.

### İpucu #2

Klasik Docker komutlarından farklı olarak Compose da `logs`, `restart`, `rm`, `exec` vb. pek çok komutu sağlıyor. 
Bunların amaçlarını ve kullanım şekillerini örneğin;

```
docker-compose logs --help
```

komutuyla görüntüleyebilirsiniz.

### İpucu #3

Yukarıdaki örnekte bir API servisi, bir de DB servisi çalıştırmıştık. Aşağıdaki komutla istediğiniz servisten, istediğiniz adette başlatabilirsiniz:

```
docker-compose scale api=2 db=1
```

Tabii uygulamanızın da buna hazır olması kaydıyla! 😉

{{< figure src="docker_compose_scale_ciktisi.png" >}}

---

Bu bölümünün de sonuna geldik. Bir sonraki bölümde [Docker Machine](https://docs.docker.com/machine/) ve 
[Docker Swarm](https://docs.docker.com/swarm/)’dan bahsedeceğim.

Gidişâta göre bu planda zaman zaman değişiklikler yapacak olsam da serinin tüm bölümlerinin planına 
[şuradan](https://www.evernote.com/l/AB7CctYtJkpMUJsae1_3FgzIXgMY5MvFQhU) ulaşabilirsiniz.
