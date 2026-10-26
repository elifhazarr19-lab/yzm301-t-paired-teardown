# YZM301 Teardown Sprint: t-paired (eşleştirilmiş t testi)

Bu repo YZM301 Yazılım Gerçekleştirme ve Test dersi "Teardown Sprint" ödevi içindir. Ücretsiz istatistiksel güç aracı G*Power'ın eşleştirilmiş t testi (t-paired) davranışını REA ile incelemeyi, kanıtlarını belgelemeyi ve temiz oda yöntemiyle yeniden yazmayı amaçlar.

## Durum (Aşama 1, taslak)

Bu commit yalnızca araştırma ve belge aşamasını içerir:

- **LEDGER.md**: kanıt defteri. Ortam kontrolleri, belgelerden gelen bilgiler `[DOK]` ve REA'dan gözlenen ilk string ve referanslar `[REA]` etiketiyle.
- **SPEC.md**: taslak şartname. Doğrulanmamış her madde `[AÇIK]` veya `[HİPOTEZ]` olarak işaretli.
- **HALLUCINATIONS.md**: araştırma sırasında ortaya çıkan varsayımlar ve açık noktalar.
- **oracle/**: G*Power referans vektörleri için düzen. Henüz gerçek vektör yok.

Henüz yok: G*Power'dan alınmış referans vektörleri, ncp/df formülünün kodda bulunması, temiz oda CLI'si, testler, MCP ve ajan katmanı, demo videosu.

## Dosyalar hakkında

- Repoda G*Power çalıştırılabilir dosyası, arşivi veya decompile çıktısı yoktur.
- LEDGER'daki REA kanıtları yalnızca adres, kısa string ve referans içerir.

## Atıf

G*Power: Faul, F., Erdfelder, E., Lang, A.-G. & Buchner, A. (2007, 2009). Bu çalışma yalnızca eğitim amaçlıdır.
