---
title: Docker'laştıramadıklarımızdan mısınız?
date: 2016-06-21
slug: dockerlastiramadiklarimizdanmisiniz
cover:
    image: docker.png
tags:
    - docker
    - linux
    - macos
    - raptiye
    - blog
    - bulut
    - günlük
    - sunucu
---

Bugün itibarıyla kendimi bildim bileli açık tutmak için elimden geleni yaptığım, defalarca kez 
[farklı](https://github.com/tunix/raptiye-django) [teknolojilerle](https://github.com/tunix/raptiye) baştan yazdığım 
raptiye’yi kapatma kararı aldım. Bundan sonraki tüm yazılarımı Medium üstünden sürdüreceğim. Peki raptiye’yi neden 
kapattım? Çok kısa özetlersem;

1. İlk başta yönetim panelinin iPad’de neredeyse çalışmıyor olmasından dolayı motivasyonumu kaybettim. Markdown desteği 
  getirsem de bir türlü istediğim seviyeye getiremedim.
2. İçeriği zenginleştirmek için kullandığım görselleri [instagram](https://www.instagram.com/tunix/), flickr gibi 
  harici servislere yüklemiştim. flickr hesabımı kapattım, instagram ise CDN’inde değişiklikler yapmış. Her 2 sebepten 
  ötürü yazılarımda kullandığım görsellere artık ulaşılamıyor ve bu içeriğin kalitesini çok ciddi bir biçimde 
  düşürüyordu.
3. Google Analytics’e baktığımda bir kaç yazı haricinde trafiği yoktu ama ben her ay raptiye’yi yaşatmak adına $5 
  veriyordum. (tabii başka sebepleri de var bunun)
4. Eski yazılarımda bağlantı verdiğim sayısız dosya var ve sitenin yeniden yazılması esnasında yaptığım URL 
  yönlendirmelerini aynen korumam daha da uğraştırıcı olacaktı.
5. Siteyi statik içerik olacak şekilde son bir kez daha yazdım. Bu yeniden yazmaların asıl odaklanmam gereken yazma 
  eylemini ciddi sekteye uğrattığını, bende de bir takıntı haline geldiğini farkettim ve buna son vermeye karar verdim.
6. Ben raptiye’yi ilk yazdığımda WordPress’te etiket bulutu yapmak tam bir dertti. Şimdiyse bırakın etiket bulutuna 
  ihtiyaç olmasını, blog tutmak için sayısız araç var. Kasmaya ne gerek var?
7. Siteyi statik üretme veya docker’laştırmak bir çözüm gibi görünse de yukarda yazdığım sebeplerden ötürü çok zaman 
  aldığından kapatma kararı en mantıklı karar gibiydi.

### docker...

Uzun süredir hem şirkette, hem de kişisel projelerimde docker ile uğraşıyorum. Şirketteki deneyimlerimden kişisel 
projelerimde de faydalanmak istiyorum. Bu nedenle kişisel sunucularımı tek tek kapattım ve artık sadece Debian tabanlı 
docker makineleri kullanıyorum.

[Docker](https://www.docker.com/), yazılım ve teknoloji dünyasının şu aralar en sıcak konusu. Monolitik kod yazmaya 
alışmış biri için Docker’ı anlamak bir mesele. Bu nedenle bu konuda ayrı bir yazı serisi hazırlamayı düşünüyorum. 
Yakında ;)

Proje baş döndürücü bir hızla geliştiriliyor. Öyle ki; tam bir şeyi çözdüğünüzde yeni bir aracın varlığından haberdar 
oluyorsunuz; bu sefer onu öğrenirken yine karşınıza çıkan başka şeyleri öğrenmek durumunda kalıyorsunuz. Örneğin; 
overlay network adı verilen container’lar arası iletişim ağını okurken [Swarm](https://docs.docker.com/swarm/)’a, 
[consul](https://www.consul.io/)’e dalmak zorunda kalıyorsunuz ve daldan dala zıplamanız kaçınılmaz oluyor. :)

Bugünlerde devam eden [Docker Con 2016](http://2016.dockercon.com/)'da heyecan verici yenilikler ardı ardına 
açıklanıyor. Dün ilk günüydü ve docker 1.12 ile gelen, makine yönetimini (orchestration) çekirdeğe ekleyen çok önemli 
yeniliklerden [bahsettiler](https://blog.docker.com/2016/06/docker-1-12-built-in-orchestration/). Açıklamayı okurken 
15 senedir Linux’da bulunup benim hiç duymadığım [Linux IPVS](http://www.linuxvirtualserver.org/software/ipvs.html)’i 
duyma imkanım oldu örneğin. :)

DigitalOcean üstünde minimum masraflara sahip bir yapı kurmaya çalışıyorum ve 
[Docker 1.12](http://docs.docker.com/release-notes/) nihayet ihtiyacım olan şeyleri sunuyor gibi. brew’e düşmesini ve 
docker-machine ile kullanabilmeyi bekliyorum şimdilik. Bu konudaki detayları da yukarda bahsettiğim yazı serisinde 
işliyor olacağım.
