# B106AA

![B106AA](https://github.com/akkoyun/P101CA/blob/master/Modules/Electronic/%5BB106AA%5D/2D/B106AA.png)

***

| Segment Adı | Açıklama | Prototip | Seri Üretim |
|-------------|----------|----------|-------------|
| A1 | Batarya yuvası (soketi) ve batarya koruma devresi | Evet | Evet |
| A2 | Batarya ölçüm devresi | Evet | Evet |
| A3 | Batarya şarj devresi | Evet | Evet |
| A4 | 3V8 Buck-Boost devresi | Evet | Evet |
| B1 | Uyandırma kaynağı devresi | Evet | Evet |
| B2 | Zamanlama yönetici devresi | Evet | Evet |
| B3 | Harici uyandırma butonu soket devresi | Evet | Evet |
| C1 | GSM modem güç anahtarı | Evet | Evet |
| C2 | Uyuyan (zamanlı) 3V3 güç regülatörü | Evet | Evet |
| C3 | Uyumayan 3V3 güç regülatörü | Evet | Evet |
| D1 | Ana işlemci devresi | Evet | Evet |
| D2 | FOTA işlemcisi uyandırma devresi | Evet | Evet |
| D3 | FOTA işlemcisi güç anahtarı devresi | Evet | Evet |
| D4 | SD kart seçim multiplexeri | Evet | Evet |
| D5 | SD kart devresi | Evet | Evet |
| D6 | FOTA işlemci devresi | Evet | Evet |
| D7 | FOTA işlemci LED bildirim devresi | Evet | Hayır(1) |
| E1 | GSM modem devresi | Evet | Evet |
| E2 | GSM modem LED bildirim devresi | Evet | Hayır(2) |
| E3 | GSM modem haberleşme voltaj dönüştürücü devresi | Evet | Evet |
| E4 | GSM modem sinyal kontrol devresi | Evet | Evet |
| F1 | I2C multiplexer devresi | Evet | Evet |
| F2 | T/H sensörü soket çıkış devresi | Evet | Evet |
| F3 | ST sensörü soket çıkış devresi | Evet | Evet |
| F4 | Basınç sensörü devresi | Evet | Evet |
| F5 | Yağmur sensörü devresi | Evet | Evet |
| F6 | Rezerve soket çıkış devresi | Evet | Hayır(3) |
| F7 | I2C I/O çoklayıcı devresi | Evet | Evet |
| F8 | RTC zamanlayıcı devresi | Evet | Evet(4) |
| F9 | Yapışkan sinyal devresi | Evet | Evet |


* (1) FOTA işlemci LED bildirim devresi [6,765¥]
  - 3 adet - BC847AQAZ Transistör (3 x 1,98¥ = 5,94¥)
  - 9 adet - 33pf Kondansatör (9 x 0,055¥ = 0,495¥)
  - 3 adet - 47K Direnç (3 x 0,033¥ = 0,099¥)
  - 3 adet - 330R Direnç (3 x 0,033¥ = 0,099¥)
  - 3 adet - LED (3 x 0,044¥ = 0,132¥)

* (2) GSM modem LED bildirim devresi [6,765¥]
  - 3 adet - BC847AQAZ Transistör (3 x 1,98¥ = 5,94¥)
  - 9 adet - 33pf Kondansatör (9 x 0,055¥ = 0,495¥)
  - 3 adet - 47K Direnç (3 x 0,033¥ = 0,099¥)
  - 3 adet - 330R Direnç (3 x 0,033¥ = 0,099¥)
  - 3 adet - LED (3 x 0,044¥ = 0,132¥)

* (3) Rezerve soket çıkış devresi [1,485¥]
  - 1 adet - 6 pin Tunik Soket (1 x 0,66¥ = 0,66¥)
  - 3 adet - ESD Diyod (3 x 0,22¥ = 0,66¥)
  - 3 adet - 33pf Kondansatör (3 x 0,055¥ = 0,165¥)

* (4) RTC zamanlayıcı devresi [2,068¥]
  - 1 adet - 33pf Kondansatör (1 x 0,055¥ = 0,055¥)
  - 1 adet - 330R Direnç (1 x 0,033¥ = 0,033¥)
  - 1 adet - BC847AQAZ Transistör (1 x 1,98¥ = 1,98¥)

***
Prototip üzerinde dizilmeyecek komponentler toplamı 17,083¥ (2,44$)