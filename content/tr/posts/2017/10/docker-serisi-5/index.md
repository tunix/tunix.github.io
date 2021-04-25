---
title: "Docker Serisi #5 -- Docker Machine & Swarm Bölüm 1"
date: 2017-10-30
slug: docker-serisi-5
tags:
    - yazılım
    - docker
    - docker serisi
    - container
    - sanallaştırma
    - linux
    - devops
---

5. bölüme hoşgeldiniz! 🤘🏻 Serinin önceki bölümlerine ulaşmak için aşağıdaki bağlantıları kullanabilirsiniz:

* [Docker Serisi #1]({{< ref "docker-serisi-1" >}})
* [Docker Serisi #2 — Docker Engine Bölüm 1]({{< ref "docker-serisi-2" >}})
* [Docker Serisi #3 — Docker Engine Bölüm 2]({{< ref "docker-serisi-3" >}})
* [Docker Serisi #4 — Docker Compose]({{< ref "docker-serisi-4" >}})

Serinin bu bölümünde Docker Machine’den ve teknoloji camiasının bu sıralar çok sık duyduğu Docker Swarm’dan 
bahsedeceğim. Swarm konusu derya deniz olduğundan konuyu 2 ayrı bölüm halinde işleyeceğim. İlk bölümde Docker 
Machine’den bahsedip Swarm’a giriş yapacağız. İkinci bölümdeyse Swarm’ın, makine topluluklarının yönetiminde nasıl 
kolaylıklar sağladığını; örnek bir projenin makinelere dağıtılması ve ölçeklenmesiyle göreceğiz!

---

### Docker Machine Nedir?

Diyelim ki kendi makinenizde ya da bulutta (cloud) bir Docker makine ağı (cluster) kurmak istiyorsunuz. Eskiden bunu 
nasıl yapardık? Gelin kendi makinemizde (Virtualbox kullandığımızı varsayarak) yapacak olsaydık neler yapacaktık; bir 
gözatalım:

* Kuracağımız işletim sisteminin disk imajını (ISO) indirilmesi
* Virtualbox’ta N tane VM yaratılması ve her birinin ayarlarını düzenlenmesi (disk, bellek, işletim sistemi imajı vb.)
* Her bir VM’i başlatıp işletim sisteminin kurulması ve yapılandırılması (dil/zaman/klayve ayarları, disk ayarları vb.)
* Her bir VM için işletim sisteminin son güncellemelerinin yapılması ve ihtiyaç olabilecek paketlerin kurulumu
* Her bir VM için Docker paket deposu ayarlarının yapılması, Docker kurulumu ve yapılandırması (Docker Engine’in 
  dinleyeceği bağlantı noktaları -port’lar-, atanacak etiketler -label’lar- vb.)
* DigitalOcean gibi bulut ortamlarında Docker’ın TLS ile çalışacak şekilde ayarlanması tavsiye ediliyor. Bu nedenle 
  gerekli sertifikaların yaratılması ve Docker Engine’in TLS modunda çalıştırılması.

Bu listede yapılacak işler, proje ihtiyacına göre uzayabilir. Elbette basit bir betikle (script) bu işler otomatize 
edilebilir. Peki farklı bulut ortamlarında da bu adımları yapmanız gerekirse? İşler zorlaşıyor, değil mi? 😉

Docker Machine, tam olarak bunları çözüyor. İster kendi makineniz, isterseniz de AWS ya da DigitalOcean gibi bir bulut 
ortamı olsun; Docker Machine ile ihtiyacınız olan makineleri, istediğiniz özelliklerde ve istediğiniz adetle 
yaratabiliyorsunuz.

#### Virtualbox ile Yerel Geliştirme

Serinin daha önceki bölümlerinde söylediğim gibi; eğer Mac kullanıyorsanız, Docker for Mac kullanmanız en sağlıklısı. 
Ancak özel bir ihtiyaçtan ya da Swarm denemesi yapacağınız varsayımıyla Linux tabanlı Docker makinelerine ihtiyacınız 
varsa Docker Machine’i kullanabilirsiniz:

```
docker-machine create -d virtualbox \
    --engine-insecure-registry registry.local \
    --engine-label role=node \
    --engine-label role=manager \
    manager1
```

Parametrelerin anlamına bakalım;

* `-d`: Kullanılacak sürücüyü (driver) belirler. Virtualbox için `virtualbox`, AWS için `amazonec2`, DigitalOcean 
  içinse `digitalocean` yazabilirsiniz.
* `--engine-insecure-registry`: Docker Hub dışında bir imaj deposu ve kendi ürettiğiniz bir SSL sertifikası 
  kullanıyorsanız bu parametreyi kullanmalısınız. Böylece Docker Engine’in, imaj deposuna bağlanmaya çalışırken yaptığı 
  güvenlik kontrollerini geçiştirmiş olacaksınız.
* `--engine-label`: Docker Engine’e etiketler atayarak özellikle Swarm modunda container’ların yerleşiminin bu 
  etiketlere göre yapılmasını sağlayabilirsiniz. Tek makine açacaksanız tanımlamasanız da olur. `role=node` gibi 
  tanımlar tamamen tercihe bağlı. Diyelim ki makineye s3fs kurdunuz. Bu durumda Docker Engine’e `s3fs=enabled` gibi 
  bir etiket atayarak s3fs’ten faydalanan container’ların bu makinelere yerleşmesini sağlayabilirsiniz.

Sondaki `manager1` ise makinemize ulaşmak için kullanacağımız isim olacak. İlk makinemizi yarattıktan sonra 
`docker-machine ls` komutunu verirsek açık olan makinelerimiz listelenecektir. Daha önce farklı bulut ortamlarında 
makineler açtıysanız bu makineler de bu listelemede gözükecektir. Yani _ortam bağımsız_ olarak Docker Machine ile 
açtığınız tüm makineleri görme imkanına sahipsiniz.

{{< figure src="docker_machine_ls_ciktisi.png" caption="`--filter driver=virtualbox` ya da `--filter label=role=worker` gibi parametrelerle listelemeyi kontrol edebiliyorsunuz." >}}

Oluşturduğunuz makineleri silmek isterseniz;

```
docker-machine rm deneme
```

komutuyla silebilirsiniz.

Makinenin içine SSH ile girmek için;

```
docker-machine ssh deneme
```

komutunu verebilirsiniz. İçine girdikten sonra docker komutlarıyla istediğiniz gibi çalışabilirsiniz. Alternatif olarak 
kendi makinenizden bu makineyi hedefleyerek çalışabilmek için;

```
eval $(docker-machine env deneme)
```

komutunu verebilirsiniz. Bu komut, bulunduğunuz terminal oturumundaki `DOCKER_HOST` vb. değişkenlerin değerlerini, 
Docker Machine ile açtığınız makinenin değerleriyle değiştirerek, yazdığınız komutların o makine tarafından 
çalıştırılıp çıktısının sizin makinenizde gösterilmesini sağlar. Yani kendi makinenizden, uzaktaki makinede docker 
komutları çalıştırmış oluyorsunuz.

Tekrar kendi makinenizdeki Docker Engine’e dönmek isterseniz terminali açıp kapatabilir ya da;

```
eval $(docker-machine env -u)
```

> Protip: Docker Machine’i özellikle AWS vb. bulut ortamlarında makine açmak için kullanacaksanız 0.12.2+ kullanmanızı 
> öneririm. Aradaki sürümlerde Ubuntu vb. dağıtımlardaki değişiklikler nedeniyle problem yaşayabilirsiniz.

Docker Machine ile yapabileceğiniz diğer işlemler hakkında bilgi almak için `docker-mackine` komutunu hiç bir parametre 
olmadan vermeniz yeterli. Alt komutlarla ilgili bilgi almak içinse örneğin;

```
docker-machine create --help
```

yazabilirsiniz.

Docker ekosistemindeki değişiklikler son derece hızlı gerçekleşiyor ve zaman zaman alt projeler bu değişime ayak 
uyduramayabiliyor. Üst paragrafta söylediğim şekilde `docker-machine`’in desteklediği komutlara baktıysanız swarm’la 
ilgili de bazı komutlar içerdiğini göreceksiniz. Swarm oluşturmak için, aşağıda bahsedeceğim yeni yöntemleri 
kullanmanız daha iyi olur. Docker Machine ile swarm yöneticisi yaratmak ya da swarm ağına dahil olmak şimdiden demode 
sayılmaya başlamış bile!

#### AWS’de Makine Açmak

Docker Machine’in güçlü yanlarından birisi bulut ortamlarında da rahatlıkla makine açabiliyor olmanız. Bunun için 
AWS’de bir hesabınız ve bu hesaba ait anahtarların (token) elinizde olduğundan emin olun.

```
docker-machine create -d amazonec2 \
    --amazonec2-access-key erisim-anahtari \
    --amazonec2-secret-key cok-gizli-anahtar \
    --amazonec2-region eu-west-1 \
    --amazonec2-vpc-id ozel-vpc-id \
    --amazonec2-instance-type m4.large \
    --amazonec2-root-size 50 \
    --amazonec2-iam-instance-profile automated \
    --amazonec2-monitoring \
    --engine-label role=node n1
```

Kullandığım parametrelerin isimlerinden anlaşıldığını düşünüyorum. Sadece bazılarını neden özellikle yazdığımı 
paylaşayım;

* `--amazonec2-vpc-id`: Öntanımlı VPC ağını sildiyseniz ya da farklı bir VPC ağı kullanıyorsanız mutlaka belirtmeniz 
  gerekiyor.
* `--amazonec2-iam-instance-profile`: Makineki container’lar aracılığıyla AWS üstündeki diğer kaynaklara (örneğin ben 
  EC2 etiketlerini okumak için kullanıyorum) gizli anahtarlarınızı vermeden ulaşabilmek için kullanabilirsiniz.

#### Docker Machine İpuçları 💡

* Docker Machine, açtığı makinelere ait tüm verileri ve oluşturduğu SSL anahtarlarını `~/.docker/machine` dizinine 
  yazar. Bu dizine erişiminizi bir şekilde kaybederseniz, yarattığınız makinelere erişiminizi de kaybedersiniz. Ben 
  çözüm olarak bu dizini Google Drive’a taşıyıp `MACHINE_STORAGE_PATH` çevresel değişkenini Google Drive’daki dizini 
  gösterecek şekilde ayarladım.
* Docker Machine ile bulut ortamında makine açıyorsanız çok fazla parametre kullanmanız gerekiyor. Bu parametreleri 
  sıkça kullanıyorsanız çevresel değişken karşılıklarını tanımlayarak öntanımlı hale getirebilirsiniz. Örneğin AWS 
  hesap anahtarınızı (access key) `AWS_ACCESS_KEY_ID` değişkeni üstünden, kullandığınız imajı da `AWS_AMI` üstünden 
  tanımlayabilirsiniz. Bu tür başka ne değişkenler olduğunu görmek için `docker-machine create -d amazonec2` (farklı 
  bulut ortamları için farklı sürücü adı verebilirsiniz) komutunu verebilirsiniz.
* Docker Machine’i bulut ortamında kullanmayı düşünüyorsanız ve servis keşfi (service discovery) ihtiyaçlarınız için 
  de Docker’ı kullanmayı düşünüyorsanız, TLS sizin için bir problem oluşturabilir. Bu senaryoda yönetici makineler 
  üstünde TLS’i kapatabilir ya da Docker Machine kullanmayabilirsiniz. Benim böyle ihtiyaçlarım olduğundan 
  kurulumlarımı tektipleştirmek amacıyla kapsamlı bir betik yazdım.

---

### Docker Swarm Nedir?

{{< figure src="docker_version_dialog.png" caption="Bu yazıyı yazdığım sırada Docker CE 17.09.0-ce-mac35 (19611) var." >}}

Swarm, yönetici (master) ve yönetilen (worker) adı verilen makinelerin oluşturduğu bir ağdır (cluster). Bir Swarm ağı 
oluşturduğunuzda aslında bu ağda en az bir adet yönetici makine vardır ve yönetilenler bu ağa katılırlar. Herhangi bir 
anda, herhangi bir yönetilen makine, yönetici olarak atanabilir. Ancak ağda bağlı bulunan makineler, ağ ve DNS 
tanımları, çalışan servislerin kayıtları vb. tüm bilgiler (kısaca makine topluluğunun o anki durumu) yalnızca 
yöneticilerde tutulur ve bu bilgilere yalnızca yöneticiler üstünden ulaşılabilir. Son olarak Swarm yaratmak ya da 
mevcut bir Swarm ağına dahil olmak için Docker (≥ 1.12) kurulu olması yeterlidir. Swarm için birden fazla makineye 
ihtiyacım olduğundan burada anlattığım her şeyi Docker Machine ve Virtualbox aracılığıyla yarattığım sanal makineler 
üstünde göstereceğim.

Yazının geri kalanını benimle birlikte takip edebilmek için aşağıdaki 3 sanal makineyi yaratın:

```
docker-machine create -d virtualbox \
    --engine-label role=mgr \
    mgr1

docker-machine create -d virtualbox \
    --engine-label role=node \
    n1

docker-machine create -d virtualbox \
    --engine-label role=node \
    n2
```

`role` etiketiyle makineleri ikiye ayırdık. Deneme yapmamız nedeniyle yalnızca 1 yönetici (`role=mgr`) ve 2 yönetilen 
(`role=node`) makinemiz var. Gerçek ortamda ise minimum üç (tekil numara olması) yöneticiniz olması tavsiye ediliyor. 
Her yönetici, aynı zamanda yönetilen de olabiliyor. Yani yönetici makineleriniz, ağın durumunu tutmakla birlikte üstüne 
atacağınız bir kaç container’ı da çalıştırmaktan geri kalmayacaktır. 🙂

Makinelerin hepsini oluşturduktan sonra şöyle bir şey görmeliyiz:

{{< figure src="swarm_vm_yaratimi.png" >}}

Makinelerimiz hazır olduğuna göre, yöneticiye bağlanıp Swarm ağımızı yaratmaya başlayabiliriz:

```
$ eval $(docker-machine env mgr1)

$ docker swarm init --advertise-addr $(dm ip mgr1)
Swarm initialized: current node (xwpzchdnz1fl1xq2shalhxexq) is now a manager.

To add a worker to this swarm, run the following command:

docker swarm join --token SWMTKN-1–1yavlpsjjd0xx6wujmngq6tvjcrpin5j3zm6kv4cwcyp2y1gad-04trkq963fymb0541nzbdkpbm 192.168.99.101:2377

To add a manager to this swarm, run ‘docker swarm join-token manager’ and follow the instructions.
```

`docker swarm init` komutunu verdiğinizde mgr1 makinesinde Swarm ağınızı yaratmış bulunuyorsunuz. Bu makine üstünde 
`docker info` komutunu verirseniz şöyle bir şey görmelisiniz:

```
$ docker info
...
Swarm: active
NodeID: xwpzchdnz1fl1xq2shalhxexq
Is Manager: true
ClusterID: 53x1z42eir65p7gvw1nc5utuy
Managers: 1
Nodes: 1
...
```

Şimdi diğer makineleri yeni Swarm ağımıza bağlayalım:

```
$ eval $(docker-machine env n1)

docker swarm join — token SWMTKN-1–1yavlpsjjd0xx6wujmngq6tvjcrpin5j3zm6kv4cwcyp2y1gad-04trkq963fymb0541nzbdkpbm 192.168.99.101:2377 ⏎
This node joined a swarm as a worker.

$ eval $(docker-machine env n2)

docker swarm join — token SWMTKN-1–1yavlpsjjd0xx6wujmngq6tvjcrpin5j3zm6kv4cwcyp2y1gad-04trkq963fymb0541nzbdkpbm 192.168.99.101:2377 ⏎
This node joined a swarm as a worker.
```

`mgr1`'e geri gidip Swarm ağımıza bir bakalım:

{{< figure src="swarm_node_list.png" caption="`docker node ls` komutuyla yönetici makinenin bildiği tüm makineleri listeleyebilirsiniz." >}}

Artık kullanmaya hazır bir Swarm ağımız var! Devam etmeden önce Swarm terminolojisinden biraz bahsetmekte fayda var.

#### Docker Swarm Terminolojisi

* **Config**: Container’larınıza ait yapılandırma dosyaları ya da dışarıdan verebileceğiniz çeşitli amaçlı dosyaları 
  Docker Config aracılığıyla verebilirsiniz. Serinin ileriki bölümlerinde bu özelliği kullanıyor olacağız. 
  Tanımladığınız tüm dosyalar (config’ler), Swarm ağı genelinde yalnızca onay verdiğiniz makineler tarafından 
  erişilebilir durumda olacaktır.
* **Secret**: Herhangi bir amaçla kullandığınız ve gizli kalması gerekebilecek şifre, makine adresi, kullanıcı adı vb. 
  bilgileri Docker Secret aracılığıyla güvenli bir şekilde saklayabilirsiniz. Tanımladığınız tüm sırlar (secret’lar), 
  Swarm ağı genelinde yalnızca onay verdiğiniz makineler tarafından erişilebilir durumda olacaktır.
* **Volume**: Swarm kullanırken de tıpkı kendi makinenizde yapabildiğiniz gibi dışarıdan disk alanları 
  bağlayabilirsiniz. Bunu yine ev sahibi makine aracılığıyla yapabileceğiniz gibi, eklentiler (plugins) aracılığıyla 
  da yapabilirsiniz.
* **Network**: Swarm kullanmayı düşünüyorsanız, bu konu, bilmeniz gerekenlerin başında geliyor. Swarm’daki servis 
  keşfi, Swarm’la birlikte yaratılan alt ağlara (ve bunlara bağlı IP havuzları) ve servislerle oluşturulan DNS 
  kayıtlarına dayanıyor. Swarm’ı anlatırken bu konuya da özel olarak değiniyor olacağım.
* **Service**: Aynı container’dan bir veya daha fazlasının, ayarlarıyla birlikte gruplanmasına servis adı veriliyor. 
  Örneğin bir MySQL container’ınız varsa; bu container’dan kaç tane çalışacağını, hangi makinelere, hangi kurallarla 
  yerleştirileceğini, kullanılacak disk alanlarını, dışarıya açılacak bağlantı noktalarını, çevresel değişkenlerini ve 
  daha bir çok ayarını servis içerisinde tanımlayabiliyoruz.
* **Stack**: Servislerin, ağların ve disk alanlarının, yapılandırma dosyaları ve sır tanımlarının oluşturduğu daha 
  büyük gruba stack diyoruz. Örneğin, MySQL veritabanıyla konuşan bir uygulamanız varsa; uygulamanızı ve veritabanını 
  bir stack içerisinde tanımlayıp rahatlıkla yönetebilirsiniz. Stack yardımıyla saniyeler içerisinde uygulamanızı 
  yayına alabilir, kaldırabilir ya da aşağı/yukarı ölçekleyebilirsiniz.

#### Docker Swarm Demo #1

İlk denememizi basit tutalım. `tutum/hello-world` imajından 2 tane ayağa kaldırarak, Swarm’ın basitçe nasıl çalıştığını 
görelim:

```
docker service create -d --name helloworld \
    --constraint engine.labels.role==node \
    -p 80:80 \
    --replicas 2 \
    tutum/hello-world
```

Yukarıdaki komutla; `tutum/hello-world` servisini, yalnızca `node` rolündeki makinelere, toplamda 2 container olacak 
ve 80. bağlantı noktasını dışarıya açacak şekilde "dağıtıyoruz" (schedule). Bu komutu çalıştırdığınızda servise ait 
tanımlayıcıyı (Service ID) dönecektir. Dilerseniz bu tanımlayıcıyı ya da servisin ismini vererek sorgulama 
yapabilirsiniz:

{{< figure src="docker_service_komut_ciktilari.png" caption="`docker service` komutlarıyla \"deploy\" ettiğimiz servislerimizi, çalıştıkları makineler ve durum bilgileriyle görebiliyoruz." >}}

Ben makineleri Virtualbox’da yarattığımda aldığım IP’ler şöyleymiş:

* *mgr1*: 192.168.99.101
* *n1*: 192.168.99.102
* *n2*: 192.168.99.103

Yeni servisimizi test edelim mi? 🤞🏻

{{< figure src="servis_tarayici_testi.png" >}}

Hangi makineye istek attığımı farkettiniz mi? 192.168.99.**101**! Yani `mgr1`! E hani sadece rolü `node` olan 
makinelere yerleştirmiştik servisi? 😳 Şimdi arka arkaya defalarca kez sayfayı yenileyin. "My hostname is" ifadesinin 
karşısındaki tanımlayıcının sürekli değiştiğini göreceksiniz. Aynı IP’ye istek atıyoruz ama farklı cevaplar alıyoruz. 
Servisimiz bir de yük dengeleme yapıyor?! 😮

Bir üstteki ekran görüntüsünde açıkça görüldüğü gibi; aslında servislerimizden 2 adet var ve yalnızca rolü `node` olan 
`n1` ve `n2` makinelerine yerleştirilmiş durumda. Peki nasıl oluyor da `mgr1` makinesine istek atınca cevap alıyoruz? 
Cevap: **ingress** ağı! Docker 1.12+ ile gelen bu özellik sayesinde eğer bir servis, dışarı herhangi bir bağlantı 
noktası açarsa, bu bağlantı noktası tüm makinelerde açılır ve gelen istekler hangi makineye gelirse gelsin Swarm 
üzerinde o servisi çalıştıran makinelere yönlendirilir. Etkileyici, değil mi? 👏🏻👏🏻👏🏻

{{< figure src="swarm_cluster_semasi.jpeg" caption="**ingress** ağı sayesinde uygulamamıza her makine üstünden erişilebiliyor! 👍🏻" >}}

Üstteki diagram’da, tüm VM’lerin üstünde bir yük dengeleyici (LB) olduğunu varsayalım. Bir şekilde Swarm içerisindeki 
tüm makinelerin adresini LB’e ekleyebilirsek; tek bir noktadan uygulamamıza ölçeklenebilir bir şekilde ulaşabilir hale 
gelmiş oluyoruz. Diyelim ki; uygulamamız bu şekilde çalışırken çok fazla istek gelmeye başladı ve birer container’a 
daha ihtiyacımız var. Tek yapmamız gereken:

{{< figure src="swarm_scale_ps_ciktisi.png" >}}

Bir şey dikkatinizi çekti mi? Yalnızca 2 `node` makinemiz var ve bu nedenle aynı servisten her makinede artık iki adet 
çalışmaya başladı. Peki ama 80. bağlantı noktasını hala nasıl dinliyoruz? Sürekli istek atarsanız, yukarıdaki ekran 
görüntüsünün de teyid ettiği şekilde, 4 tane container’ın da başarılı şekilde çalıştığını göreceksiniz.

Cevabı aslında yukarıdaki diyagram’da! Ingress ağı her zaman mevcut ve herhangi bir ayar yapmanıza gerek kalmaksızın, 
servisleriniz için başlatılan her container’a bu ağın IP havuzundan farklı bir adres veriliyor. Swarm içerisinde 
çalışan yük dengeleyiciler, her makinede dinlenen 80. bağlantı noktasının, hangi container’lara yönlendirileceğini 
yaptığınız servis tanımından dolayı biliyorlar ve otomatik olarak istekleri yönlendiriyorlar!

`n1` ya da `n2`'ye bağlanıp container'ları rastgele öldürmeyi deneyin. Swarm, otomatik olarak yeni container'lar 
başlatacak ve ölçeklenebilirlik için ayarladığınız "minimum 4 container olsun" kuralını sağlamaya devam edecektir. 🎉

Servisinize ait imajı (örneğin uygulamanızın yeni sürümü çıktığında), çevresel değişkenleri, yapılandırma ya da sır 
dosyalarını, yerleşim ayarlarını ve diğer pek çok ayarı, servisinizi kapatmak zorunda kalmadan ya da herhangi bir 
servis dışı durum oluşmadan güncelleyebilirsiniz:

```
docker service update -d \
    --env-add server.port=8080
    --label-add foo=bar \
    helloworld
```

Değiştirebileceğiniz ayarlarla ilgili daha detaylı bilgi almak için;

```
docker service update --help
```

komutunu kullanabilirsiniz. Yaptığınız değişikliklerde bir problem oluşması halinde bir önceki kararlı duruma geri 
dönmek için

```
docker service rollback helloworld
```

komutunu kullanabilirsiniz.

Servislerin güçlü özelliklerinden bir diğeri ise tüm container’ların log kayıtlarını bir arada görme şansı vermesi:

```
docker service logs --tail 10 -f helloworld
```

Kişisel fikrimi sorarsanız; bu özellik oldukça işe yarıyor olmakla beraber gerçek ortamda çalışan servisler için pek 
yeterli olmuyor. Birden fazla makinenin kayıtlarını bir araya topladığınızdan birbirine girmiş karman çorman kayıtlarla 
karşılaşabiliyorsunuz. Ancak Docker’ın log sürücüleri üstünden bu kayıtları 
[logstash](https://www.elastic.co/products/logstash) vb. servislerle paylaşabildiğini düşünürsek çok da mühim değil.

Küçük ve fazla bağımlılıkları olmayan projelerinizi yalnızca `docker service` komutlarıyla sunuculara dağıtabilir ve 
ölçekleyebilirsiniz. Daha büyük ölçekli projeler için yapılması gerekenleri serinin bir sonraki yazısında ele alacağım.

Bilgisayarınızın kaynaklarını boş yere harcamamak için oluşturduğunuz servisi;

```
docker service rm helloworld
```

komutuyla, Docker Makine ile yarattığınız VM’leri ise;

```
docker-machine rm mgr1 n1 n2
```

komutuyla silebilirsiniz.

---

Bu bölümünün de sonuna geldik. Bir sonraki bölüm olan "Docker Serisi #5 — Docker Machine & Swarm Bölüm 2"'de görüşmek 
dileğiyle!

Gidişâta göre bu planda zaman zaman değişiklikler yapacak olsam da serinin tüm bölümlerinin planına 
[şuradan](https://www.evernote.com/l/AB7CctYtJkpMUJsae1_3FgzIXgMY5MvFQhU) ulaşabilirsiniz.
