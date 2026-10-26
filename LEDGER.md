# LEDGER — G*Power t-paired kanıt defteri

**Durum: Aşama 1 (başlangıç). REA ile doğrulanmış tek bir davranış henüz yok.**
Bu dosyadaki satırlar üç kaynaktan gelir ve etiketle ayrılmıştır:

- `[REA]` Binary'den doğrudan kanıtlandı (fonksiyon adresi veya dize referansı). **Şu an 0 satır.**
- `[DOK]` Ödev metni, ders slaytları veya kılavuz. Doğrulanmış davranış sayılmaz; kaynak olarak kullanılır.
- `[AJAN]` Ajanın çıkarımı. Kanıtı yok; SPEC'te kesin kural olarak kullanılmaz.

Bölüm A ortamın durumunu kaydeder. Bunlar G*Power'ın davranışı değildir.

---

## A. Ortam kontrolleri (davranış değil)

| ID | Kontrol | Gözlem | Kanıt | Sonuç |
|---|---|---|---|---|
| ENV-01 | G*Power 3.1.9.7 bu makinede var mı? | İlk taramada bulunamadı. Sonradan indirilenler klasöründe zip arşivi bulundu; arşivin içinde `GPowerNT.exe` var. Arşiv dışarıya çıkarılmadı, yalnızca analiz için geçici klasöre ayrıca çıkarıldı. | Dosya listesi ve SHA-256 (bkz. Bölüm C). | Sürüm ve hash doğrulandı. Repoya dosya konmaz. |
| ENV-02 | REA erişimi | `rea-agents` **6.7.0** npm global paketi kurulu. Oturum sonunda REA MCP araçları bağlandı; `open_binary`, `search_strings`, `xrefs` çalıştı. | Araç çağrıları (Bölüm C). | REA ile `[REA]` kanıtı toplanabiliyor. |
| ENV-03 | Ghidra ve JDK 21 | Sonradan Ghidra 12.1.4 ve Eclipse Temurin JDK 21 kuruldu; REA bunları kullandı. | REA çıktısındaki sürüm bilgisi. | Analiz yapılabiliyor. |
| ENV-04 | GUI gözlemi ve ekran görüntüsü | Bilgisayar kontrolü henüz bu oturumda kullanılamıyor (araçlar yüklenmedi). G*Power değerleri şu an elle ya da kontrol aracıyla alınmadı. | Ajan araç listesi. | Ekran görüntüsü yok. `oracle/` içinde görsel yok. |
| ENV-05 | Ders belgesi `yzlm.gerceklesme.pdf` | 26 sayfa, metin katmanı yok (görüntü tabanlı). PyMuPDF ile 110 dpi PNG'ye çevrilip sayfa sayfa okundu. | Okuma sırasında alınan sayfa görüntüleri (geçici klasör). | İçerik okundu. Bölüm B'deki `[DOK]` satırlarının bir kısmı buradan geliyor. |
| ENV-06 | Ödev metni `2026-10-16-odev-supp (1)` | Uzantısız düz metin, ödevin tamamı okundu. | Dosya okuması. | Okundu. |
| ENV-07 | Grup/aile tablosu `Ogrenciler_gruplar.pdf` | Test aileleri tablosu okundu (K1–K4). Öğrenci satırları bu kayıtta kullanılmadı. | PDF metin çıkarımı. | K2 = t-paired (bkz. DOK-01). |
| ENV-08 | `CONTRACT.md` | Verilen dosyalar arasında yok. Ödev metni `[LİNK: CONTRACT.md]` diyor. | Dosya listesi. | **Eksik.** Diğer aileler ve t-paired parametre adları buradan okunamadı. |

---

## B. Belgelerden gelen bilgiler [DOK]

**DOK-01: Aile K2 = t testi, eşleştirilmiş ortalama (önce ve sonra).**
- Kaynak: `Ogrenciler_gruplar.pdf`, "TEST ALELER" tablosu; ödev metni madde 2.
- Belirsizlik: Hangi grubun K2 aldığını bu kayıt doğrulamıyor. Takımınızın satırını siz teyit etmelisiniz.

