# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

# Proje Kurulumu

Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

## Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#Tablolar
`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/] (update, delete, drop sorguları iptal edilmiştir).

### Görevler

Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını altlarına yazın.

    1) ÖRNEK SORU: Öğrenci tablosundaki tüm kayıtları listeleyin.

    	CEVAP: select * from ogrenci

    2) Öğrenci tablosundaki öğrencinin adını ve soyadını ve sınıfını listeleyin.

    	SELECT ograd,ogrsoyad,sinif FROM ogrenci

    3) Öğrenci tablosundaki kız öğrencileri listeleyin.

    	SELECT * from ogrenci WHERE cinsiyet="K"

    4) Öğrenci tablosunda kaydı bulunan sınıfların adını her sınıf bir kez görüntülenecek şekilde listeleyiniz

    	 SELECT DISTINCT sinif from ogrenci

    5) Öğrenci tablosunda, 10A sınıfında olan kız öğrencileri listeleyiniz.

     SELECT * from ogrenci where sinif="10A" AND cinsiyet="K"

    6) Öğrenci tablosundaki 10A veya 10B sınıfındaki öğrencilerin adını, soyadını ve sınıfını listeleyiniz.

    SELECT ograd,ogrsoyad,sinif from ogrenci where sinif in("10A","10B")

    7) Öğrenci tablosundaki öğrencinin adını, soyadını ve numarasını okul numarası olarak listeleyiniz. (as kullanım örneği)

SELECT ograd,ogrsoyad,ogrno as okulno from ogrenci

    8) Öğrenci tablosundaki öğrencinin adını ve soyadını birleştirip, adsoyad olarak listeleyiniz. (concat, as kullanım örneği)

SELECT CONCAT(ograd, ogrsoyad) AS adsoyad from ogrenci ;

    9) Öğrenci tablosundaki Adı ‘A’ harfi ile başlayan öğrencileri listeleyiniz.

SELECT \* from ogrenci WHERE OGRAD like "a%"

    10) Kitaplar tablosundaki sayfa sayısı 50 ile 200 arasında olan kitapların adını ve sayfa sayısını listeleyiniz.

SELECT kitapadi,sayfasayisi from kitap where sayfasayisi>50 and sayfasayisi<200 order by sayfasayisi

    11) Öğrenci tablosunda adı Fidan, İsmail ve Leyla olan öğrencileri listeleyiniz.

SELECT \* from ogrenci where ograd in("fidan","ismail","leyla")

    12) Öğrenci tablosundaki öğrencilerden adı A, D ve K ile başlayan öğrencileri listeleyiniz.

SELECT \* from ogrenci where ograd like "a%" or ograd like "d%" or ograd like "k%"

    13) Öğrenci tablosundaki sınıfı 9A olan Erkekleri veya sınıfı 9B olan kızların adını, soyadını, sınıfını ve cinsiyetini listeleyiniz.

SELECT ogrsoyad,sinif,cinsiyet from ogrenci where sinif="9A" and cinsiyet="E" or sinif="9B" and cinsiyet="K"

    14) Sınıfı 10A veya 10B olan erkekleri listeleyiniz.

SELECT \* from ogrenci where sinif in("10A","10B") and cinsiyet="E"

    15) Öğrenci tablosunda doğum yılı 1989 olan öğrencileri listeleyiniz.

SELECT \* from ogrenci where dtarih=1989

    16) Öğrenci numarası 30 ile 50 arasında olan Kız öğrencileri listeleyiniz.

SELECT \* from ogrenci where ogrno between 30 and 50 and cinsiyet="K"

    17) Öğrencileri adına göre sıralayınız (alfabetik).

SELECT \* from ogrenci order by ograd

    18) Öğrencileri adına, adı aynı olanlarıda soyadlarına göre sıralayınız.

SELECT \* from ogrenci order by ograd,ogrsoyad

    19) 10A sınıfındaki öğrencileri okul numarasına göre azalan olarak sıralayınız.

SELECT \* from ogrenci where sinif="10A" order by ogrno desc

    20) Öğrenciler tablosundaki ilk 10 kaydı listeleyiniz.
    [İPUCU: `Select top tüm mysql versiyonlarında düzgün çalışmaz. LİMİT kullanmak daha faydalıdır`]

SELECT \* from ogrenci limit 10 21) Öğrenciler tablosundaki ilk 10 kaydın ad, soyad ve doğum tarihi bilgilerini listeleyiniz.
SELECT ograd ,ogrsoyad,dtarih from ogrenci limit 10

    22) Sayfa sayısı en fazla olan kitabı listeleyiniz.

SELECT \* from kitap order by sayfasayisi desc limit 1

    23) Öğrenciler tablosundaki en genç öğrenciyi listeleyiniz.

SELECT \* from ogrenci where dtarih!="" order by dtarih desc limit 1

    24) 10A sınıfındaki en yaşlı öğrenciyi listeyin.

SELECT \* from ogrenci where sinif="10A" and dtarih!="" order by dtarih limit 1

    25) İkinci harfi N olan kitapları listeleyiniz.

SELECT \* from kitap where kitapadi like "\_N%"

    26) Öğrencileri sınıflarına göre gruplayarak listeleyin.

SELECT sinif from ogrenci group by sinif

    27) Öğrencileri her sorgulamada sıralaması farklı olacak şekilde rastgele listeleyin.
    [İPUCU: rand() fonksiyonu]

SELECT \* from ogrenci order by RAND()

    28) Öğrenci tablosundan Rastgele bir öğrenci seçiniz.

SELECT \* from ogrenci order by RAND() limit 1

    29) 10A sınıfından rastgele bir öğrencinin adını, soyadını, numarasını ve sınıfını getirin.

SELECT ograd,ogrsoyad,ogrno,sinif from ogrenci where sinif="10A" order by RAND() limit 1

    # Esnek
    30) Öğrenci tablosunda aynı isimde kaçar öğrenci olduğunu bulmak istiyoruz.
    Öğrenci isimlerinin sayısını "adet" olarak öğrencilerin isimleri "isim" olarak listeleyin.
    [İPUCU: count() ve group by]

SELECT count(ograd) as ayniAd,ograd from ogrenci group by ograd
