# oracle/ — G*Power referans vektörleri

**Durum: 0 gerçek vektör.** G*Power bu makinede olmadığı için hiçbir satır G*Power'da çalıştırılmadı.

## Kurallar

1. Bir satır yalnızca G*Power arayüzünde çalıştırıldıktan sonra `verified_by_gpower = yes` olur.
2. Her gerçek satırın bir ekran görüntüsü olur ve `screenshot_path` bu dosyayı gösterir.
3. Sentetik vektörler (scipy, pwr, statsmodels) ayrı bir dosyada tutulur ve asla `verified_by_gpower = yes` olmaz.
4. Sınır vektörleri ayrıca etiketlenir (`category = boundary`).
5. Hedef: en az 30 gerçek G*Power vektörü (ödev madde c).

## Dosyalar

- `t_paired_vectors.csv`: G*Power'dan alınan gerçek referans değerleri (şu an yalnızca başlık).

## Vektör planı (henüz çalıştırılmadı)

| Kategori | Ne test edilecek | Kaynak |
|---|---|---|
| Ana akış | a priori, çift kuyruk, orta etki, α=0,05, güç=0,95 | Ödev sınır listesi |
| Ana akış | Post hoc, aynı girdilerle gücü hesapla | Ödev "Modlar" |
| Sınır | `d` çok küçük | Ödev madde d |
| Sınır | `d` çok büyük | Ödev madde d |
| Sınır | güç ≤ α | Ödev madde d |
| Sınır | tek ve çift kuyruk farkı | [AÇIK] |
| Hata | geçersiz α, güç, d | DOK-04 |

Bu planda hiçbir beklenen sayı yazılmadı. Sayılar G*Power'dan gelecek.
