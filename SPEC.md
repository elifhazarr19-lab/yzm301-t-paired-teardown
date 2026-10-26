# SPEC — G*Power t-paired (K2) yeniden uygulama şartnamesi

**Durum: TASLAK. Büyük bölümü doğrulanmamış.**
Bu dosya yalnızca [LEDGER.md](LEDGER.md) içindeki `[DOK]` kaynaklarına dayanır. Hiçbir sayısal kural G*Power'da çalıştırılarak doğrulanmamıştır. Doğrulanmamış her madde **[AÇIK]** veya **[HİPOTEZ]** olarak işaretlidir ve kesin kural gibi uygulanmamalıdır.

Okuyucu bu dosyayı tek başına okuyarak uygulamayı yazabilmelidir. Bu nedenle her başlık ya bir kesin kural ya da bir açık maddedir.

---

## 1. Test ailesi

- **Aile adı:** `t-paired` (K2). [DOK: Ogrenciler_gruplar.pdf, DOK-01]
- **Tanım:** Aynı bireylerin iki ölçümü (ör. tedavi öncesi ve sonrası tansiyon) arasındaki ortalama farkın sıfırdan farklı olup olmadığını sınayan t testi.
- **Bağımsız iki grup testiyle (`t2-indep`) karıştırılmaz.** [DOK: ödev metni, madde 1]
- **Mod:** `a-priori` (N hesapla) ve `post-hoc` (gücü hesapla). [DOK: DOK-02]

## 2. Desteklenen analiz türleri

| Tür | Durum |
|---|---|
| `t-paired`, `a-priori` | Hedef. [AÇIK: giriş ve çıktı alanları CONTRACT.md olmadan kesinleşmedi] |
| `t-paired`, `post-hoc` | Hedef. [AÇIK] |
| `t2-indep` | Kapsam dışı; yalnızca karşılaştırma için referans. |
| Diğer aileler | Kapsam dışı. |

## 3. Giriş parametreleri

Adlandırma [DOK: DOK-03] örneğindeki `t2-indep` çağrısından alındı. `t-paired` için bu adların geçerli olup olmadığı [AÇIK].

| Parametre | Anlamı | Tür | Durum |
|---|---|---|---|
| `--test` | Aile adı | metin | `t-paired` olmalı [DOK] |
| `--mode` | `a-priori` veya `post-hoc` | metin | [DOK] |
| `--tails` | `1` veya `2` | tam sayı | [AÇIK] t-paired için tek ve çift kuyruk davranışı gözlenmedi |
| `--d` | Etki büyüklüğü | ondalık | [AÇIK] t-paired için `dz` mi, başka bir tanım mı? |
| `--alpha` | Tip I hata oranı | ondalık | [AÇIK] geçerli aralık belgede yok |
| `--power` | Hedef güç | ondalık | [AÇIK] geçerli aralık belgede yok |
| `--ratio` | Grup oranı | ondalık | [AÇIK] t-paired'da grup kavramı belirsiz |

## 4. Parametre aralıkları ve doğrulama

**[AÇIK]** Tüm aralıklar G*Power'da gözlenerek belirlenecek. Bu tabloyu doldurmak için şunlar yapılmalı: her parametre için sınır değerleri (ör. `alpha` için 0, 1 ve 1'in dışı) girilip G*Power'ın hata ya da kabul davranışı kaydedilmeli.

Şimdilik tek kesin kural [DOK: DOK-04]: geçersiz girdide `{"error":"<açıklama>"}` çıktısı verilir ve çıkış kodu sıfırdan farklıdır.

## 5. İstatistiksel kavramlar

- **Alfa (α):** Tip I hata oranı.
- **Güç (power):** Doğru olan bir alternatifi yakalama olasılığı.
- **Etki büyüklüğü (d):** Ölçeksiz etki büyüklüğü. Hangi tanım kullanıldığı [AÇIK].

**[HİPOTEZ H-S1]:** t-paired için merkezi t dağılımı `df = N − 1` serbestlik derecesiyle, dışmerkez parametre `ncp = dz · √N` ile hesaplanır, `N` çift sayısıdır.
- Durum: Bu bir hipotez. Kaynağı ajanın genel istatistik bilgisidir, bir kılavuz ya da kanıt değildir. [AJAN]
- Doğrulama: G*Power'da aynı girdilerle çalıştırılıp `df` ve `ncp` alanlarıyla karşılaştırılmalı.

## 6. Örneklem büyüklüğü N'nin anlamı

