---
title: System76 Lemur Pro Hakkında
date: 2021-05-08T01:23:00+03:00
slug: system76-lemur-pro
draft: true
cover:
    image: system76.png
tags:
    - bilgisayar
    - system76
    - lemur pro
    - linux
    - açık kaynak
---

Uzun zamandır çalıştığım şirketlerin verdiği, çoğunlukla da Mac bilgisayarlar kullanıyorum. Açıkcası en son ne zaman 
kendi bilgisayarıma sahiptim, ne zaman ve kaça sattım, hatırlayamıyorum bile.

Bir dönem kendi masaüstü bilgisayarlarımızı topladığımız, bilgisayar fiyatlarının ulaşılabilir olduğu bir dönem vardı. 
Mac'ler belki yine pahalıydı ama bilgisayar fiyatları hiç bir zaman **erişilmez** değildi. Geldiğimiz noktadan ciddi 
anlamda endişe duyuyorum. Özellikle içinden geçtiğimiz pandemi sürecinde, eğitimin bile internetten yapıldığı bir 
dönemde öğrencilerin, yeni mezunların iyi bir bilgisayara erişimi oldukça zorlaşmış durumda. Üstelik sadece maddi bir 
durumdan söz etmiyorum; fiyat artışları nedeniyle üreticilerin üst modelleri getirmediği ya da sınırlı getirdiği bir 
dönemi yaşıyoruz. Yüksek performans verebilecek cihazları piyasada bulmak bir hayli zor.

{{< figure src="ipad.jpg" caption="2012'de iPad ile SSH üzerinden kod yazmaya çalışırken.." >}}

