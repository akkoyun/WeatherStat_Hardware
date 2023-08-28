# FOTA (Firmware Over The Air) Güncelleme

Yeni nesil IoT cihazlarda; sahada stabil çalışma ve cihaz yanına olabildiğince az gidilmesi zorunluluk haline gelmiştir. Bu sebeple cihazların uzaktan güncellenmesi konusu üzerine çalışılmış ve bir çözüm bulunmuştur. Sahada bulunan IoT cihazlarımız GSM üzerinden kendini güncelleme özelliğine sahip olmuşlardır. Aşağıda konu ile ilgili teknik algoritma detaylıca anlatılmıştır.

![FOTA Çalışma Diagramı](https://github.com/akkoyun/P101CA/blob/master/Modules/Electronic/%5BB106AA%5D/Documentation/FOTA%20WorkFlow/Images/FOTA%20Update.gif?raw=true)

## FOTA Çalışma Algoritması

1. Uyku modunda çalışmakta olan B106AA modülü (sensörler hariç tim sistem enerjisiz, MCU kapalı) herhangi bir uyandırma kaynağından gelen uyarı ile enerjilenir. 
2. Ana işlemci enerjilenerek çalışmaya başlar.
3. GSM modem enerjilendirilir ve internete bağlanır.
4. Sistem içerisinde yer alan SD kart üzerindeki ayar dosyası okunur.
5. IoT root sunucularına mevcut firmware versiyonu sorgulanmak üzere gönderilir (diğer boot bilgileri ile birlikte).
6. Gönderilen firmware versiyonu sunucu tarafından ilgili kayıtlardan kontrol edilir.
7. Eğer herhangi bir güncellemeye ihtiyaç yok ise kayıt başarılı cevabı verilir ve B106AA rutin kodunu çalıştırmaya devam eder.
8. Eğer yeni bir firmware var ise sunucu firmware kayıt kodunu B106AA ya döner.
9. B106AA gerekli kod ile firmware sunucusundan istekte bulunur.
10. Firmware sunucu güncel firmware i TXT formatında B106AA ya döner.
11. B106AA TXT formatındaki dosyayı okuyarak SD kart üzerine HEX olarak kaydeder.
12. Kayıt işleminin ardından FOTA işlemcisini enerjilendirmek için "Signal Latch" devresine sinyal verir.
13. "Signal Latch" gelen sinyal doğrultusunda FOTA işlemcisi güç anahtarını aktif eder.
14. Aktif olan güç anahtarı FOTA işlemcisini enerjilendirir.
15. Enerjilenen FOTA işlemcisi öncelikle ICSP anahtarına sinyal göndererek ICSP hattını kendi üzerine aktarır.
16. FOTA işlemcisi artık SPI veri yolu üzerinden SD karta bağlanmış olur.
17. FOTA işlemcisi SD kart üzerinden okuduğu firmware i ilgili I/O bağlantısı üzerinden ana işlemciye yazar.
18. Yazma işlemi başarılı olması durumunda ana işlemci resetlenir.
19. Ana işlemci yeniden çalışmaya başladığı an FOTA işlemcisi "Latch" devresine işlemin tamamlandığını belirten sinyal gönderir.
20. Bu sinyal ile FOTA güç anahtarı tekrar pasif olarak FOTA işlemcisinin güç hattını keser ve pasif eder.
21. Güncellenen ana işlemci reset sonrası tekrar sunucuya yeni versiyon bilgisi ile sorgulama yapar.