**DOK-02: Modlar a priori (N hesapla) ve post hoc (gücü hesapla).**
- Kaynak: ödev metni "Modlar"; ders slaytı 21.

**DOK-03: Örnek CLI çağrısı ve JSON çıktısı, `t2-indep` içindir, `t-paired` için yoktur.**
- Çağrı: `gpower-clone --test t2-indep --mode a-priori --tails 2 --d 0.5 --alpha 0.05 --power 0.95 --ratio 1`
- Çıktı: `{"n1":105,"n2":105,"n_total":210,"actual_power":0.9501,"critical":1.9714,"df":208,"ncp":3.6228}`
- Kaynak: ödev metni, madde 1a.
- Not: Bu değerler t-paired'a aktarılamaz. t-paired'da `n1/n2` alanlarının anlamı bu belgede tanımlı değil.

**DOK-04: Geçersiz girdi davranışı.** `{"error":"<açıklama>"}` çıktısı ve sıfırdan farklı çıkış kodu.
- Kaynak: ödev metni, madde 1a.

**DOK-05: Tolerans.** `N`, `n1`, `n2` tam eşleşmeli. Diğer değerler G*Power ekranının gösterdiği basamağa kadar eşleşmeli.
- Kaynak: ödev metni, madde e.

**DOK-06: Kütüphane kesirli N verir, G*Power yukarı yuvarlar.** Bu fark açıklanması gereken bir bulgu.
- Kaynak: ödev metni, madde c (Not).

**DOK-07: Kâhin G*Power'ın kendisidir.** Arayüzden en az 30 vektör, her biri ekran görüntüsüyle. Kütüphane (`pwr`, `statsmodels`) karşılaştırması ölçek için ayrıca 500+ vektör.
- Kaynak: ödev metni, madde c; ders slaytı 20.

**DOK-08: Sınır değerleri vektörlere konmalı.** `d` çok küçük, `d` çok büyük, güç `≤ α`, eşit olmayan oran, geçersiz girdi.
- Kaynak: ödev metni, madde d.

**DOK-09: Puan yalnızca `[REA]` satırlarına verilir.** Bu defterdeki `[DOK]` ve `[AJAN]` satırları temel puana katkı vermez.
- Kaynak: ödev metni, madde f.

**DOK-10: Ders slaytındaki t2-indep örneği.** `a priori, iki bağımsız ortalama, d=0,5, α=0,05, güç=0,95` → toplam N=210 (grup başına 105), kritik t≈1,9714, df=208, δ≈3,6228. Slayt bu değerlerin scipy ile doğrulandığını yazıyor.
- Kaynak: `yzlm.gerceklesme.pdf`, slayt 20.
- Not: Bu bizim gözlemimiz değil. t2-indep örneği olduğu için t-paired'a uygulanamaz.

**DOK-11: Slayttaki kanıt defteri örnekleri bu projenin kanıtı değildir.** Slayt 22'deki `ceil çağrısı: 104,2 → 105`, `df = 2n − 2`, `güç 0,95 iterasyonu` satırları örnek olarak verilmiş. Bu defterde kopyalanmadı.
- Kaynak: `yzlm.gerceklesme.pdf`, slayt 22.

**DOK-12: REA kaynakları.** `github.com/morluto/rea`, `rea.tools`, npm paketi `rea-agents`. Benzer isimli sahte paketlere dikkat.
- Kaynak: ödev metni, KURULUM; slayt 19; REA README.

---

## C. Gözlenen davranışlar [REA]

Hedef: `GPowerNT.exe` (G*Power 3.1.9.7 Windows zip içinden çıkarıldı), SHA-256 `C63E6A133EB6372932F810C08CC33DC35A06D1DDB658F897BD6C34A754EFC812`, PE x86, 9116 prosedür, 2570 string. Analiz REA 6.7.0 + Ghidra 12.1.4 ile yapıldı. Arşiv (`GPowerWin_3.1.9.7.zip`) SHA-256: `3BB7F1F2478D74EE5BA701AE7F849373CF2B8A11F6B6216C7C6B236DB7861199`.

