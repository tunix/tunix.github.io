---
title: About System76 Lemur Pro
date: 2021-05-16T01:30:00+03:00
slug: system76-lemur-pro
cover:
    image: system76.png
tags:
    - computer
    - system76
    - lemur pro
    - linux
    - open source
---

I was using mostly Mac computers from companies I worked for for a long time. Frankly, I can't even remember the last time I had my own computer, when and for how much I sold it.

There was a time when we built our own desktop computers and computer prices were reasonable. Macs were still expensive, but computer prices were never out of reach . I'm seriously worried about the prices we have nowadays. Especially during the pandemic we are going through, in a period when even education is carried out on the internet, it has become very difficult for students and new grads to access a good computer. Moreover, I am not only talking about the financial situation; we are living in a period in which manufacturers either do not sell or sell very limited models due to price increases. It is very difficult to find performant devices in the market. (at least in Turkey)

{{< figure src="ipad.jpg" caption="2012. When I wrote code in SSH sessions, using an iPad.." >}}

Until early 2020, I used to have a Macbook Pro (2014 -- provided by my employer) with 8 GB of memory. Obviously it wasn't enough for the high demands of my daily work at [dataroid](https://www.dataroid.com/) where I start many containers at the same time and test code changes. So occasionally, I had to use certain dependencies like Kafka, ElasticSearch via the sandbox servers that we had inside company premises.

