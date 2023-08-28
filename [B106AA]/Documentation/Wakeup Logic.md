# Sistem Uyandırma Kaynakları Lojik Devresi.

B106AA GSM IoT modülü güç tüketimini minimize edebilmek adına sürekli uyuyan bir güç mimarisi üzerine kurgulanmıştır. Sürekli uyuyan ana kaynaklar yanı sıra sürekli açık olup ardışık ölçümler yapabilen bir sensör mimarisi de mevcuttur. Sürekli enerjili ve ölçüm yapmaya devam eden sensörler belirlenen (sensör üzerine programlanan) interuptlar yardımı ile ana sistem uyku modundan çıkartılabilmektedir. Bu uyandırma sistematiği aşağıda detaylı olarak anlatılmıştır.

## Interrupt Kaynakları

Sistem üzerinde yer alan ölçüm sensörleri ve manüel veri gönderim butonu sistemi uyku modundan çıkmasına yardım edicek şekilde kurgulanmıştır.

![Wakeup Logic Circuit](https://github.com/akkoyun/P101CA/blob/master/Modules/Electronic/%5BB106AA%5D/Documentation/Wake%20up%20logic.jpg)

### A- Manüel Veri Gönderim Butonu

Sistem kurulumu sırasında veri gönderim testleri yapılabilmesi veya herhangi bir kullanıcı kontrolünde veri göndermesi istenen durumlarda cihaz üzerinde bulunan manüel veri gönderim butonuna basılarak sistem uyandırılabilmektedir. Bu sinyal hattı şematik üzerinde [Signal_Shot_Interrupt] olarak tanımlanmıştır. Sinyal aktif high olacak şekilde kurgulanmıştır. Ve bu sinyal lojik devre elemanları ile diğer uyandurma kaynakları ile eşlenik olarak ana sistem zamanlayıcısını çalıştırmaktadır. Tüm uyandırma kaynakları sistem uyandırıldıktan sonra I2C üzerinden sıfırlanabilmektedir (sıfırlanana kadar sinyal latch olarak kalmaktadır). Diğer uyandırma kaynakları aksine butona basıldıktan sonra bırakıldığı için buton tekrar low konuma gelmekte ve butona basıldığı tesbit edilememektedir. Buton basımını tesbit etmek ve sistemin hangi uyandırma kaynağından uyandırıldığını belirlemek adına bu sinyal hattı bir latch devresi ile (nor latch) işlemci tarafından belirlenebilir şekilde kurgulanmıştır.

Uyandırma butonu ile sistem uyandırılması durumunda [Signal_Shot_Latch] high duruma geçecektir. Ve işlmeci tarafından bu kaynak tesbit edildikten sonra gene işlemci tarafından [Signal_Latch_Reset] sinyali ile sıfırlanacaktır. Bu sayede butona basıldığı ve sistemin manüel olarak uyandırıldığı tesbit edilebilecektir.

Manüel veri gönderim sinyalini oluşturacak kaynak B303AA buton modülüdür ve parazit koruması mevcuttur.

### B- Yağmur Tesbit Interrupt'ı

P101CA meteoroloji istasyonu üzerinde yağmur yağıp yağmadığını anlamak amacı ile FDC2112 kapasitif algılama sensörü kullanılmaktadır. Sistem kapasite algılama plakaları üzerinde oluşacak her türlü kapasitif değişim durumlarından (2 algılama plakası ile 2 kanal çalışmaktadır) aktif low uyandırma sinyali oluşturmaktadır.

	Bug Report 001 : sistem üzerinde active low olması gereken sinyal hattı active high olarak kurgulanmış

### C- Hava Sıcaklığı / Bağıl Nem Interrupt'ı

P101CA meteoroloji istasyonu üzerinde hava sıcaklığı ve bağıl nem ölçümü yapmak amacı ile HDC2010 sıcaklık nem sensörü kullanılmaktadır. Sıcaklık ve bağıl nem değişiklikleri belirlenen aralıklardan dışarı çıkması durumunda sistem active high (**değiştirilebilir**) çıkış vermektedir.  

### D- Rezerve Sensör Interrupt'ı

P101CA meteoroloji istasyonu üzerinde harici sensör bağlamaya uygun bir soket bulunmaktadır. Bu soket üzerinde oluşacak aktif high interupt girişi bulunmaktadır.

### E- Hava Basıncı Interrupt'ı

Sistem üzerinde bulunan NXP firmasına ait MPL3115A2R1 basınç sensörü belirlenen parametreler doğrultusunda interrupt üretmektedir. Basınç değişiklikleri belirlenen aralıklardan dışarı çıkması durumunda sistem active high (**değiştirilebilir**) çıkış vermektedir.  

### F- Toprak Sıcaklığı Interrupt'ı

P101CA meteoroloji istasyonu üzerinde toprak sıcaklığı ölçümü yapmak amacı ile HDC2010 sıcaklık nem sensörü kullanılmaktadır. Sıcaklık değişiklikleri belirlenen aralıklardan dışarı çıkması durumunda sistem active high (**değiştirilebilir**) çıkış vermektedir.  

### G- Batarya Ölçüm Interrupt'ı

P101CA meteoroloji istasyonu üzerinde batarya ölçümü yapmak amacı ile MAX17055 ölçüm sensörü kullanılmaktadır. Bataryada problem çıkması durumunda sistem active low çıkış vermektedir.  

### H- Zamanlayıcı Interrupt'ı

P101CA meteoroloji istasyonu üzerinde zaman kritik işlemler yapmak amacı ile RV-3028 zamanlayıcı saati kullanılmaktadır. Belirlenen parametrelerin oluşması durumunda sistem active low çıkış vermektedir.  