| ID | Davranış / yapı | Gözlem | Kaynak | Sonuç ve belirsizlik |
|---|---|---|---|---|
| [REA] REA-01 | Etki büyüklüğü kaynağı: t-paired iletişim kutusu | `CEff_T_PairedMeans` string'i 0x5d698c adresinde; bu adrese referans veren yer 0x5d6794 (`PTR_s_CEff_T_PairedMeans_005d6794`, işaretçi tablosu girdisi) | `xrefs`, `inspect_address_context` (ev_03e1a5…) | Sınıf/iletişim kutusu adı doğrulandı. Hangi kod yolunun bu girdiyi çağırdığı henüz izlenmedi. |
| [REA] REA-02 | Etki büyüklüğü dz girdi alanları | `tdm_mean_dz` (0x5d6b9c), `tdm_sd_dz` (0x5d6b90) string'leri; 0x5d6b90'a referanslar 0x52e976 ve 0x52ec29 | `xrefs` (ev_6e335d…) | Ortalama ve standart sapmadan dz hesaplayan kod 0x52e976 çevresinde (`FUN_0052e8d0`, gövde 0x52e8d0–0x52e9b6, 231 bayt). Formül henüz çözülmedi. |
| [REA] REA-03 | Etki büyüklüğü adı | "Effect size dz" string'i 0x5c5ba0 | `search_strings` (ev_422b1f…) | Arayüz etiketi doğrulandı. |
| [REA] REA-04 | Mod adları | "A priori", "Post hoc", "Compromise", "Sensitivity", "Criterion" metinleri 0x5c51a7–0x5c5310 | `search_strings` | Beş analiz modu metinde doğrulandı. t-paired'a özgü davranış henüz gözlenmedi. |
| [REA] REA-05 | Girdi doğrulama mesajı | "In a priori calculations the effect size must not be zero." (0x5c67d0); "effect size must be greater than 0.00001." (0x5cb220) | `search_strings` | Mesaj metni doğrulandı; eşiğin t-paired'da hangi kodda uygulandığı [AÇIK]. |
| [REA] REA-06 | Dağılım/ncp kodu | `search_procedures` ile "noncentral" aramasında isim bulunamadı (semboller temizlenmiş) | `search_procedures` (ev_9fe0e5…) | Ncp hesabı henüz bulunmadı. Prosedür adı yok; adres ve çağrı grafiğiyle izlenecek. |

Henüz yok: ncp/df formülünün kodda bulunması, N'nin yuvarlaması, geçersiz girdi davranışı. Bunlar için GUI vektörleri ve prosedür çağrı grafiği gerekli.

**Not:** `analyze_function` çıktısı çok büyük olduğu için kaydedilemedi; bu adım tekrar edilmeli.

Her satırın şu alanları olacak: kanıt kimliği, araştırılan davranış, gözlenen giriş, gözlenen çıktı, kaynak (fonksiyon adresi veya dize referansı), ekran görüntüsü veya kanıt dosyası, yeniden üretim adımları, sonuç, belirsizlik.

---

## D. Ajan çıkarımları [AJAN]

Henüz yok. Ajanın t-paired için ürettiği formül ve kurallar buraya girecek; hiçbiri SPEC'e kesin kural olarak girmeden önce [REA] ile sınanacak. Bu konuda bkz. [HALLUCINATIONS.md](HALLUCINATIONS.md), H-03.

---

## E. Açık sorular ve sınırlar

1. `CONTRACT.md` yok. t-paired parametre adları ve çıktı alanları doğrulanamadı.
2. t-paired için `n1`/`n2` alanlarının anlamı belirsiz (tek grup, çift sayısı).
3. G*Power'ın t-paired için kullandığı etki büyüklüğü (`dz` veya başka) belirsiz.
4. Yuvarlama kuralı ve iterasyon durma koşulu henüz gözlenmedi.
5. Geçersiz girdi davranışı henüz gözlenmedi.
6. Takım aile teyidi (DOK-01) kullanıcı tarafından yapılmalı.