- **[AÇIK]** t-paired'da `N`, çift sayısı mıdır? Yoksa toplam gözlem sayısı (2 × çift) mı? Belirlenmeli.
- Ödev, `N` ve `n1/n2` alanlarının tam eşleşmesini istiyor [DOK: DOK-05]. t-paired için `n1` ve `n2` alanlarının ne anlama geldiği belgede yok.

## 7. Beklenen çıktı alanları

[AÇIK] t2-indep örneğindeki alanlar: `n1`, `n2`, `n_total`, `actual_power`, `critical`, `df`, `ncp` [DOK: DOK-03]. t-paired için hangi alanların çıkacağı, adlarının ne olacağı ve tek grup nedeniyle hangilerinin olmayacağı doğrulanmalı.

## 8. Hata davranışları

- Geçersiz girdi: `{"error":"<açıklama>"}` ve sıfırdan farklı çıkış kodu. [DOK: DOK-04]
- Hangi girdilerin geçersiz sayıldığı [AÇIK].

## 9. Sayısal toleranslar

- `N`, `n1`, `n2`: tam eşleşme. [DOK: DOK-05]
- Diğer değerler: G*Power ekranının gösterdiği basamağa kadar eşleşme. [DOK: DOK-05] Basamak sayısı her alan için ekran görüntüsünden belirlenecek [AÇIK].

## 10. Yuvarlama ve tam sayı N

- G*Power `N`'yi yukarı yuvarlar. Kütüphane (`pwr`, `statsmodels`) kesirli verir. [DOK: DOK-06]
- t-paired için yuvarlama kuralı [AÇIK]. Yukarı yuvarlama yalnızca `N` için mi, `n1/n2` için de mi? Gözlenmeli.

## 11. CLI sözleşmesi

- Tek satır JSON çıktı. [DOK: ödev metni, madde 1a]
- Girdi: yukarıdaki parametreler [AÇIK: t-paired için kesinleşmedi].
- Çıkış kodu: başarı 0, hata sıfırdan farklı.
- `CONTRACT.md` olmadan tam sözleşme yazılamaz. [AÇIK, ENV-08]

## 12. Test senaryoları (Gherkin)

Ödev, kabul kriterlerinin Gherkin biçiminde olmasını istiyor. Değerler G*Power'dan gelmeden tamamlanamaz; şimdilik yalnızca belgeyle kesinleşen senaryolar yazıldı.

```gherkin
Feature: t-paired a priori hesabı

  Scenario: Geçersiz alfa girdisi hata döndürür
    Given aile "t-paired" ve mod "a-priori" seçildi
    When alfa değeri geçersiz bir sayı olarak verilir
    Then çıktı {"error": "<açıklama>"} biçiminde olur
    And çıkış kodu sıfırdan farklıdır
    # Kaynak: DOK-04. Hangi değerin geçersiz olduğu [AÇIK].

  Scenario: Geçerli girdi için N tam sayıdır
    Given aile "t-paired", mod "a-priori", d, alfa ve güç geçerli
    When hesap çalıştırılır
    Then N tam sayıdır
    # Değer [AÇIK]: G*Power'dan alınacak. Kaynak: DOK-05, DOK-06.

  Scenario: Çıktı alanları t-paired için tanımlıdır
    Given geçerli bir t-paired girdisi
    When JSON çıktısı üretilir
    Then çıktı alanları G*Power'ın çıktı alanlarıyla eşleşir
    # [AÇIK]: alan listesi doğrulanmadı.
```

## 13. Sınır durumları (vektör kapsamı)

Ödev sınır değerleri istiyor [DOK: DOK-08]. Şimdilik kapsam listesi:

- `d` çok küçük
- `d` çok büyük
- Güç `α`'ya eşit ya da küçük
- Eşit olmayan oran (yalnızca t-paired için anlamlıysa)
- Geçersiz girdi

Her biri için beklenen değer G*Power'dan gelecek. Ajanın tahmini kullanılmayacak.

## 14. Henüz doğrulanmamış davranışlar (özet)

Bkz. [LEDGER.md](LEDGER.md), bölüm E. Her madde için araştırma yolu:

1. `CONTRACT.md` dosyasını edinmek. [Kullanıcıdan istenecek.]
2. G*Power 3.1.9.7'yi resmi kaynaktan kurup t-paired modunda en az 30 vektör almak.
3. Her vektörün ekran görüntüsünü `oracle/` içine koymak.
4. Yuvarlama ve iterasyon durma koşulunu boundary vektörleriyle gözlemlemek.
5. Geçersiz girdi davranışını (sınır değerleri ve hatalı tipler) gözlemlemek.
6. REA ile bunların her birini `[REA]` olarak LEDGER'a yazmak.
