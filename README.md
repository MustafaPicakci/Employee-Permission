# Employee-Permission

## Acknowledgements

- ibrahimaltinoluk
- tugayipek1
- kenanyasinsarigul


# Hexagonal Mimari Örnek Uygulaması Hakkında

Domain ve Infrastructure katmanının bulunduğu iki ana maven modülü bulunmaktadır.

## Domain

Domain modülü herhangi bir db, que yada framework'e bağımlı değildir.
Sorumluluğu olan business'ı yerine getirir.

- Varlıkların kalıcılığını (diske yazma, hafızada tutma) sağlama,
- Kullanıcıdan veri alma (Http, CLI, Form...),
  sorumluluğunu `application` katmanına bırakır.

Bu repodaki örnek business, personelin bina ve daireler içerisindeki giriş çıkış yetkileri ile ilgilidir

## Application

Bu modül, domain katmanındaki business'ı çalıştır hale getirecek etkileşimleri (springboot http) ve altyapıları (postgresql db) sağlamaktadır.

## Application katmanı nasıl geliştirilmeli?

### Crud işlemleri

Domain katmanı crud işlemlerini `com.acme.domain.<entity>.service` paketi içerisindeki servis implementayonları sayesinde gerçekleştirir. Ancak varlıkların kalıcılığını sağlanması sorumluluğunu application katmanına bırakır. Application katmanının bunu sağlayabilmesi için domain katmanının verdiği apiler `com.acme.domain.<entity>.port` altındaki repository interface'leridir.

## Örnek Case Hakkında

- Uygulamada firma tanımlanabilir.
- Binanın bir adresi olmalı.
- Firmaya ait yalnızca bir bina tanımlanabilir.
- Binaya ait katlar bulunuyor.
- Bir binada en fazla 5 kat bulunabilir.
- Katlara girmek isteyen personellerin hangi yetkilere sahip olması gerektiği katlara tanımlanabilir.
- Katlara ait daireler bulunuyor.
- Bir katta en fazla 4 daire olabilir.
- Dairelere girmek isteyen personellerin hangi yetkilere sahip olması gerektiği daireye tanımlanabilir.
- Firmaya ait departmanlar bulunuyor.
- Deparmana ait personellerin yetkileri departmana tanımlanabilir.
- Departmana ait personeller bulunuyor.
- Sistemde bir takım yetkileri bulunuyor.
- Sistemdeki yetkiler hem departman hem de personele verilebiliyor.
- Personel ait yetkiler departmanına ait yetkileri ezmektedir.

Her departman'ın personellerine ait genel kısıtlar bulunuyor. Örneğin IT departmanında çalışan personeller yalnızca 1. ve 2. kata çıkabilir. yada sadece daire 5 ve 7 ye giriş yapabilir. gibi..

Her giriş çıkış işlemi ve başarı durumu loglanmalı.
