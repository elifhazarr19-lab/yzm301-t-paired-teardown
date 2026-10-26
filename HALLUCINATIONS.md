# HALLUCINATIONS — Aşama 1 günlüğü

Bu dosya araştırma sırasında ortaya çıkan varsayımları, çelişkileri ve eksikleri kaydeder. Ajanın yanlış çıkarımları Aşama 2'de (REA ve diferansiyel testle) güncellenecek.

Durum sütunu: **AÇIK** (doğrulanmadı), **ÇÜRÜTÜLDÜ** (yanlış çıktı), **KAPANDI** (kanıtla doğrulandı).

| ID | Tür | Varsayım ya da bulgu | Durum | Nasıl ele alınacak |
|---|---|---|---|---|
| H-01 | Eksik kanıt | Prompt ve ödev `CONTRACT.md` dosyasına atıf yapıyor; dosya verilmedi. t-paired parametre adları ve çıktı alanları bu yüzden kesinleşemedi. | AÇIK | Kullanıcıdan dosyayı istemek. Yoksa CLI sözleşmesi t-paired için belirsiz kalır. |
| H-02 | Çelişkili/yanıltıcı kaynak | Ödevdeki CLI örneği ve JSON çıktısı `t2-indep` içindir. `t-paired` için aynı alan adlarının geçerli olduğu belgede yazmıyor. | AÇIK | Örneği t-paired'a uygulamamak. Alanları G*Power'dan gözlemek. Ayrım SPEC'te işaretlendi. |
| H-03 | Ajan çıkarımı | t-paired için `ncp = dz · √N` ve `df = N − 1` formülü. Ajanın genel istatistik bilgisine dayanıyor; kılavuz ya da kanıt yok. | AÇIK (HİPOTEZ H-S1) | G*Power ile aynı girdilerle karşılaştırmak. Uyuşmazsa hipotez ÇÜRÜTÜLDÜ olarak işaretlenecek. |
| H-04 | Kaynak karışıklığı riski | Ders slaytındaki `ceil çağrısı: 104,2 → 105` ve `df = 2n − 2` satırları REA kanıtı gibi görünebilir. Bunlar örnek; bu projenin kanıtı değil. | KAPANDI (kopyalanmadı) | Yalnızca LEDGER DOK-11'de not olarak tutuldu. [REA] satırı yazılmayacak. |
| H-05 | Doğrulanmamış değer | Slayt 20'deki t2-indep değerleri (N=210, t≈1,9714, df=208, δ≈3,6228) "scipy ile doğrulandı" diyor. Bu değerler bizim gözlemimiz değil ve t-paired'a ait değil. | AÇIK | Yalnızca [DOK] olarak tutuldu. Kesin referans olarak kullanılmadı. |
| H-06 | Yanlış varsayım riski | Kullanıcının seçtiği K2 ailesinin takımına ait olduğu varsayıldı. Grup tablosunda öğrenci numarası var, isim yok; satır bu kayıtla eşleştirilemedi. | AÇIK | Kullanıcının teyidi istenecek (LEDGER DOK-01). |
| H-07 | Eksik ortam | G*Power, Ghidra ve JDK 21 bu makinede yok. Prompt erişimi varsaymamamızı istiyor; ödev metni ise bu araçları ön koşul olarak gösteriyor. | KAPANDI (ortam kaydı) | LEDGER ENV-01..04 olarak kaydedildi. Hiçbir yerde G*Power ya da REA sonucu üretilmedi. |

## Aşama 2 için ilk hedefler

- H-01 ve H-02 için CONTRACT.md ya da G*Power çıktısı gerekiyor.
- H-03 için en az 3 t-paired vektörüyle hipotezi sınamak.
- Ödevin istediği en az 2 gerçek ajan yanılgısı, Aşama 2'de REA ve diferansiyel test sonuçlarıyla kayda geçecek.
