---
title: "Docker Serisi #4 -- Docker Compose"
date: 2017-03-20
slug: docker-serisi-4
draft: true
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

TODO