[commencis](https://www.commencis.com/) decided to refresh the aging computers (excluding some teams with certain needs) with [Dell Precision 5530](https://www.dell.com/en-us/work/shop/dell-laptops-and-notebooks/precision-5530-mobile-workstation/spd/precision-15-5530-laptop)'s. With an i7 series Intel CPU, multiple GPU's (Intel + nVIDIA) and 64 GB's of RAM, it solved most of my issues. Of course, such a change also meant making a choice about an operating system. Thankfully though, it was a fully Linux compatible laptop and with the approval of IT, I was able to choose [Ubuntu](https://ubuntu.com/). I started with 18.04 LTS, continuing with 20.10. 🤙

I'm extremely pleased with the point that the desktop Linux experience has reached since 2010. Significant progress has been made in terms of performance, stability, hardware support and application diversity. Not only that but platforms such as Steam has opened up [a huge library of Windows games](https://www.protondb.com/) being playable on Linux without any issues. Some games are reported to work even faster than Windows. 🤯

I strongly recommend you to take a look at [r/unixporn](https://www.reddit.com/r/unixporn/) if you have time. Here's a how-to video of making [GNOME desktop](https://www.gnome.org/) to look like macOS Big Sur:

{{< youtube jT1RnyGJRMU >}}

Since 2017, due to the increase in exchange rates, I started to think that it would be good to have my own computer again and started researching. I had the following models on my list:

* [Dell XPS 9310](https://www.dell.com/tr/sletmeler/p/xps-13-9310-laptop/pd)
* [System76 Lemur Pro](https://system76.com/laptops/lemur)
* [Starlabs Starbook Mk V](https://starlabs.systems/pages/starbook)
* [TUXEDO InfinityBook S 14 - Gen 6](https://www.tuxedocomputers.com/en/Linux-Hardware/Linux-Notebooks/10-14-inch/TUXEDO-InfinityBook-S-14-v6.tuxedo)
* [Monster Huma H4 V4.1.2](https://www.monsternotebook.com.tr/huma/monster-huma-h4-v4-1-2/)
* [Slimbook Pro X](https://slimbook.es/en/pro-x-en)

Before I write my thoughts about the models, it is useful to specify my criterias:

-   Long battery life (preferably I should be able to get through the whole day)
-   Lightness (< 1.5 kg)
-   World-class Linux support
-   13-14 inches of screen size
-   Having a quality touchpad and keyboard
-   (Preferably) on AMD platform; if not, be on Intel Xe platform
-   (Preferably) Fully or mostly open source (ex: coreboot support)

Now let's see what we have…

### Monster Huma H4

Despite the fact that Monster is the most accessible vendor of all (afterall it's a Turkish computer manifacturer), it wasn't even an option for me as they have no support (or any intention at all) for Linux. I had the opportunity to visit their store in İzmir and although they use [Clevo](http://clevo.tw/) chassis', I must say that this is a very nice looking and light computer.

### Dell XPS 13

Dell XPS 13, which has not lost the first place in the portability and thinness category for years, was the model that has been on my radar for the longest time. For quite some time, they've been running an exciting project with Canonical called [Project Sputnik .](https://bartongeorge.io/2020/01/01/introducing-the-2020-xps-13-developer-edition-this-one-goes-to-32/) For this reason, I wanted to buy a Developer Edition, but this model is not sold in Turkey. In fact, the current series of the Dell XPS 13 model was not on sale in our country for quite a long time. Until today, I never came across a Dell in the stores in the shopping malls. [I think](https://twitter.com/tunix/status/1351876496726614021) Dell focuses more on the corporate side in Turkey and doesn't care about the rest .

{{< tweet 1351876496726614021 >}}

In 2020 and 2021, computer manufacturers such as Dell and Lenovo have made agreements with various Linux distributors and made many announcements that their computers can be purchased from their online stores with Fedora and Ubuntu, just like computers with Windows. However, this unfortunately did not happen.

Models with Ubuntu on Dell's US pages are sometimes easily accessible, sometimes quite difficult. The most annoying part of the it is that different configurations in different countries and vary a lot. (you may not find it on your next visit) The Developer Edition is almost impossible to get outside of the USA.

### Starlabs Starbook Mk V

Except for Dell, all the models I consider definitely offer a chassis of [Clevo with different configurations.](http://clevo.tw/) Starlabs, on the other hand, follows [a different approach](https://starlabs.systems/pages/about-us) at this point. The company, located in UK, does ship to Turkey and with more affordable prices than others.

[The models before the Starbook Mk V](https://starlabs.systems/pages/starbook) , which was launched this month , were technically inadequate. I think this model is a good alternative to System76 Lemur Pro. If I hadn't bought the Lemur Pro, I would probably buy this computer.

### TUXEDO InfinityBook S 14

Based in Germany, [TUXEDO](https://www.tuxedocomputers.com/en) is one of the very well known players of the market. There are many different models, but they all use [Clevo](https://translate.google.com/website?sl=tr&tl=en&hl=en&client=webapp&u=http://clevo.tw/) chassis'. Earlier, many of these did not appeal to me as they looked rather bulky. [The model I mentioned above](https://www.tuxedocomputers.com/en/Linux-Hardware/Linux-Notebooks/10-14-inch/TUXEDO-InfinityBook-S-14-v6.tuxedo) uses the same chassis as the Lemur Pro. They manufacture a lot of different models that may appeal to many people with different needs. They even have models with AMD Ryzen platform.

TUXEDO has a few important advantages in my opinion:

-   They can send many models with Turkish keyboard layout.
-   Including my favorite model; an LTE module can be added to some models
-   They can ship to many countries including Turkey.

After System76 and Starlabs, I always had an eye on TUXEDO. I think they announced the models with the Intel Iris XE platform a little late, and I think the biggest shortcomings compared to System76 and Starlabs are the absence of coreboot and the fact that it does not provide much value compared to its competitors.

### Slimbook Pro X

Spanish [Slimbook](https://slimbook.es/en/) is again a manufacturer that I've been watching for a while, using the same (Clevo) chassis' as Monster. Although models such as the KDE Slimbook which comes with an AMD Ryzen series CPU and GPU made a lot of excitement, the model I thought was [Pro X.](https://slimbook.es/en/pro-x-en) I had to ignore this model, both because the lion in my heart was System76 and the lack of reviews was worrying at the time I was looking at it.

---

Before moving on to System76, there are one or two last things I need to address. I tried to do my research based on only 1 model of the manufacturers that met my criteria. For each model, I scanned the reviews and comments on Youtube, various websites and reddit in detail. I took note of the downsides, and tried to figure out if the manufacturers had fixed these issues.

For example; there are so many reviews on the internet for a computer like the Dell XPS 13 that you'll get bored. However, almost all of these reviews were made with Windows, and the Developer Edition review is either non-existent or quite old. Similarly; reviews of the computer models I have listed above are also very limited or old. Especially comparisons with each other are much, much rare.

For Lemur Pro, my favorite and most useful review belongs to [Steve](https://www.youtube.com/user/SteveM0732/videos) .

Other resources I have used are:

* https://www.reddit.com/r/System76/
* https://partofthething.com/thoughts/hands-on-with-the-new-system-76-lemur-pro-laptop/
* https://www.youtube.com/watch?v=vv1w78YRrNk
* https://moddingtheworld.com/review-system76s-lemur-pro/

---

### System76

[System76](https://system76.com) is a startup based in the USA (Denver/Colarado) whose primary priority is to produce Linux desktop, laptop and server computers. Among all the manufacturers I have mentioned, I can count coreboot support, battery performance of Lemur Pro and Thelio series among the main reasons why it is the most popular company. In addition, as of yesterday, they became a [keyboard]https://system76.com/accessories/launch) manufacturer as well! With the Ubuntu-based operating system called [Pop!_OS](https://pop.system76.com/) , they managed to reach a considerable user base. (I hope to cover this topic in a separate article)

In particular, Lemur Pro (after the last hardware + software updates) meets almost all the criterias I mentioned at the beginning of the article. And also; I must say that the vision and values that System76 stands for as a company and the methods they use especially in laptop production have impressed me a lot.

#### Why System76?

Because;

- They prioritize Linux on all their computers.
* [Coreboot](https://alperkan.at/2021/05/system76-lemur-pro/#coreboot--ec-firmware) is installed by default on all laptops.
- You get direct support for any problem you may have with the computer. They can even [fix your problem by updating the firmware within a few hours](https://www.forbes.com/sites/jasonevangelho/2020/06/07/system76-lemur-pro-owners-are-about-to-get-a-free-performance-boost/?sh=2f4922971129) .
- The close integration between the OS (Pop!_OS) & hardware which I've always dreamed of for Linux
- In the long term, they have a vision to publish the schematics of all their computers and hardware documents with GPLv3, which anyone can print, produce and modify. The design of the [Launch keyboard](https://system76.com/accessories/launch) they started to manufacture is released under GPLv3 license and [is available](https://github.com/system76/) at Github.

#### Tamir Hakkı (Right to Repair)

{{< tweet 1390599847506497542 >}}

Most of the new generation computers have a problem that we as end users are not very aware of. The new generation of computers is getting lighter and thinner. Unfortunately, we do not give much thought to what is given up in order to reach this state.

Due to this trend heavily promoted by Apple, many critical components are soldered to the motherboard of the computer. In this way; in addition to saving space and weight, in cases where repair is required, directly replacing the motherboard not only saves money, but also makes it easy for production.

Inside the flood of tweets above, I also mention [TBW](https://www.tech-worm.com/tbw-total-bytes-written-ssd-nedir/) (Total Bytes Written) which I recently found out about. TBW, basically determines the lifetime of your SSD. It starts to fail after this value reached and your [only option](https://medium.com/codex/the-shocking-discovery-of-apple-m1-ssd-that-you-need-to-know-a3a5415df1db) is to replace the motherboard. Don't you ever say that you wouldn't reach this value! The author of the article may look as if he's misusing his computer (for what it's designed for) but it's irrelevant and anyone can face this issue.

It wouldn't be wrong to assume that soldering everything on the motherboard is based on the same environmental arguments as removing chargers from the boxes of new phones. You don't need to sacrifice in order to have a lighter and thinner laptop! Being environmentally friendly and supportive of customer rights at the same time have been proven sustainable & profitable by the [Framework](https://frame.work/products/laptop-diy-edition) which is a very ambitious startup that was founded recently. I really wish the best of their success. In fact, if I haven't purchased the Lemur Pro, I'd seriously consider their [DIY Edition](https://frame.work/products/laptop-diy-edition).

{{< youtube fGle6z9KfZQ >}}

Let me share some of my notes (that really surprized me) of this amazing discussion between System76's [Jeremy Soller](https://twitter.com/jeremy_soller) and Louis Rossman:

* They design all their computers to last 10+ years and have positioned their entire business model around that.
- Asus, Dell, HP etc. many manufacturers rely on computer manufacturers in Taiwan. Computer chassis', motherboards compatible with them, and firmwares running on motherboards were produced by these companies, and in case of any problems, solutions are expected from these companies.
- System76 takes schematics of the devices from Clevo to develop open source firmware and share them with customers (if they ask for it).
- It's possible to purchase spare parts and do the repairs by yourself by following the [guides](https://support.system76.com/articles/service-manuals/) on their [website](https://tech-docs.system76.com/models/lemp10/repairs.html).
* Çoğu üretici için marjlar oldukça düşük: ~%5

I highly recommend you to listen this episode of [Linux 4 Everyone](https://www.linux4everyone.com/) podcast in which [Jason Evangelho](https://twitter.com/killyourfm) and [Jeremy Soller](https://twitter.com/jeremy_soller) discusses about this topic:

{{< rawhtml >}}
<iframe src="https://player.fireside.fm/v2/GTYFbp1j+ODGErxgQ?theme=dark" width="740" height="200" frameborder="0" scrolling="no"></iframe>
{{< /rawhtml >}}

{{< rawhtml >}}
<iframe src="https://player.fireside.fm/v2/GTYFbp1j+8cs3C4Mn?theme=dark" width="740" height="200" frameborder="0" scrolling="no"></iframe>
{{< /rawhtml >}}

There is currently a serious [lobbying activity](https://www.youtube.com/playlist?list=PLkVbIsAWN2lsmovRO20_gtfUfgWi-XnnT) in the USA on the Right to Repair . For now, they have not achieved great success, but it is useful to follow.

{{< tweet 1379480063159140352 >}}

#### coreboot & EC firmware

[coreboot](https://www.coreboot.org/) is an open source firmware that supports many architectures. It contains nothing but the code needed to start the computer and leaves the rest to the operating system level. This is why computers using coreboot are known for their fast boot.

The secondary firmware, called EC (Embedded Controller) firmware, manages some other important functions of the computer (fan curves, keyboard layout, etc.). The fact that these two are separate actually facilitates the separation of concerns and individual/model-specific customization.

Using [open source firmware](https://support.system76.com/articles/open-firmware-systems/), System76 claims that their computers run better and faster in terms of battery performance, fan operating curves, and overall performance compared to closed source firmware. If you look at the [GitHub page](https://github.com/system76/ec) of the EC firmware, you can see that they often receive PR's on certain topics, and all of these eventually lead to positive changes in the user's life. As an example, all Lemur Pro users now leverage the performance improvements which is reported by [Jason Evangelho](https://twitter.com/killyourfm) at the time he was working on a [review article for Forbes](https://www.forbes.com/sites/jasonevangelho/2020/06/07/system76-lemur-pro-owners-are-about-to-get-a-free-performance-boost/?sh=2f4922971129). He found out some shortcomings compared to other Linux laptop models and reported them to System76 engineers and they were fixed before the article was published!

{{< figure src="pgdnup.jpg" caption="the infamous PgUp & PgDn keys of Lemur Pro" >}}

Let me give an example from my experience. As you can see in the image above; unfortunately, Lemur Pro's `Page Up` & `Page Down` keys are pretty close to the arrow keys. Because of this situation, I was frequently pressing these keys while typing anything and was having silly problems. I rearranged these keys to act as as left and right arrow keys inside the EC code, following the instructions [on this page](https://github.com/system76/ec/blob/master/doc/keyboard-layout-customization.md), and made them behave as `PgUp` & `PgDn` only when the `Fn` key is pressed.

I'm aware of the risks of reflashing the firmware but it's really worth it to have such freedom and customizability. On the other hand, there's currently [a tool](https://system76.com/accessories/launch/download) for making such changes instantly without even flashing the firmware.

#### How did I buy it?

System76 currently ships to 64 [countries](https://system76.com/shipping). Unfortunately, Turkey is not among these countries. Turned out that, the trade agreements between the USA and Turkey do not allow the trade of computers. We have no problem with the UK and EU countries in this regard. I was surprised that we had problems with the USA, but I couldn't get enough information about the details of the issue.

The first solution that came to my mind was to send it to my uncle in UK and have him bring to Turkey somehow. Shipping from US to UK costs ~$120. I also wasn't aware that on top of this price, a tax of around 20% (VAT) is added upon entry to the UK. It was also unclear when I would be able to pick up the computer as the UK had closed its borders due to the pandemic. It may additionally get stuck at the customs of Turkey as well which led me to think of ways to handle this without incurring additional costs.

At this very point, I came across a site called [amerikapostam.com](https://amerikapostam.com/). To summarize; you forward the products you bought from the USA to the address they give you. You are informed separately of each incoming product. And whenever you want, you can have it repackaged (in order to reduce costs by shrinking their packaging) and send it to your address in Turkey. Of course, after paying the shipping and customs fees. 😊 If you have problems paying to sites in the USA, you can ask them to purchase on your behalf as well! You can access all these details on their website, and if you have any questions, they even have customer support on Whatsapp. I got fast and clear answers to all my questions on Whatsapp and decided to give it a shot after doing my research only to find out nothing but good comments on various sources.

I purchased the laptop directly from System76's website with my virtual (debit) card at [papara](https://www.papara.com/). Shortly after placing the order, I got a phone call and was asked to share the code of the expense on my card statement to confirm that I am the real owner of the card. After doing this, my order was confirmed and dispatched to the factory.

As if the effects of the pandemic isn't enough, it was the very early days of the global chip crisis so I decided to place my order asap. (it was the right decision btw as Lemur Pro's were out of stock soon after I placed my order) However I made the wrong choice for shipping to UK as the details I mentioned above were not yet clear to me. Thankfully, we quickly re-routed it to the address inside the US and System76 refunded ~$88 to my card.

The computer arrived at [amerikapostam.com](https://amerikapostam.com/) in about 2 weeks and I received an email confirming the device had arrived, including a picture of their measurements. At this stage, I had to make a choice for repackaging. The box System76 uses to ship the computer is designed to protect it pretty well against potential damages and it also serves well in case I need to send it back. I did not request repackaging as I could not afford it to get damaged on the way to Turkey. (If I did, the package with 13 LBS would drop to around ~3 LBS; the shipping price would also drop by 1/3)

As a result; The shipping ($75) + customs fee calculated by [amerikapostam.com](https://amerikapostam.com/) was ~$325. After a few hours I made the payment, I received a notification that the cargo was on its way for JFK airport. And it arrived exactly the day they said it would. The computer I ordered on April 7th arrived in the last week of April. Not only did I save money compared to shipping via the UK, since I send directly within the US, but I also avoided the delay I would experience due to the closed borders. I have to say that I am extremely satisfied with the service provided by [amerikapostam.com](https://amerikapostam.com/).

### Lemur Pro

{{< figure src="kutu.jpg" caption="I love the design of packaging of these computers -- they're designed to be reusable" >}}

At the beginning, I listed my criterias for choosing a computer. The computers given by my employer are usually 15" and quite heavy. That's why I prefer a 13-14" computer. To be honest I forgot how petite this form can be. 😊 Even though it is not very clear from the photos, all of my friends were really puzzled when they get the chance to weight it.

{{< figure src="dell_ile_karsilastirma.jpg" caption="Dell Precision 5530 and Lemur Pro stacked for a comparison" >}}

A 65W adapter comes out of the huge box, which is easy to carry around with the computer. Rightfully, there are heavy criticisms about the cable length which I overcame by purchasing a 3m cable while replacing the US plug. The computer can also be charged via USB-C, but the adapter that comes out of the box is of the barrel type. It provides a full charge in ~2-3 hours.

Apart from this, nothing comes out of the box except a screen wipe and a few stickers.

{{< figure src="lemur_kapali.jpg" >}}

The computer is around ~1 kg and has a plastic like surface similar to magnesium chassis'. I have to admit that from time to time I had to check my bag just to see if I had forgotten the computer while lifting it. 😊 I don't think it looks cheap/simple as some argue. On the contrary, it has a pretty nice feel.

The model I purchased has the following feature set:

* **OS:** Pop!_OS 20.10 (64-bit) (fully encrypted)
* **CPU:** 11th Gen Intel® Core i5-1135G7: Up to 4.20 GHz - 8MB Cache - 4 Cores - 8 Threads
* **RAM:** 40 GB DDR4 @ 3200 MHz
* **Disk:** 500 GB PCIe Gen3 Seq Read: 2400 MB/s, Seq Write: 1750 MB/s

{{< figure src="lemur_acik.jpg" >}}

As soon as I turned on the computer, the setup assistant greeted me. After a few steps such as language/keyboard selection and user creation, it instantly became ready to use and the first updates (including firmware) came as soon as it was open. I've done all the updates and it's been working just fine since day one.

Here are my general notes on the computer:

* On Dell I can see 3-4 hours max, even though I turn off the NVIDIA card. On this device, I can work all day without charging. (I haven't done the exact measurement yet)
* From time to time, depending on the work I do, I can hear the fan noise. My experience so far; it seems to be set to kick in quickly and shut down asap. The fan can kick in when the IDE is scanning code or starting a Windows VM (ievms). I can't say that it works for a very long time in the IDE, but it works non-stop in Windows VM. I have a general [problem](https://www.reddit.com/r/System76/comments/n9xgqo/bad_windows_experience_inside_virtualbox/) with the Windows VM, but it seems other people have different experiences. I will keep trying on this.
* As mentioned in all reviews; the computer speakers are not good unfortunately. I can't say that it is very suitable for listening to music as the treble is a bit high. Not bad for a meeting or watching something on Youtube.
* Touchpad works fine. Can navigate between workspaces with multiple fingers. I can't wait to try [GNOME 40](https://youtu.be/vK-SwsWnEmo).
* It has a 1M 720p camera and the image quality is good. I think there are also Windows Hello sensors on the device; I'm thinking of doing an experiment with [howdy](https://github.com/Boltgolt/howdy) at a convenient time . 🤞
* There are 5 steps for the keyboard lights and it does not go out by itself. If you don't need it, you have to turn it off. Since the device does not have an ambient light sensor, I guess there will not be a firmware fix for this issue.
* It has a FHD matte display. I can say it is more than enough and bright for me. In fact, I even had to install a [shell extension](https://extensions.gnome.org/extension/1625/soft-brightness/) for extra dimming as it stays a bit too bright at night.

{{< figure src="neofetch.png" caption="neofetch output (shell is `zsh`)" >}}

Finally; Here are my thoughts on Pop!_OS:

* Although it is an Ubuntu-based operating system, there are points where different preferences are made. For example it uses systemd-boot instead of GRUB. I am not well-versed in the subject to comment too much, but thanks to this preference, it was not affected by [the bug](https://www.omgubuntu.co.uk/2021/04/why-you-cant-upgrade-to-ubuntu-21-04-for-now) that caused the delay of the release of Ubuntu 21.04.
* In general, I have to say that it offers a leaner and faster experience than Ubuntu.
* A mod called Pop Shell, which puts window management in grids, has reshaped the way I work. I look forward to the [upcoming changes](https://youtu.be/ydRlDv0heAo) with COSMIC.
* Unlike Ubuntu, flatpak is preferred instead of snap packages. I had serious concerns about this, but the snap integration is pretty seamless. As of now, I seem to have installed 27 flatpaks and 22 snap packages. 😊 I'm thinking of preparing a separate article about Flatpak vs snap in time.

{{< youtube ydRlDv0heAo >}}

Lemur Pro cost me around ₺16k including shipping and customs. Unfortunately, many devices with similar features are sold in the ₺20-30k range. That's all I'm going to write about the device for now. If you have questions, please feel free to contact me. And stay tuned for the next blog post as a long-term review! 🤞