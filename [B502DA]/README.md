# T/H Sensör Spesifikasyonları

STF Tarım A.Ş. tarafından üretilen meteoroloji sensörleri aşağıda detaylıca incelenmiş ve üreticiler tarafından belirlenen kullanım koşulları (ilgili teknik doküman atıfları) göz önünde bulundurularak detaylı bir rapor halinde aşağıda sunulmuştur.

## Sıcaklık ve Nem Sensörü

**Sensör Üretici Firması** : Texas Instruments
**Sensör Modeli** : HDC2010
**Kullanım Amacı** : Hava Sıcaklığı ve Bağıl Nem Ölçümü

Kullanılan HDC2010 model sensör için ilgili teknik [dokümanın](https://www.ti.com/lit/ds/symlink/hdc2010.pdf) 5. sayfasında yer alan teknik özellikler şu şekildedir.

| Teknik Detay | Veri |
|----------------|------|
|Sıcaklık ölçüm başarımı| 0,2 C|
|Sıcaklık ölçüm aralığı| -40 C  / 125 C|
|Nem ölçüm başarımı| 2%|
|Nem ölçüm aralığı| 0% / 100% (bağıl nem)|
|Ölçüm hızı | 600 uS |
|Uyarı tipi | Sıcaklık ve Nem Aralığı |
|Uyku modu güç tüketimi| 0,105 uA|
|Ölçüm modu güç tüketimi| 600 uA|
|Sensör iletişim yöntemi| I2C|
|Çalışma Sıcaklığı |  -40 C  / 125 C|

## Hesaplanabilen Parametreler

	1- Su Üstü Bağıl Nem (Uw)
	2- Buz Üstü Bağıl Nem (Ui)
	3- Çiğ Noktası (Td)
	4- Mutlak Nem (Dv)
	5- Karışım Oranı (r) 
	6- Kısmi Su Basıncı (e)
	7- Kısmi Doygun Su Basıncı (ew)
	8- Sıcaklık İndisi (Hi)
	9- Donma Noktası (tf)
	10- Entalphy (h)
	11- Hava Yoğunluğu (Ph)
	12- Sıcaklık Kapasitesi (Cph)  

Hesaplamaları yapılabilir ve veritabanında kaydedilebilir. Ayrıca bunların mevsim normalleri ile karşılaştırmaları yapılabilir. 

### NOT :

	Türkiyede şimdiye kadar ölçülmüş en düşük sıcaklık -41 C (Van Çaldıran 1931), En yüksek sıcaklık 
	ise 48,8 C (Mardin Kocatepe 1990). [Kaynak Meteoroloji Genel Müdürlüğü]
	
	Dünyada şimdiye kadar ölçülmüş en düşük sıcaklık -82,2 C (Vostok Antartika 1983), En yüksek 
	sıcaklık ise 56,7 C (Greenland Ranch, California USA 1913). [Kaynak Meteoroloji Genel Müdürlüğü]
	
	Görüleceği üzere tüm sensörler en zorlu arazi şartları olan -40 C ila +85 C arasında stabil 
	şekilde çalışmaktadır. Bu rakamların üstüne ve altına inildiğinde sadece hata payı oluşmakta 
	ve sensör kalıcı bir hasar oluşmamaktadır. Ayrıca -10 C altında ve +30 C üzerinde sulama 
	yapılmadığı için (kaynak ziraat mühendisleri odası) sensör kendini kapalı tutacağı için ölçüm 
	hatasıda söz konusu değildir.

# Sensör Veri Ölçüm Algoritmaları

Meteoroloji sensörlerinde kullanılan ölçüm sistematiği veri doğruluğu açısından tekli ve çoklu ölçüm prensibi ile yapılmaktadır. Yaptığımız deneyler ve testler doğrultusunda çoklu ölçüm sistematiğinin daha temiz ve doğru veri verdiği belirlenmiştir. Çoklu ölçüm sistematiğinde kullanıcının tanımladığı (n) ölçüm sayısı kadar ölçüm yapmak ve bu ölçümleri çeşitli istatistiksel ortalama metodları ile tek bir veri üzerine dönüştürmek üzerine algoritmalar kurulmuştur. Fonksiyonlarda ölçüm sistematiği seçimsel olarak planlanmıştır böylece kullanıcının veriyi istediği yöntem ile ölçmesine olanak tanıyan istatistik yöntemleri belirlenmiştir.

STF Sensör ölçümlerinde kullanılan istatistiki yöntemler şu şekildedir. (bu methotlar ile sınırlı kalınmayıp ek ölçüm sistemleri tanımlanabilmektedir.)

	1- Aritmetik Ortalama
	2- RMS Ortalama
	3- Temizlenmiş RMS Ortalama (max ve min pikleri arındırılmış)
	4- Median Ortalama
	5- 1 Sigma RMS Ortalama (1 Sigma aralığına giren verilerin ortalaması)

## Artimetik Ortalama Yöntemi

1. Kullanıcı tarafından belirtilen sayıda (n) ölçüm yapılır.
2. Bu ölçüm değerleri toplanır.
3. Hesaplanan Toplam, veri sayısına bölünür.

## RMS Ortalama Yöntemi

1. Kullanıcı tarafından belirtilen sayıda (n) ölçüm yapılır.
2. Bu ölçüm değerlerinin kareleri alınarak toplanır.
3. Hesaplanan toplam, veri sayısına bölünür.
4. Elde edilen değerin karekökü alınır.

Not : Sıcaklık değerleri eksi değerler alabileceği için bu yöntem kullanılamaz.

## Temizlenmiş RMS Ortalama Yöntemi

1. Kullanıcı tarafından belirtilen sayıda (n) ölçüm yapılır.
2. Bu ölçüm değerieri içerisinden MAX ve MİN ölçüm değerleri çıkartılır.
3. Kalan verilerin kareleri alınarak toplanır.
4. Hesaplanan toplam, veri sayısına bölünür.
5. Elde edilen değerin karekökü alınır

Not : Sıcaklık değerleri eksi değerler alabileceği için bu yöntem kullanılamaz.

## Median Ortalama

1. Kullanıcı tarafından belirtilen sayıda (n) ölçüm yapılır.
2. Bu ölçüm değerlerinin orta noktası bulunar.

## 1 Sigma RMS Ortalama

1. Kullanıcı tarafından belirtilen sayıda (n) ölçüm yapılır. 
2. Bu ölçümlere ait Standart Sapma hesaplanır. 
3. 1 Sigma aralığına giren veriler seçilir.
4. Seçilen bu verilerin toplamı alınır.
5. Hesaplanan toplam, veri sayısına bölünür.
