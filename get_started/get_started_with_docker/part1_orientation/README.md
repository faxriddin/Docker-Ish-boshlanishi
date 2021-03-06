# Docker-Ish-boshlanishi

Xush kelibsiz! Biz sizni Docker o'rhganishni xohlaganingizdan xursandmiz.

Docker bilan birgalikda ish boshlash.
[Qo'llanmani](https://docs.docker.com/get-started/) o'zbek tilidagi tarjimasi.

Bu qo'llanma texnik bo'lmagan faqatgina Dockerni o'rganishga qiziqishi bo'lgan foydalanuvchilarga mo'ljallangan. Ushbu qo'llanmadan foydalanib, siz Docker asoslarini ma'lum bir topshiriqlarni bajargan holatda o'rganasiz. Siz qanday:

    1. O'zingizning Docker muhitingizni o'rnatishni (ushbu sahifada)
    2. Image (obrazni)ni  build(yasash) va uni run (qilish) qilish. 
    1. Ilovangizni mashtablash orqali ko'p konteynerlarni ishga tushirishni o'rganish
    2. Ilovangizni klasterlar orasida taqsimlash
    3. Ma'lumotlar bazasini qo'shish orqali xizmatlarni yig'ish 
    4. Ilovangizni production serverga joylang. (Deploy)

## Docker tushunchalari

Docker bu developerlar va sisadminlar uchun bo'lib, ilovalarni kontayner asosida yaratish (develop), tarqatish(deploy) va ishga tushirish(run) uchun xizmat qiladi.Linux konteynerlarini ishlatgan holda ilovalarni tarqatish va joylash konteynerizatsiya deyiladi. Konteynerlar yangi narsa emas, lekin ular  ilovalrni onsongina joylash uchun ishlatilishi.  

Konteynerizatsiyalash borgan sari mashxurlashib borayabdi. Bunga asosiy sabablar quyidagilar:

- Flexible (Moslashuvchangligi): xatto eng murakkab ilovalar ham konteynerizatsiyalanishi mumkin  
- Lightweight (Yengil tizim asosida ishlashi): Konteynerlar foydalanuvchi yadrosini foydalanishi va o'zaro almashishi mumkin.
- Interchangeable (Almashtiriluvchan): Siz tez o'zgarishni va tarqatish(deploy)ni amalga oshirishingiz mumkin.  
- Portable (Ko'chirib yuriluvchi): Siz mahalliy qurishni amalga oshirib, kloudga tarqatib va istalgan joyda ishga tushirishingiz mumkin.
- Scalable (Mashtablash imkonini beradi): Siz konteyner nushalarini avtomatik tarzda ko'paytirib yetkazib tarqata olasiz.
- Stackable (Birin ketinlikni xosil qila oladi): Siz servislarni ustma-ust vertikal tahlab ishgha tushirishingiz mumkin.

## Obrazlar va konteynerlar

Konteyner obrazni ishga tushirish bilan ishga tushadi. Obraz bu - bajariluvchan paket bo'lib, u o'zida ilovani ishga tushirish uchun barcha zarur bo'lgan narsalarni o'z ichiga oladi. Masalan, programma kodi, ishga tushirish muhiti, kutubxonalar, o'zgaruvchilar muhiti va sozlashlar fayllari shular jumlasidandir.

Konteyner bu - obrazni ishga tushgan holatdagi nusxasi bo'lib, u bunday vaqtda xotirada joylashadi. Boshqacha qilib aytganda konteyner - obraz holati yoki foydalanuvchi ish jarayoni. Siz ishga tushgan konteynerlar ro'yhatini huddin Linuxdagidek 
``` 
docker ps
```
buyrug'i orqali ko'rishingiz mumkin.

## Konteynerlar va virtual moshinalar

Konteyner Linuxda azaldan ishlaydi, u host moshinani yadrosini boshqa konteynerlar o'rtasida o'zaro taqsimlash uchun xizmat qiladi. U xotiradan kichkna joy oluvchi alohida protsessni ishga tushiradi, aynan mana shuni evaziga uni yengillik hislati ta'minlanadi.

Dockerda Virtual Moshinadan (VM) farqli o'laroq, gipervizor yordamida yadro host resurlariga virtual huquqi bo'lgan "mehmon uchun" Operatsion tizimi ishlab turadi. Qoidaga asosan, ko'p hollarda, virtual moshina ilova ishlashi uchun kerak bo'lgan resursdan ko'prog'i bilan ta'minlaydi. Docker mana shunday hislati yo'qligi bilan ham resurslarni tejaydi.

## Docker muhitingizni tayyorlang

Operatsion tizimga mos qo'llab quvvatlanuvchi Docker Community Edition (DCE) yoki Enterprise Edition (EE) talqinini o'rnating.

[Dockerni o'rnatish](/install/install.md)

## Docker talqinini tekshirish

1. ```docker --version``` ni ishga tushiring va kerakli talqin o'rnatilganligiga ishonch xosil qiling:

``` shell script
docker --version

Docker version 17.12.0-ce, build c97c6d6
```

2. O'rnatilgan Docker haqida batafsilroq ma'lumotga ega bo'lish uchun ```docker info``` (yoki ```docker version``` ni ```--``` larsiz) ni ishga tushiring:

``` shell script
docker info

Containers: 0  
 Running: 0  
 Paused: 0  
 Stopped: 0  
Images: 0  
Server Version: 17.12.0-ce  
Storage Driver: overlay2  
... 
```

Ruhsatga oid muammolardan holi bo'lish uchun ```sudo``` ni ishlating yoki o'zingizning foydalanuvchingizni docker guruhiga qo'shing. [Batafsilroq](https://docs.docker.com/engine/installation/linux/linux-postinstall/).

## Docker o'rnatilganligini test qilish

1. Sizning o'rnatmangiz ishlayotganini tekshirish uchun Dockerning sodda obrazi ```hello-world```ni ishga tushirishga urinib ko'ring:

```
   docker run hello-world

    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    ca4f61b1923c: Pull complete
    Digest: sha256:ca0eeb6fb05351dfc8759c20733c91def84cb8007aa89a5bf606bc8b315b9fc7
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.
...
```
2. Moshinangizga yuklangan ```hello-world``` obrazini ro'yhatda ko'rish uchun quyidagi komandani tering:
```
docker image ls
```
3. Yuqoridagi komandani muvaffaqiyatli natijasini ko'rganingizdan so'ng, ```hello-world``` (shu nomli obrazdan nasl olgan) konteynerini ro'yhatda ko'rish uchun quyidagi komandani tering. Agar u hali ham ishlayotgan bo'lsa sizga ```--all``` opsiyasi kerak emas:
```
docker container ls --all

CONTAINER ID     IMAGE           COMMAND      CREATED            STATUS
54f4984ed6a8     hello-world     "/hello"     20 seconds ago     Exited (0) 19 seconds ago

```

## Takrorlash va aldovnoma

```
## Docker CLI komandalarini ro'yhati
docker
docker container --help

## Docker talqini va u haqda ma'lumotni namoyish etish
docker --version
docker version
docker info

## Docker obrazni ishga tushirish
docker run hello-world

## Docker obrazlar ro'yhatini chiqarish
docker image ls

## Docker konteynerlar ro'yhatini chiqarish (ishga tushirilganlarini ko'rish, hammasini ko'rish (all), hammasini tinch rejimidagilarni ham)
docker container ls
docker container ls --all
docker container ls -aq
```

# Birinchi qism natijalari

Konteynerlash CI/CD ni uzluksizligini ta'minlaydi. Misol uchun:
- ilovalar tizimga bog'liq emas
- o'zgarishlar tarqatilgan ilovaning ixtiyoriy qismiga yuborilishi mumkin
- resurs tig'izligi optimallashtirilishi mumkin
  
Docker bilan ilovangizni masshtablash bu - ijro etiluvchi borliqni izolyatsiyalash bo'lib, og'ir VM hostlarini ishga tushirish emas!