2020 başlarına kadar şirketin sağladığı 8 GB belleğe sahip bir Macbook Pro (2014) kullanıyordum. 
[dataroid](https://www.dataroid.com/)'deki günlük çalışma tempom içerisinde birden çok container'ı ayağa kaldırmam, kod
değişikliklerini test etmem vs gerektiği için bilgisayar yetmiyor ve bu nedenle de Kafka, Elasticsearch vb. bir çok
bağımlılığı sandbox ortamımızdaki sunuculardan kullanmam gerekiyordu.

Şirket 2020 içerisinde, belli ihtiyaçları olan takımlar haricindeki herkesin bilgisayarlarını 
[Dell Precision 5530](https://www.dell.com/en-us/work/shop/dell-laptops-and-notebooks/precision-5530-mobile-workstation/spd/precision-15-5530-laptop) 
ile yenileme kararı aldı. i7 serisi Intel CPU, çift GPU (Intel + NVIDIA) ve 64 GB belleğe sahip bu makine, yaşadığım
sıkıntıların çoğunu giderdi. Elbette böyle bir geçiş, işletim sistemiyle ilgili bir seçim yapmam anlamına da geliyordu.
Neyse ki bu modelin tamamen Linux uyumlu bir model olması ve IT'nin onay vermesiyle [Ubuntu](https://ubuntu.com/) 
kullanabiliyorum. 18.04 LTS ile başladım, 20.10 ile devam ediyorum. 🤙 Masaüstü Linux deneyiminin, 2010'dan bu yana 
geldiği nokta beni son derece memnun etti. Performans, kararlılık, donanım desteği, uygulama çeşitliliği anlamında ciddi
yol kat edilmiş ve bununla da yetinilmemiş; Steam vb. platformlar üzerinden hem doğrudan Linux desteği olan oyunları,
hem de [azımsanamayacak kadar fazla Windows oyununu](https://www.protondb.com/) sorunsuzca (ve hatta yer yer Windows'dan 
daha hızlı olacak kadar) oynayabiliyorsunuz.

Vaktiniz olursa reddit'teki [r/unixporn](https://www.reddit.com/r/unixporn/) bölümüne göz atmanızı öneririm. [GNOME
masaüstünün](https://www.gnome.org/) Big Sur'e ne kadar benzetilebileceğine dair bir video'yu da şuraya bırakayım:

{{< youtube jT1RnyGJRMU >}}

2017'den itibaren döviz kurlarındaki artış nedeniyle tekrar kendime ait bir bilgisayarım olmasının iyi olabileceğini
düşünmeye başlayıp araştırmalara başladım. Listemde şu marka/modeller vardı:

* [Dell XPS 9310](https://www.dell.com/tr/sletmeler/p/xps-13-9310-laptop/pd)
* [System76 Lemur Pro](https://system76.com/laptops/lemur)
* [Starlabs Starbook Mk V](https://starlabs.systems/pages/starbook)
* [TUXEDO InfinityBook S 14 - Gen 6](https://www.tuxedocomputers.com/en/Linux-Hardware/Linux-Notebooks/10-14-inch/TUXEDO-InfinityBook-S-14-v6.tuxedo)
* [Monster Huma H4 V4.1.2](https://www.monsternotebook.com.tr/huma/monster-huma-h4-v4-1-2/)
* [Slimbook Pro X](https://slimbook.es/en/pro-x-en)

### Monster

Tüm bu markalar arasında en rahat erişimim olan Monster olmasına rağmen; Monster'ın herhangi bir Linux uyumluluk
garantisi vermemesi nedeniyle elim gitmedi. Bu arada İzmir'deki dükkanlarına gidip cihazı inceleme fırsatı buldum; 
[Clevo](http://clevo.tw/) şasi kullanmalarına rağmen oldukça şık ve hafif bir bilgisayar olduğunu söylemeliyim.

### Dell XPS 13

Taşınabilirlik ve incelik kategorisinde senelerdir birinciliği kimselere kaptırmayan Dell XPS 13, en uzun süredir
radarımda olan modeldi. Epeyce bir süredir, Canonical ile birlikte
[Project Sputnik](https://bartongeorge.io/2020/01/01/introducing-the-2020-xps-13-developer-edition-this-one-goes-to-32/)
adında heyecan verici bir proje yürütüyorlar. Bu nedenden ötürü bir Developer Edition almak istiyordum ancak bu model,
Türkiye'de satılmıyor. Hatta Dell XPS 13 modelinin güncel serileri oldukça uzun bir süre ülkemizde satışta değildi.
Bugüne kadar AVM'lerdeki mağazalarda hiç bir zaman bir Dell'e denk gel(e)medim. Dell'in, Türkiye'de daha çok kurumsal
tarafa odaklandığını ve gerisini umursamadığını [düşünüyorum](https://twitter.com/tunix/status/1351876496726614021).

{{< tweet 1351876496726614021 >}}

2020 ve 2021 yılları içerisinde Dell, Lenovo gibi bilgisayar üreticileri, çeşitli Linux dağıtımcılarıyla anlaşmalar
yaparak Fedora ve Ubuntu yüklü olan bilgisayarların artık çevrimiçi mağazalardan, tıpkı Windows yüklü bilgisayarlar gibi
rahatça satın alınabileceğine dair çokça duyuru yaptılar. Ancak bu durum maalesef gerçekleşmedi.

Dell'in ABD sayfalarında Ubuntu olan modellere bazen rahat, bazense oldukça zor ulaşılabiliyor. İşin daha da can sıkıcı
tarafı; farklı ülkelerde farklı yapılandırmalara yer verilmesi ve sık sık değişmesi. (bir sonraki ziyaretinizde
bulamayabiliyorsunuz) Developer Edition'a ise ABD dışında ulaşmak neredeyse imkansız.

### Starlabs

Dell dışında saydığım tüm modeller mutlaka [Clevo](http://clevo.tw/)'nun bir şasisini farklı yapılandırmalarla 
sunuyorlar. Starlabs ise bu noktada [farklı bir yol](https://starlabs.systems/pages/about-us) izliyor. İngiltere'de
bulunan şirket Türkiye'ye gönderim ve diğerlerine göre daha ulaşılabilir fiyatlarda üretim yapıyorlar.

Bu ay içerisinde lansmanı yapılan [Starbook Mk V](https://starlabs.systems/pages/starbook) öncesindeki modeller teknik 
anlamda yetersiz kalıyordu. Bu modelin System76 Lemur Pro'ya iyi bir alternatif olduğunu düşünüyorum. Lemur Pro almamış
olsaydım muhtemelen bu bilgisayarı alacaktım.

### TUXEDO

Almanya'da bulunan TUXEDO, piyasanın eski oyuncularından. Farklı pek çok modelleri var ancak hepsinde 
[Clevo](http://clevo.tw/)'nun şaselerine yer veriyorlar. Bunların bir çoğu oldukça hantal göründüğünden bana hitap
etmiyordu.
[Yukarıda bahsettiğim model](https://www.tuxedocomputers.com/en/Linux-Hardware/Linux-Notebooks/10-14-inch/TUXEDO-InfinityBook-S-14-v6.tuxedo)
ise Lemur Pro ile aynı kasayı kullanıyor. Ayrıca yine beğendiğim, farklı şaselere yer verdikleri; hatta AMD Ryzen 
platformunu kullandıkları modelleri de mevcut.

TUXEDO'nun bence bir kaç önemli artısı da var:

* Bir çok modeli Türkçe klavye düzeniyle yollayabiliyorlar
* Benim beğendiğim model de dahil olmak üzere; bir çok modele LTE modülü eklenebiliyor.

System76 ve Starlabs'dan sonra bir gözüm hep TUXEDO'da idi. Intel Iris XE platformuna sahip modelleri biraz geç
açıkladılar ve bence System76 ve Starlabs'a göre en büyük eksiklikleri, coreboot'un yokluğu ve rakiplerine göre fazla 
bir değer üretmiyor oluşu diyebilirim.

### Slimbook

TODO

### System76

TODO
