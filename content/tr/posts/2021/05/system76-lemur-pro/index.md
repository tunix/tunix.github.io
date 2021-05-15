---
title: System76 Lemur Pro Hakkında
date: 2021-05-16T01:30:00+03:00
slug: system76-lemur-pro
cover:
    image: system76.png
tags:
    - bilgisayar
    - system76
    - lemur pro
    - linux
    - açık kaynak
---

Uzun zamandır çalıştığım şirketlerin verdiği, çoğunlukla da Mac bilgisayarlar kullanıyordum. Açıkcası en son ne zaman 
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
kullanabiliyorum. 18.04 LTS ile başladım, 20.10 ile devam ediyorum. 🤙

Masaüstü Linux deneyiminin, 2010'dan bu yana geldiği nokta beni son derece memnun etti. Performans, kararlılık, donanım 
desteği, uygulama çeşitliliği anlamında ciddi yol kat edilmiş ve bununla da yetinilmemiş; Steam vb. platformlar 
üzerinden hem doğrudan Linux desteği olan oyunları, hem de 
[azımsanamayacak kadar fazla Windows oyununu](https://www.protondb.com/) sorunsuzca (ve hatta yer yer Windows'dan 
daha hızlı olacak kadar) oynayabiliyorsunuz.

Vaktiniz olursa reddit'teki [r/unixporn](https://www.reddit.com/r/unixporn/) bölümüne göz atmanızı öneririm. [GNOME
masaüstünün](https://www.gnome.org/) Big Sur'e ne kadar benzetilebileceğine dair bir video'yu da şuraya bırakayım:

{{< youtube jT1RnyGJRMU >}}

2017'den itibaren döviz kurlarındaki artış nedeniyle tekrar kendime ait bir bilgisayarım olmasının iyi olabileceğini
düşünmeye başlayıp araştırmalara başladım. Listemde şu modeller vardı:

* [Dell XPS 9310](https://www.dell.com/tr/sletmeler/p/xps-13-9310-laptop/pd)
* [System76 Lemur Pro](https://system76.com/laptops/lemur)
* [Starlabs Starbook Mk V](https://starlabs.systems/pages/starbook)
* [TUXEDO InfinityBook S 14 - Gen 6](https://www.tuxedocomputers.com/en/Linux-Hardware/Linux-Notebooks/10-14-inch/TUXEDO-InfinityBook-S-14-v6.tuxedo)
* [Monster Huma H4 V4.1.2](https://www.monsternotebook.com.tr/huma/monster-huma-h4-v4-1-2/)
* [Slimbook Pro X](https://slimbook.es/en/pro-x-en)

Modellerle ilgili düşüncelerimi yazmadan önce kriterlerimi de belirtmemde fayda var:

* Uzun pil ömrü (tercihen tüm günü geçirebilmeliyim)
* Hafiflik (< 1.5 kg)
* Birinci sınıf Linux desteği
* 13-14 inch boyutlarında olması
* Kaliteli bir touchpad ve klavyesinin olması
* (Tercihen) AMD platformunda olması; olamıyorsa Intel Xe platformunda olması
* (Tercihen) Tamamen ya da maksimum derecede açık kaynak olması (ör: coreboot desteği)

Şimdi gelelim modellere...

### Monster Huma H4

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
bulamayabiliyorsunuz) Developer Edition'a ise ABD dışında ulaşmak neredeyse imkânsız.

### Starlabs Starbook Mk V

Dell dışında saydığım tüm modeller mutlaka [Clevo](http://clevo.tw/)'nun bir şasisini farklı yapılandırmalarla 
sunuyorlar. Starlabs ise bu noktada [farklı bir yol](https://starlabs.systems/pages/about-us) izliyor. İngiltere'de
bulunan şirket Türkiye'ye gönderim ve diğerlerine göre daha ulaşılabilir fiyatlarda üretim yapıyorlar.

Bu ay içerisinde lansmanı yapılan [Starbook Mk V](https://starlabs.systems/pages/starbook) öncesindeki modeller teknik 
anlamda yetersiz kalıyordu. Bu modelin ise System76 Lemur Pro'ya iyi bir alternatif olduğunu düşünüyorum. Lemur Pro 
almamış olsaydım muhtemelen bu bilgisayarı alırdım.

### TUXEDO InfinityBook S 14

Almanya'da bulunan [TUXEDO](https://www.tuxedocomputers.com/en), piyasanın eski oyuncularından. Farklı pek çok 
modelleri var ancak hepsinde [Clevo](http://clevo.tw/)'nun şaselerine yer veriyorlar. Daha önce, bunların bir çoğu 
oldukça hantal göründüğünden bana hitap etmiyordu.
[Yukarıda bahsettiğim model](https://www.tuxedocomputers.com/en/Linux-Hardware/Linux-Notebooks/10-14-inch/TUXEDO-InfinityBook-S-14-v6.tuxedo)
ise Lemur Pro ile aynı kasayı kullanıyor. Ayrıca yine beğendiğim, farklı şaselere yer verdikleri; hatta AMD Ryzen 
platformunu kullandıkları modelleri de mevcut.

TUXEDO'nun bence bir kaç önemli artısı da var:

* Bir çok modeli Türkçe klavye düzeniyle yollayabiliyorlar.
* Benim beğendiğim model de dahil olmak üzere; bir çok modele LTE modülü eklenebiliyor.
* Türkiye dahil pek çok ülkeye gönderim yapabiliyorlar.

System76 ve Starlabs'dan sonra bir gözüm hep TUXEDO'da idi. Intel Iris XE platformuna sahip modelleri sanırım biraz geç
açıkladılar ve bence System76 ve Starlabs'a göre en büyük eksiklikleri, coreboot'un yokluğu ve rakiplerine göre fazla 
bir değer üretmiyor oluşu diyebilirim.

### Slimbook Pro X

İspanyol [Slimbook](https://slimbook.es/en/) yine bir süredir izlediğim, Monster ile aynı (Clevo) kasaları kullanan 
bir üretici. AMD Ryzen serisi CPU ve GPU ile ürettikleri KDE Slimbook gibi modeller oldukça ses getirmiş olsa da benim
düşündüğüm model [Pro X](https://slimbook.es/en/pro-x-en) idi. Hem gönlümde yatan aslanın System76 olmasından, hem de
benim bu modele baktığım dönemde bu bilgisayarın çok yeni olması nedeniyle bu modeli de gözardı etmek durumunda kaldım.

---

System76'a geçmeden önce değinmem gereken son 1-2 konu daha var. Bilgisayarları incelerken kriterlerime uyan
üreticilerin yalnızca 1 modelini baz alarak araştırmamı yapmaya çalıştım. Her model için Youtube, çeşitli internet
siteleri ve reddit'teki incelemeleri ve altlarına yazılan yorumları detaylıca taradım. Olumsuz yanları not aldım ve
aradan geçen zamanda üreticilerin bu sorunları çözüp çözmediklerini anlamaya çalıştım.

Örneğin; Dell XPS 13 gibi bir bilgisayar için internette sıkılacağınız derecede fazla sayıda inceleme mevcut. Ancak bu
incelemelerin neredeyse tamamı Windows ile yapılmış ve Developer Edition incelemesi ya yok ya da oldukça eski zamanlara
ait. Benzer şekilde; yukarıda listelediğim bilgisayar modellerine ait incelemeler de oldukça sınırlı ya da eski. Hele
ki; birbiriyle karşılaştıranlar ise çok çok daha nadir.

Lemur Pro özelinde benim en beğendiğim ve faydalı olduğunu düşündüğüm inceleme 
[Steve'e](https://www.youtube.com/user/SteveM0732/videos) ait.

Faydalandığım diğer kaynaklar şöyle:

* https://www.reddit.com/r/System76/
* https://partofthething.com/thoughts/hands-on-with-the-new-system-76-lemur-pro-laptop/
* https://www.youtube.com/watch?v=vv1w78YRrNk
* https://moddingtheworld.com/review-system76s-lemur-pro/

---

### System76

[System76](https://system76.com), ABD'de (Denver/Colarado) bulunan ve birincil önceliği Linux masaüstü, dizüstü ve
sunucu bilgisayarlar üretmek olan bir girişim. Saydığım tüm üreticiler arasında adından en çok söz ettiren firma
olmasının başlıca sebepleri arasında coreboot desteğini, Lemur Pro'nun pil performansını ve Thelio serisini sayabilirim.
Ayrıca dün itibarıyla yalnızca bir bilgisayar üreticisi olmaktan çıkıp bir de 
[klavye](https://system76.com/accessories/launch) üreticisi oldular. Ubuntu tabanlı [Pop!_OS](https://pop.system76.com/) 
adını verdikleri işletim sistemiyle de hatırı sayılır bir kullanıcı kitlesine ulaşmayı başardılar. (bu konuya ayrı bir 
yazıyla yer vermeyi umuyorum)

Özellikle Lemur Pro, (aldığı son donanımsal + yazılımsal güncellemeler sonrasında) yazının başında saydığım kriterlerin 
neredeyse tamamını sağlıyor. Bunun yanısıra; System76'nın şirket olarak benimsediği vizyon ve değerler ile özellikle 
dizüstü bilgisayar üretiminde benimsedikleri yöntemlerin beni çok etkilediğini söylemeliyim ki yazının geri kalanında 
bundan bolca bahsetmek istiyorum.

#### Neden System76?

Çünkü;

* Tüm bilgisayarlarında Linux'a öncelik veriyorlar.
* Tüm dizüstü bilgisayarlarında öntanımlı olarak [coreboot]({{< ref "#coreboot--ec-firmware" >}}) firmware kurulu 
  geliyor.
* [Tamir hakkını]({{< ref "#tamir-hakkı-right-to-repair" >}}) açık bir şekilde savunuyorlar.
* Bilgisayardaki herhangi bir sorunla ilgili doğrudan destek alabiliyorsunuz. Hatta [bir kaç saat içerisinde firmware
  güncellemesi yaparak sorununuzu çözebiliyorlar](https://www.forbes.com/sites/jasonevangelho/2020/06/07/system76-lemur-pro-owners-are-about-to-get-a-free-performance-boost/?sh=2f4922971129).
* Linux için hep hayal ettiğim yakın işletim sistemi (Pop!_OS) & donanım desteği
* Uzun vadede tüm bilgisayarlarının şemasını, donanım dökümanlarını GPLv3 ile yayınlamak ve isteyenin basıp 
  üretebileceği, modifiye edebileceği bir vizyona sahipler. ([Launch](https://system76.com/accessories/launch) adını 
  verdikleri klavye tasarımına kadar GPLv3 ile dağıtılıyor ve tüm bunlara [GitHub'dan](https://github.com/system76/) 
  ulaşılabiliyor)

#### Tamir Hakkı (Right to Repair)

{{< tweet 1390599847506497542 >}}

Yeni nesil bilgisayarların çoğunda, son kullanıcı olarak hepimizin çok da farkında olmadığımız bir problem var. Yeni
nesil bilgisayarlar giderek hafifliyor ve inceliyor. Hepimizin temel kriterleri arasında olan bu duruma ulaşabilmek için
nelerden vazgeçildiğine maalesef çok kafa yormuyoruz.

Apple'ın yoğun şekilde önayak olduğu bu trend nedeniyle bir çok kritik bileşen, bilgisayarın anakartına lehimleniyor. 
Bu sayede; yerden ve ağırlıktan kazanç sağlandığı gibi, tamir gerektiren durumlarda doğrudan anakart değiştirilerek hem 
kazanç sağlanıyor, hem de üretim kolaylaşıyor.

Yukarıdaki tweet'in altına yazdığım bir yorumda, benim de yeni öğrendiğim, 
[TBW](https://www.tech-worm.com/tbw-total-bytes-written-ssd-nedir/)'den bahsetmiştim. Toplam Yazılan Bayt olarak
çevirebileceğimiz bu değer, bilgisayarınızda takılı olan SSD diskin ömrünü ifade ediyor. Bu değere ulaşıldığında
maalesef disk kullanılmaz hale geliyor. Diskiniz ana kartınıza lehimlenmiş durumdaysa 
[geçmiş olsun](https://medium.com/codex/the-shocking-discovery-of-apple-m1-ssd-that-you-need-to-know-a3a5415df1db).
Nasıl olsa bu değere ulaşamam demeyin. Yazıyı yazan kişi, bilgisayarını biraz amacı dışında kullanıyor gibi görünse de
bahsettiği sorun bununla doğrudan ilişkili değil ve herkesin başına gelebilecek bir sorun.

Şarj cihazlarının telefon kutularından çıkarılmasında çevresel nedenler ne kadar etkiliyse, bilgisayarların incelmesi ve
hafiflemesi için her şeyin lehimlenmesi de aynı ölçüde etkili desem yanlış olmaz. Hafif ve ince bir bilgisayara sahip
olmak için fedakârlık etmek zorunda değilsiniz! Çevreci ve tüketici haklarını gözeten bir iş modeli ve bunun etrafında
şekillenen bir aksesuar pazar alanı inşa etmek mümkün! Üstelik System76 bu konuda çalışan tek üretici de değil. Dün
piyasaya çıkan [Framework](https://frame.work/products/laptop-diy-edition), bu konuda oldukça iddialı bir girişim.
Başarılı olmalarını can-ı gönülden istiyorum. Lemur Pro almamış olsaydım; muhtemelen Framework'ün 
[DIY Edition](https://frame.work/products/laptop-diy-edition)'ı için $100 kaparo yatırmayı ciddi ciddi düşünürdüm.

{{< youtube fGle6z9KfZQ >}}

System76 ana geliştiricilerinden biri olan [Jeremy Soller](https://twitter.com/jeremy_soller)'ın, Louis Rossman ile 
yaptığı röportajda beni çok şaşırtan/etkileyen bazı notlarımı paylaşmak istiyorum:

* Tüm bilgisayarlarını 10+ sene dayanacak şekilde tasarlıyorlar ve tüm iş modelini bunun etrafına konumlamışlar.
* Asus, Dell, HP vb. bir çok üretici Tayvan'daki bilgisayar üreticilerine bel bağlamış vaziyette. Bilgisayarların
  kasaları, bu kasalara uyumlu anakartlar ve anakartlar üzerinde çalışan firmware'ler bu firmalar tarafından
  üretiliyormuş ve herhangi bir problem çıktığında çözümü yine bu firmalardan bekleniyormuş.
* System76, açık kaynak firmware geliştirmek için Clevo'dan cihazların şemalarını alabiliyor ve bunları (isteyen)
  müşterileriyle paylaşabiliyor.
* Cihazlarda kullanılan bir çok parçanın yedeğini almak mümkün ve nasıl değiştirilebileceğiyle ilgili sitelerinde
  [dökümanlar](https://support.system76.com/articles/service-manuals/) 
  [mevcut](https://tech-docs.system76.com/models/lemp10/repairs.html).
* Çoğu üretici için marjlar oldukça düşük: ~%5

[Linux 4 Everyone](https://www.linux4everyone.com/) podcast'i için 
[Jason Evangelho](https://twitter.com/killyourfm)'nun, [Jeremy Soller](https://twitter.com/jeremy_soller) ile yaptığı 
bölümleri mutlaka dinlemenizi tavsiye ederim:

{{< rawhtml >}}
<iframe src="https://player.fireside.fm/v2/GTYFbp1j+ODGErxgQ?theme=dark" width="740" height="200" frameborder="0" scrolling="no"></iframe>
{{< /rawhtml >}}

{{< rawhtml >}}
<iframe src="https://player.fireside.fm/v2/GTYFbp1j+8cs3C4Mn?theme=dark" width="740" height="200" frameborder="0" scrolling="no"></iframe>
{{< /rawhtml >}}

ABD'de şu aralar Tamir Hakkı konusunda ciddi bir lobi faaliyeti 
[yürütülüyor](https://www.youtube.com/playlist?list=PLkVbIsAWN2lsmovRO20_gtfUfgWi-XnnT). Şimdilik büyük bir başarı
sağlayabilmiş değiller ancak takip etmekte fayda var.

{{< tweet 1379480063159140352 >}}

#### coreboot & EC firmware

[coreboot](https://www.coreboot.org/), pek çok mimariyi destekleyen, açık kaynak kodlu bir firmware'dir. Bilgisayarın 
başlatılabilmesi için gerekli olan kod dışında bir şey içermez ve gerisini işletim sistemi seviyesine bırakır. Bu 
nedenle de coreboot'u kullanan bilgisayarlar hızlı başlamalarıyla (boot) bilinirler.

EC (Embedded Controller) firmware adı verilen ikincil firmware ise bilgisayarın (fan çalışma eğrileri, klavye düzeni
vb.) diğer bazı önemli işlevlerini yönetiyor. Bu ikisinin ayrı olması, aslında sorunların ayrıştırılmasını (separation 
of concerns) ve kişiye/modele özel özelleştirme yapılmasını kolaylaştırıyor.

System76, [açık kaynaklı firmware kullanarak](https://support.system76.com/articles/open-firmware-systems/)
bilgisayarlarının kapalı kaynak kodlu firmware'lere kıyasla pil performansı, fan çalışma eğrileri, genel performans
anlamında daha iyi ve hızlı çalıştığını iddia ediyor. EC firmware'in [GitHub sayfasına](https://github.com/system76/ec) 
bakarsanız belli konularda sıklıkla PR aldıklarını ve bunların gelişerek kullanıcının hayatında olumlu değişikliklere
yol açtığını görebilirsiniz. Örneğin [Jason Evangelho](https://twitter.com/killyourfm)'nun Forbes için 
[yazdığı](https://www.forbes.com/sites/jasonevangelho/2020/06/07/system76-lemur-pro-owners-are-about-to-get-a-free-performance-boost/?sh=2f4922971129) 
bir inceleme/karşılaştırma yazısında, Lemur Pro'nun diğer modeller karşısında bazı eksikliklerini olduğunu görmesi ve
bunu System76 mühendislerine bildirmesi sonrasında, kısa sürede yapılan performans iyileştirmelerinden bugün tüm Lemur 
Pro kullanıcıları faydalanıyor.

{{< figure src="pgdnup.jpg" caption="Lemur Pro'nun herkesçe eleştirilen PgUp & PgDn tuş düzeni" >}}

Bir de kendimden örnek vereyim. Yukarıdaki görselde de gördüğünüz üzere; Lemur Pro'nun `Page Up` & `Page Down` tuşları
maalesef yön tuşlarıyla dipdibe. Bu durum nedeniyle herhangi bir şey yazarken sıklıkla bu tuşlara basıyor ve saçma sapan
sorunlar yaşıyordum. [Şu sayfada](https://github.com/system76/ec/blob/master/doc/keyboard-layout-customization.md) yazan 
yönergeleri takip ederek EC kodunda bu tuşları sol ve sağ olarak yeniden düzenledim ve Fn tuşuna basıldığında `PgUp` & 
`PgDn` olarak davranmalarını sağladım.

Elbette EC güncellemesinin yanlış gitmesi sonucu bilgisayarımı geçici bir süre kullanamama riskim de mevcut ancak bu 
özgürlük ve klavye düzenimi tamamen değiştirebiliyor olmak çok daha önemli. Öte yandan bu tür düzenlemeleri EC
güncellemelerinden bağımsız hale getirmek ve hatta işletim sistemi tarafından kontrol edilebilir hale getirmek için de
bir [PR](https://github.com/system76/ec/pull/63) mevcut.

#### Nasıl aldım?

System76 hali hazırda 64 ülkeye gönderim [yapıyor](https://system76.com/shipping). Türkiye, maalesef bu ülkeler arasında 
yer almıyor. ABD ile Türkiye arasındaki ticaret sözleşmeleri maalesef bilgisayarların ticaretine olanak sağlamıyormuş. 
Bu konuda İngiltere ve AB ülkeleriyle sorunumuz yok. ABD ile sorun yaşamamıza şaşırdım ama konunun detaylarıyla ilgili 
yeterince bilgi de alamadım.

Aklıma ilk gelen çözüm, İngiltere'deki dayıma yollayıp oradan bir şekilde Türkiye'ye getirtmek oldu. ABD'den
İngiltere'ye kargo ücreti ~$120 tutuyor. Bu vesileyle öğrenmiş oldum ki; bu fiyatın üzerine, bir de İngiltere'ye 
girişte %20 civarında vergi (VAT) ekleniyor. Ayrıca İngiltere'nin sınırlarını kapatmış olması nedeniyle bilgisayarı
ne zaman teslim alabileceğim net değildi. Oradan Türkiye'ye gelirken de gümrüğe takılma durumunu düşününce bu ek
masraflara girmeden halledebilir miyim diye araştırmaya başladım. Ne de olsa vergiden kaçınmak 
[ata sporumuz](https://onedio.com/haber/kizilay-baskani-kinik-tan-ensar-vakfi-aciklamasi-vergi-kacirmak-baska-vergiden-kacinmak-baska-895906).

İşte tam da bu noktada karşıma [amerikapostam.com](https://amerikapostam.com/) adındaki site çıktı. Çok kabaca; ABD'den
aldığınız ürünleri size verdikleri adrese yönlendiriyorsunuz. Gelen her ürün için ayrı ayrı bilgilendiriliyorsunuz. Ve
istediğiniz an, dilerseniz (küçülterek masrafları düşürmek adına) yeniden paketleme de yaptırarak, Türkiye'deki
adresinize göndertebiliyorsunuz. Elbette kargo ve gümrük bedellerini ödedikten sonra. 😊 ABD'deki sitelere ödemede
sorunlar yaşıyorsanız talep etmeniz durumunda sizin adınıza satın alma da yapabiliyorlar. Tüm bu detaylara sitelerinden
ulaşabilir, sorularınız varsa da Whatsapp'tan iletebilirsiniz. Ben Whatsapp'tan sorduğum tüm sorulara hızlı ve net
cevaplar aldım. Hem sitelerinden, hem de Whatsapp'tan güven verdikleri; hem de 
[Ekşi Sözlük](https://eksisozluk.com/amerikapostam-com--4581484)'te son derece olumlu yorumlar gördüğüm için 
alışverişimde bu siteyi tercih etmekte bir sakınca görmedim.

System76'in sitesinden alışverişimi [papara](https://www.papara.com/)'ya ait sanal kartımla yaptım. Siparişi verdikten
kısa bir süre sonra telefonla arandım ve kartın gerçek sahibi olduğumun teyidi amacıyla, kart ekstremdeki harcamaya ait
kodu kendileriyle paylaşmam istendi. Bunu da yaptıktan sonra siparişim onaylandı ve fabrikaya iletildi.

Küresel çip krizi nedeniyle siparişimi bir an önce vermek istediğim için, ilk olarak İngiltere'ye gidecek şekilde
sipariş verdim. (İyi ki de vermişim çünkü kısa süre sonra sitedeki tüm bilgisayarlar tükendi; bu yazıyı yazdığım esnada 
hala da stok eklenebilmiş değil) Ancak sonradan amerikapostam.com'a yollayacak şekilde değişiklik yaptım. Konuyla 
ilgili System76'a ulaştım; kısa sürede değişikliği yapıp ~$88'ı kartıma iade ettiler.

Bilgisayar yaklaşık 2 hafta içinde amerikapostam.com'a ulaştı ve yaptıkları ölçümlere dair bir resmi de içeren,
cihazın kendilerine ulaştığını teyid eden bir e-posta aldım. Bu aşamada yeniden paketleme için bir tercih yapmam
gerekiyordu. System76'ın bilgisayarı göndermek için kullandığı kutu, olası hasarlara karşı bilgisayarı oldukça iyi
koruyacak (ve olur da geri göndermem gerekirse diye tekrar kullanılabilir) şekilde tasarlanmış. Türkiye'ye gelirken
hasar görmesini göze alamadığım için yeniden paketleme talep etmedim. (Yapsaydım 13 LBS olan paket ~3 LBS civarına
düşecek; kargo fiyatı da 1/3 oranında düşecekti)

Sonuç olarak; amerikapostam.com'un hesapladığı kargo ($75) + gümrük bedeli ~$325 idi. Ödemeyi yaptıktan bir kaç saat 
sonra  kargonun gönderim için yola çıktığına dair bildirim aldım. 1-2 gün içerisinde JFK havalimanına ulaşmıştı bile. 
Ve tam olarak geleceğini söyledikleri gün elime ulaştı. 7 Nisan'da sipariş ettiğim bilgisayar, Nisan'ın son haftasında 
elime ulaştı. Hem doğrudan ABD içi gönderim yaptığım için İngiltere üzerinden yollamaya göre tasarruf etmiş oldum, hem 
de sınırların kapalı olması nedeniyle yaşayacağım gecikmeden kaçınmış oldum. amerikapostam.com'un verdiği hizmetten son 
derece memnun kaldığımı söylemeliyim.

### Lemur Pro

{{< figure src="kutu.jpg" caption="System76 bilgisayar kutuları ürünü tamire göndermek için tekrar kullanılabilecek şekilde tasarlanmışlar." >}}

En başta bilgisayar seçerkenki kriterlerimden bahsetmiştim. Kullandığım şirket bilgisayarları genellikle 15" ve oldukça
ağırlar. Bu nedenle 13-14" boyutunda bir bilgisayar tercih ediyorum. Dürüst olmam gerekirse bu formun ne denli minyon
olabildiğini unutmuşum. 😊 Fotoğraflardan çok anlaşılmasa da bilgisayarı görünce ufak çaplı bir şok geçirmedim desem
yeridir.

{{< figure src="dell_ile_karsilastirma.jpg" caption="Kıyaslamak için Dell Precision 5530 ve Lemur Pro üst üste" >}}

Kocaman kutudan bilgisayarın dışında taşıması kolay 65W gücünde bir adaptör çıkıyor. Kablo uzunluğuyla ilgili yoğun
eleştiriler alsa da ABD tipi fişi değiştirirken 3 mt'lik bir kablo tercih ederek bu problemin üstesinden geldim.
Bilgisayar USB-C üzerinden de şarj olabiliyor ama kutudan çıkan adaptör barel tipinde. ~2-3 saat içerisinde tam şarj 
sağlıyor.

Kutudan bunun haricinde bir adet ekran silme bezi, bir kaç yapıştırma dışında bir şey çıkmıyor.

{{< figure src="lemur_kapali.jpg" >}}

Bilgisayar ~1 kg civarında ve magnezyum kasalara benzer plastiğimsi bir yüzeye sahip. Zaman zaman çantamı kaldırırken
bilgisayarı unutmuş olabilir miyim diye açıp kontrol ettiğimi itiraf etmeliyim. 😊 Zevkler elbette değişir ancak ben
bilgisayarın genel olarak ucuz/basit görünmediğini ve oldukça hoş bir hissiyâtının olduğunu düşünüyorum.

Benim aldığım model şu özelliklere sahip:

* **OS:** Pop!_OS 20.10 (64-bit) (tamamen şifrelenmiş disk ile)
* **CPU:** 11th Gen Intel® Core i5-1135G7: Up to 4.20 GHz - 8MB Cache - 4 Cores - 8 Threads
* **Bellek:** 40 GB DDR4 @ 3200 MHz
* **Disk:** 500 GB PCIe Gen3 Seq Read: 2400 MB/s, Seq Write: 1750 MB/s

{{< figure src="lemur_acik.jpg" >}}

Bilgisayarı açar açmaz beni kurulum asistanı karşıladı. Dil/klavye seçimi, kullanıcı tanımı gibi bir kaç adım sonrası
kullanıma hazır hale geldi ve açılır açılmaz da ilk güncellemeler (firmware dahil) geldi. Tüm güncellemeleri yaptım ve
ilk günden bu yana gayet güzel bir şekilde çalışıyor.

Bilgisayarla ilgili genel notlarım şu şekilde:

* Dell'de NVIDIA kartı kapatmama rağmen maksimum 3-4 saat görebiliyorum. Bu cihazda ise tüm gün şarj gerekmeden
  çalışabiliyorum. (henüz tam ölçüm yapmadım)
* Zaman zaman yaptığım işe göre, fan sesini duyabiliyorum. Şu ana kadarki deneyimim; hızlı bir şekilde devreye girip en
  kısa sürede kapanmak üzere ayarlanmış gibi görünüyor. IDE kodu tararken ya da Windows VM (ievms) başlattığımda fan 
  devreye girebiliyor. IDE özelinde çok uzun süre çalışıyor diyemem ama Windows VM'de aralıksız çalışıyor. Windows VM
  konusunda genel olarak [bir sıkıntım](https://www.reddit.com/r/System76/comments/n9xgqo/bad_windows_experience_inside_virtualbox/) 
  var ancak görünüşe bakılırsa başkalarının daha farklı deneyimleri var. Bu konuda denemelere devam edeceğim.
* Tüm incelemelerde değinildiği üzere; bilgisayarın hoparlörleri maalesef iyi değil. Tizler biraz yüksek kaldığı için
  müzik dinlemek için çok uygun olduğunu söyleyemem. Toplantı ya da Youtube'dan bir şeyler izlemek için fena değil.
* Touchpad'i gayet güzel çalışıyor. Birden çok parmakla çalışma alanları arasında gezinebiliyor. 
  [GNOME 40](https://youtu.be/vK-SwsWnEmo)'ı denemek için sabırsızlanıyorum.
* 1M 720p kamerası var ve görüntü kalitesi iyi. Cihazda sanırım Windows Hello sensörleri de mevcut; uygun bir vakitte
  [howdy](https://github.com/Boltgolt/howdy) ile bir deneme yapmayı düşünüyorum. 🤞
* Klavye ışıkları için 5 kademe var ve kendi kendine sönmüyor. İhtiyacınız yoksa sizin kapatmanız gerekiyor. Cihazda
  ortam ışığı sensörü olmadığı için bu konuda sanırım bir firmware düzenlemesi de gelemeyecek.
* FHD mat bir ekrana sahip. Benim için fazlasıyla yeterli ve parlak diyebilirim. Hatta geceleri biraz fazla parlak
  kaldığı için fazladan kısmak için bir [eklenti](https://extensions.gnome.org/extension/1625/soft-brightness/) kurmam 
  gerekti.

{{< figure src="neofetch.png" caption="neofetch komut çıktısı (shell olarak `zsh` kullanıyorum bu arada)" >}}

Son olarak; Pop!_OS'le ilgili notlarım şöyle:

* Ubuntu tabanlı bir işletim sistemi olmasına rağmen farklı tercihler yapılan noktalar var. Örneğin GRUB yerine
  systemd-boot kullanıyor. Çok fazla yorum yapacak kadar konuya hakim değilim ama bu tercih sayesinde Ubuntu 21.04'ün
  çıkışının [ertelenmesine sebep olan hatadan](https://www.omgubuntu.co.uk/2021/04/why-you-cant-upgrade-to-ubuntu-21-04-for-now) 
  etkilenmiyordu.
* Genel olarak Ubuntu'dan daha yalın ve hızlı bir deneyim sunduğunu söylemeliyim.
* Pop Shell denen ve pencere yönetimini ızgaralara oturtan mod çalışma şeklime yeni bir şekil verdi. COSMIC ile birlikte
  [gelecek değişiklikleri](https://youtu.be/ydRlDv0heAo) sabırsızlıkla bekliyorum.
* Ubuntu'dan farklı olarak snap paketleri yerine flatpak tercih edilmiş. Bu konuda ciddi endişelerim vardı ancak snap
  entegrasyonu oldukça sorunsuz. An itibarıyla 27 flatpak, 22 snap pakedi kurmuş görünüyorum. 😊 Flatpak vs snap
  konusunda zaman içerisinde ayrı bir yazı hazırlamayı düşünüyorum.

{{< youtube ydRlDv0heAo >}}

Lemur Pro, kargo ve gümrük dahil bana yaklaşık olarak ₺16k civarına geldi. Benzer özelliklerdeki pek çok cihaz maalesef
₺20-30k bandında satılıyor. Cihazla ilgili şimdilik yazacaklarım bu kadar. Sorularınız varsa her zaman benimle iletişime
geçebilirsiniz.
