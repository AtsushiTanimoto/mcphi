# Verner の光電離断面積のフィット

D. A. Verner の `phfit2.f` (Version 2, 1996-03-25) の `DATA` 文の係数をそのまま表にしたもの (2026-11-18 に HEASoft 6.37.1 の
`Xspec/src/XSFunctions/phfit2.f` から抽出。FAC の `ionis/phfit2.f` の係数と同一)。H〜Zn (Z = 1〜30) の全イオンの基底状態。

- `ph1.tsv`: 殻ごとのフィット (Verner & Yakovlev 1995, A&AS, 109, 125)。殻番号は 1〜7 = 1s, 2s, 2p, 3s, 3p, 3d, 4s。
  列: Z, 電子数, 殻, 閾値 E_th [eV], E0 [eV], σ0 [Mb], y_a, P, y_w。
  σ = σ0 [(y − 1)² + y_w²] y^(0.5P − l − 5.5) (1 + √(y/y_a))^(−P)、y = E/E0 (E ≥ E_th)。
- `ph2.tsv`: Opacity Project の断面積へのフィット (Verner, Ferland, Korista & Yakovlev 1996, ApJ, 465, 487)。外側の殻の合計。
  列: Z, 電子数, E0 [eV], σ0 [Mb], y_a, P, y_w, y0, y1。
  σ = σ0 [(x − 1)² + y_w²] y^(0.5P − 5.5) (1 + √(y/y_a))^(−P)、x = E/E0 − y0、y = √(x² + y1²)。
  内殻 (電子数 3〜10 は 1s、11〜18 は 2p、19 以上は 3p) の閾値未満で使い、それ以上では `ph1.tsv` の殻ごとの値を使う。

`source/atomic_data.py` の `load_verner_valence_table()` が `constants.VERNER_VALENCE_IONS` のイオンの価電子の断面積に使う。
