---
created: 2026-02-28
tags: [LiDAR, Aeva, Sensor, Hardware, FMCW, 4D]
---

# Aeva

AppleやNikonからの出資で知られ、元Appleエンジニアが創業したアメリカのLiDARメーカー。
**FMCW（Frequency Modulated Continuous Wave：周波数変調連続波）技術**に特化しており、各ピクセルごとの距離に加えて「速度（ドップラー効果を利用）」を同時に直接計測できる「4D LiDAR」を世界に先駆けて商用化した。

## 技術的特徴：FMCW 4D LiDAR技術
従来のToF（Time of Flight）方式とは異なり、レーザー光の周波数を変調させながら連続照射する。
- **特長1**: 距離情報とともに瞬時の**速度情報（Velocity）**を直接取得可能。これにより、動的物体か静的物体かの判定が即座にでき、自動運転時の予測精度が飛躍的に向上する。
- **特長2**: 太陽光などの外部環境光や、他のLiDARのレーザー光からの干渉（クロストーク）を原理的に受けない高い堅牢性を誇る。
- **特長3**: フォトニクス技術（Photonic Integrated Circuit）を利用し、チップレベルでの集積化をすすめている。

## 主要製品シリーズ

### Aeries II
世界初となる自動車グレードの4D汎用FMCW LiDAR。主要な光学コンポーネントを単一のシリコンフォトニクスチップに統合している。

- **方式**: FMCW (Frequency Modulated Continuous Wave) 4D LiDAR
- **最大検知距離**: 500m (通常自動車用途では300mレベル)
- **解像度**: 数百万 points per second (可変解像度機能搭載)
- **速度計測範囲**: 瞬時かつ直接的な速度計測機能
- **FOV**: 120°
- **サイズ**: ToFや従来のFMCWと比べてもコンパクト化を達成（チップ型への移行）
- **特徴**: 車両、歩行者、自転車を高精度・長距離から分離・検知する自動運転（L3/L4）での活用が期待される。

### Aeva Atlas
Aeriesをさらに進化させた最新の自動車向け4D LiDARセンサ。超長距離対応やさらなる小型化を目指している。

## Major Customers & Partners
- **Nikon**: FA分野や精密測定など、自動車以外の産業向け応用で協業を展開。
- **Porsche**: 自動車向けLiDARソリューションにAevaを選択。
- **TuSimple / Plus**: 自動運転トラック向けシステムで採用実績。
- **ZF**: 生産・スケーリングにおける戦略的パートナーシップ。
- **Daimler Truck**: 自動運転トラックプログラムでAevaのFMCW LiDARを採用。

## Sources
- [Aeva Official Website](https://www.aeva.com/)
