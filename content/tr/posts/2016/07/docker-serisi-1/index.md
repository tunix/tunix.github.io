---
title: "Docker Serisi #1"
date: 2016-07-13
slug: docker-serisi-1
cover:
    image: docker.png
    caption: Docker'ın sembolü; balina üstü container 🙂
tags:
    - yazılım
    - docker
    - docker serisi
    - container
    - sanallaştırma
    - linux
    - devops
---

[Docker’laştıramadıklarımızdan mısınız?]({{< ref "dockerlastiramadiklarimizdanmisiniz" >}}) başlıklı yazımda 
bahsettiğim serinin ilk yazısına biraz temelden girerek başlayacağım. Öncelikle İngilizce’niz varsa Docker’ın CTO’su 
Solomon Hykes’ın yaptığı aşağıdaki sunumu izlemelisiniz.

{{< youtube Q5POuMHxW-0 >}}

### Sanallaştırma Hakkında

Sanallaştırma, Virtualbox veya VMWare gibi yazılımlardan aşina olabileceğiniz gibi; bilgisayarınızın işlemci, bellek 
gibi kaynaklarını paylaşan, tamamen ayrı bir bilgisayarmış gibi işletim sistemi çalıştırabileceğiniz teknolojinin 
genel adı. Bu teknoloji sayesinde örneğin bilgisayarınızda Windows çalışırken Ubuntu ya da Mac işletim sistemlerini 
performanslı bir şekilde çalıştırıp kullanabilirsiniz. Hatta bazı sanallaştırma yazılımları sayesinde yalnızca bu 
işletim sistemlerinde çalışabilen uygulamaları gerçek birer Windows uygulamasıymış gibi kullanabilirsiniz. Tabii 
tersi (Mac üstünde Windows uygulamaları) de mümkün. Virtualbox, VMWare gibi bu işi mümkün kılan yazılımlara 
[Hypervisor](https://en.wikipedia.org/wiki/Hypervisor) deniyor ve temel görevi, bilgisayarınızda kurulu işletim 
sistemi üzerinden donanım kaynaklarınızı paylaştırıp sanal işletim sistemlerinin ihtiyaç duyduğu gereksinimleri 
sağlamak.

{{< figure src="hypervisor.png" caption="Sanal makineler, Hypervisor denen yazılımlar aracılığıyla işletim sistemiyle ve dolayısıyla donanımla iletişime geçebiliyor." >}}

### Container Nedir?

{{< figure src="kernel_support.png" caption="Container’lar çekirdekteki doğrudan gelen destek nedeniyle Hypervisor’a ihtiyaç duymuyor." >}}

Container teknolojisi, Hypervisor’dan farklı olarak, işletim sistemi çekirdeğinde doğrudan destekleniyor ve bu sayede 
daha az kaynak tüketerek, daha verimli ve daha hızlı çalışabiliyor. Linux çekirdeğine ilk olarak 2008 yılında eklenen 
[LXC](https://en.wikipedia.org/wiki/LXC) (Linux Containers) desteği, Docker’ın atası diyebiliriz. O dönemde kullanımı 
için ek yazılımlar kurulması, Linux’da donanımların çalışmasıyla ilgili ek bilgi gerektirmesi ve imaj hazırlamanın 
güçlüğü gibi sebeplerle yaygınlaşamayan bu teknoloji, bugün Docker sayesinde çok popüler ve kullanımı her geçen gün 
artıyor. Bu noktada Google’ın haftada 2 milyar container 
[başlattığını](https://speakerdeck.com/jbeda/containers-at-scale) belirtmeden geçemeyeceğim.

Container’ı tanımlamak için Solomon Hykes’ın söylemini çok beğeniyorum. Yük gemilerinin taşıdıkları büyük renkli 
kutuları bilirsiniz. İçine herhangi bir şey koyarsınız ve sonrasında o kutuyu istediğiniz yere götürebilirsiniz. 
Kutuyu taşımanın, kutuyla etkileşimin yolu yordamı bellidir. Kutuyla etkileşimde olan kişiler için, içinde ne 
olduğunun artık bir önemi yoktur. Sadece kutunun kime ait olduğunu, nereye gideceğini ve o kutuyla ne yapacaklarını 
bilirler ve buna göre hareket ederler. Peki bunu yazılım için de yapamaz mıyız?

{{< figure src="container.png" caption="Görsel: [Tech Finance](http://techfinance.info/blog/devops/docker/shallow-diving-on-containers-structure)" >}}

Bazı rolleri düşünelim: geliştirici, testçi, sistem yöneticisi, kullanıcı vs.. Kod yazarken başka kod parçalarına 
bağımlılıklarımız var. Bazen çalışılacak ortamda X ayarlarının yapılmış olması, Y yapılandırma dosyasının bulunması 
gibi kriterler olabiliyor. Yukarıda yazdığım rollerdeki insanlara bu farklı kriterlere hakim olma sorumluluğunu 
yüklemek doğru mu? Geliştirme ortamıyla test ortamı her zaman aynı olabilir mi? Kullanıcı bir uygulamayı çalıştırmak 
için başka bir şeyler kurmak zorunda mı? Üst paragrafta bahsettiğim anlayışı uygulayarak herkesin kendi rolüne 
odaklanmasını sağlayabiliriz.

Geliştirici yazdığı kodu, kodun bağımlılıklarını ve çalışması için gerekli olan her şeyi bir container imajı halinde 
paketler. Testçi, sistem yöneticisi ve kullanıcı için bu paket artık bir “kutudur”. Testçi kutuyu alır, çalıştırır, 
verdiği girdiye karşılık beklediği karşılıkları test eder. Sistem yöneticisinin bu projedeki sorumluluğu artık 
yalnızca kutuların yerini değiştirmek ve sistemin çalıştığından emin olmaktır. Kullanıcı için bu, artık yalnızca yeni 
bir kutudur, eskisiyle değiştirip hayatına devam edecektir. Kulağa hoş geliyor, değil mi? :)

### Docker Nedir?

Docker, 2013 yılında dotCloud tarafından geliştirilen ve temelde Linux çekirdeğindeki container desteğinin kullanımını 
son derece kolaylaştıran bir araç. Bahsettiğim destek Linux çekirdeğinde (2.6.24) uzun zamandan beri bulunduğundan 
bugün çalıştığımız tüm sunucularda desteklendiğini söylemek mümkün. Uzunca bir süre Windows ve Mac çekirdeğindeki 
desteğin noksanlığı nedeniyle Virtualbox vb. üstünde [boot2docker](http://boot2docker.io/) adında bir Linux sunucusu 
başlatmamız gerekiyordu. Bu durum Apple cephesinde yakın zamanda değişeceğe benzemiyor olmakla birlikte Windows 10'daki 
(64 bit) HyperV teknolojisiyle birlikte doğal desteğe kavuşuyor.

Dilerseniz Docker’ı tanımaya terminolojisiyle devam edelim.

### Docker Engine Nedir?

Docker çalıştıracak her makineye kurulması gereken, içerisinde yazılımsal bir sunucu (server) ve komut satırı 
istemcisi (client) bulunan bir paket. Sunucu tarafı makinenizdeki container’ları yönetirken, istemci tarafı sunucuya 
komutlarla hükmetmenizi (yeni container aç, kapa vs.) sağlıyor.

{{< figure src="docker_ps_ciktisi.png" caption="Görsel: [Microsoft Visual Studio Code Blog — Getting Started with Docker](https://blogs.msdn.microsoft.com/vscode/2015/08/11/getting-started-with-docker/)" >}}

### Docker Container Nedir?

Kabaca çalışmasını istediğiniz programın asgari ihtiyaçlarının tamamını barındıran kapsayıcı imajın çalışan hali. 
Program, container içinde çalıştığında, tamamen izole edilmiş (sandbox) bir ortamda çalışmış oluyor ve genellikle bir 
container, bir süreç (process) demek. Çeşitli betikler (script) kullanarak alt süreçler başlatabileceğiniz gibi, 
supervisord gibi süreç yöneticiler kullanarak da bu limiti safdışı bırakabilirsiniz. İleriki serilerde bahsedeceğim 
sebeplerden ötürü elzem olmadıkça çoklu süreçlere sahip container’lara yönelmemelisiniz.

### İmaj ne demek?

İmaj, çalıştıracağınız bir program için ihtiyaç duyulan her şeyi barındıran minimal disk imajlarıdır. Örneğin 
ubuntu:14.04 imajı, içerisinde Ubuntu Linux dağıtımının minimal halini barındıran ve minimal olabilmek adına bir çok 
paketi bulundurmayan bir disk imajıdır. Öntanımlı olarak Bash kabuğuyla gelir ve bu imajdan yarattığınız container 
içerisinde ihtiyacınız olan yeni yazılımları kurarak yeni bir imaj oluşturabilirsiniz.

Her container, bir imajı baz alarak başlar ve imajlar birbirinden miras alabilirler. Docker’daki imaj teknolojisi 
[AUFS](https://en.wikipedia.org/wiki/Aufs) adındaki bir dosya sistemi kullandığından yaptığınız her değişiklik yeni 
bir katman olarak kaydedilecektir. Bu sayede geçmiş bir katmana geri dönebileceğiniz gibi, yeni katmanlar ekleyerek 
kendi imajlarınızı yaratabilirsiniz. Baz olarak Ubuntu’yu alıp (birine vim, ötekine emacs kurduğunuz) 2 farklı disk 
imajı yarattığınızı varsayalım. Bu 2 imajı baz Ubuntu ile kıyaslasak aradaki katman yalnızca vim ve emacs için kurulan 
dosyaları içeriyor olacaktır. Oluşturacağınız imajların minimal olması özellikle taşınabilirlik nedeniyle son derece 
önemli olacağından yapacağınız her değişikliğin yeni bir katmana sebep olacağını anlamanız önemli.

{{< figure src="docker_run_ciktisi.png" caption="Görsel: [Microsoft Visual Studio Code Blog — Getting Started with Docker](https://blogs.msdn.microsoft.com/vscode/2015/08/11/getting-started-with-docker/)" >}}

Oluşturduğunuz imajları fiziksel olarak kopyalayabileceğiniz gibi registry adındaki depolara atabilir; başkalarının da 
faydalanmasını sağlayabilirsiniz. Bu iş için [Docker Hub](https://hub.docker.com/)’ı kullanabilir ya da 
[açık kaynak kodlu depoyu](https://github.com/docker/distribution) kurup özel imajlarınızı kendi sunucu ortamlarınızda 
saklayabilirsiniz.

### Docker'ı nerelerde kullanabiliriz?

Maddeler halinde bazı kullanım alanlarını belirteyim:

* Geliştirme ortamından çıkan paketi hiç bir değişiklik yapmadan test ortamında ve gerçek ortamda kullanabilirsiniz.
* CI ortamında paket oluşturmak ya da testleri koşturmak için kullanabilirsiniz.
* Geliştirme ortamında vagrant vb. bir araç kullanıyorsanız Docker’ı benzer şekilde kullanabilirsiniz.
* [Amazon Lambda](https://aws.amazon.com/lambda/details/) ya da [Koding](http://www.koding.com/)’de yapıldığı gibi, 
  bir süre çalışıp sonrasında bir sonraki çalışmaya kadar duracak işler için kullanabilirsiniz.
* Mikro servisler yazmak için çok uygun olduğundan altyapı olarak kullanabilirsiniz.
* İzolasyon sağladığından masaüstü uygulamalarınızı container’lar içinden 
  [çalıştırabilirsiniz](https://blog.jessfraz.com/post/docker-containers-on-the-desktop/). Örneğin 
  [Eclipse Che](https://eclipse.org/che/)’yi kurmak çok uğraştırdığından 
  [docker ile kullanmayı](https://eclipse-che.readme.io/docs/usage-docker#using-docker-syntax) tercih edenlerin sayısı 
  az değil.

{{< figure src="jessie.png" caption="Jessie Frazelle, kişisel bilgisayarında Docker içinde çalışan Chrome ile Google Hangouts denemesi [yapıyor](https://blog.jessfraz.com/post/docker-containers-on-the-desktop/)." >}}

### Docker'ın avantajı nedir? Sanal makinemi neden bırakayım?

Aslında bırakmayabilirsiniz. Şahsen PHP ya da Python projesi yazıyor olsam muhtemelen uzun süre Vagrant ile devam edip 
sonradan docker’a geçmeyi düşünürdüm. Sonraki serilerde bu konuya daha detaylı gireceğim için şimdilik en bilinen 
avantajları yazayım:

* VM’lerin aksine container’lar saniyeler içerisinde ayağa kalkabiliyor. Yönetim maliyetleri & eforları VM’lere 
  nazaran daha düşük.
* Doğrudan çekirdek desteği nedeniyle hypervisor’ın yarattığı gereksiz yükten kurtuluyorsunuz.
* Container imajları, VM imajlarına göre çok daha küçük olduklarından taşınmaları daha kolay oluyor. Yeni imaj, 
  varolanın üstüne ek bir katman olduğundan güncelleme için komple yeni bir imaj alınmıyor.
* İmajı hiç değiştirmeden, sadece çevresel değişkenler vererek, container’ın bambaşka davranması sağlanabiliyor. Bu 
  konuya sonraki serilerde uzun uzun değineceğim.

### Docker'ı kimler kullanıyor?

Google’ın her hafta 2 milyar container başlattığından yukarda söz etmiştim. Bunun dışında; Netflix, Spotify, Yandex, 
ebay, Amazon, Uber, Shopify gibi şirketlerde oldukça aktif bir şekilde kullanılıyor.

{{<figure src="docker_istatistik.png" caption="Görsel: [The Evolution of the Modern Software Supply Chain](https://www.docker.com/survey-2016)" >}}

### Docker Kurulumu

Linux kullanıyorsanız mutlaka paket yöneticileri aracılığıyla kurun. Windows için Docker’ın kendi kurulum paketini 
tercih edebilirsiniz. Benim gibi Mac kullanıyorsanız kullanım kolaylığı açısından 
[Mac paketi](https://www.docker.com/products/docker#/mac) yerine [brew](http://brew.sh/) kullanmayı tercih edin. Bu 
sayede kurması, güncellemesi ve kaldırması çok daha kolay olur. Ayrıca serinin devam yazılarında bahsedeceğim ek 
Docker projelerini (docker-compose, docker-swarm vs.) kurmanız da [brew](http://brew.sh/) ile daha kolay.

Kurulumla ilgili çok fazla kaynak olduğundan ve genellikle bir kaç adımı geçmediğinden pek detaya girmeyeceğim ancak 
sorularınızı yorum olarak yazarsanız elimden geldiğince yardımcı olmaya çalışabilirim.

### Bir sonraki yazıya...

Bir sonraki yazıda docker komutlarının kullanımı, basit kullanım, kendi imajınızı yapma, Dockerfile gibi konulardan 
bahsedeceğim. O zamana kadar görüşmek dileğiyle!✌️
