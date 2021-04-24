---
title: macOS'te Ekran Görüntüsü Almak
date: 2016-10-03
slug: macoste-ekran-görüntüsü-almak
tags:
    - macos
    - ipucu
    - üretkenlik
---

Günlük yazısı yazarken ya da herhangi bir sebepten macOS’te ekran görüntüsü çekme ihtiyacı duydunuz mu? Bu iş için 
minik uygulamalar kullanıyorsanız artık onlardan kurtulmanın zamanı geldi! Bu yazıda size macOS’te oldukça pratik 
ekran görüntüsü çekme yöntemlerinden bahsedeceğim.

---

Öncelikle tuş kısaltmalarından bahsedeyim:

### CMD: Command Tuşu

Klavyenizde boşluk tuşunun solundaki ve sağındaki `⌘ ` işaretiyle gösterilen tuş.

### CTRL: Control Tuşu

Klavyenizde üstünde `kntrl` ya da `ctrl` yazan tuş.

### SHIFT

Klavyenizin solunda ve sağında `⇧` işaretiyle gösterilen tuş.

---

### Tüm Ekran(lar)ın Görüntüsünü Çekin

`CMD+SHIFT+3` tuşuna basın. O an ekranınızda her ne varsa masaüstünüze PNG biçiminde kaydedilecektir. Birden fazla 
monitör kullanıyorsanız her monitöre ait ekran görüntüsü ayrı birer dosya olarak kaydedilecektir.

### Ekranın İstediğiniz Bölümünü Çekin

`CMD+SHIFT+4` tuşuna basın. Fare imleciniz hedef işaretine dönecek ve yanında o anda ekranda bulunduğunuz koordinatlar 
görünecektir. Ekranın istediğiniz yerindeyken fareyi basılı tutun ve istediğiniz yere kadar çekin.

{{< figure src="secerek_ekran_goruntusu_almak.gif" caption="CMD+SHIFT+4 ile ekranın sadece istediğiniz bölümünün görüntüsünü çekebilirsiniz." >}}

### Ekran Görüntüsünü Panoya Yapıştırın

Bazen çektiğiniz ekran görüntüsünü masaüstündeki bir dosyaya kaydetmektense istediğiniz programa doğrudan yapıştırmak 
daha iyi olabilir. Bu durumda tüm ekranın görüntüsünü `CMD+SHIFT+CTRL+3` ile, ekranın yalnızca belli bir bölümünüyse 
`CMD+SHIFT+CTRL+4` ile çekebilirsiniz. Çektiğiniz ekran görüntüsünü yapıştırmak için yapıştıracağınız programa geçip 
`CMD+V` tuşlarına kullanabilirsiniz.

### Sadece Bir Uygulamanın Görüntüsünü Çekin

Bunu yapmak için ekranın sadece bir bölümünü çekecekmiş gibi `CMD+SHIFT+4` tuşlarına basın. İmleciniz hedef işaretine 
döndükten sonra boşluk tuşuna basın. İmleciniz bu kez fotoğraf makinesine dönmeli. Şimdi imlecinizle istediğiniz 
pencerenin üstüne gelin. Pencere grimtrak bir renge bürünecektir. Tıkladığınız pencerenin görüntüsü masaüstüne 
kaydedilecektir. Üstelik bunu yaparken pencereye gölge vb. eklemeyi de ihmal etmiyor macOS. 😉

{{< figure src="pencere_ekran_goruntusu.png" caption="[dotfiles depomdaki](https://github.com/tunix/dotfiles) bootstrap.sh dosyasını MacVim’de düzenlerken…" >}}

Bu aşamada eğer dosyaya kaydetmek yerine panoya kaydedip yapıştırmak istiyorsanız yukarda bahsettiğim gibi 
`CMD+SHIFT+CTRL+4` tuşuna, sonra da boşluk tuşuna basarak yapabilirsiniz.

---

### Güncelleme #1

```
defaults write com.apple.screencapture location ~/Documents/Screenshots
```

komutuyla ekran görüntülerin yazıldığı dizini değiştirebilirsiniz. İpucu için [firatov](https://twitter.com/firatov)’a 
teşekkürler!

---

Ekran görüntüsü almayla ilgili bildiğiniz başka numaralar varsa yorum olarak yazabilirseniz yazıya sizin adınızla 
ekleyebilirim. 👍🏻
