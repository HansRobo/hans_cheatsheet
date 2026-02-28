---
created: 2026-02-28
tags: [LiDAR, LeddarTech, Sensor, Software, SensorFusion, LeddarVision]
---

# LeddarTech

カナダ・ケベック州に本社を置く企業。元々は自動運転やADAS向けのソリッドステートLiDARセンサ及び関連技術（LeddarEngineなど）を開発・製造するハードウェアメーカーとしてスタートしたが、近年は**センサフュージョンと認識システム（知覚）に特化したソフトウェア企業**へと大きくビジネスモデルを転換（ピボット）している。

## 技術と事業転換

> [!NOTE] ソフトウェア企業への転換
> LeddarTechはハードウェア（LiDARモジュールそのもの）の製造から距離を置き、現在は「ローレベル・センサフュージョン＆認識ソフトウェア」である **LeddarVision™** のライセンス提供を中心とするビジネスモデルに集中しています。カメラ、レーダー、LiDARから得られる生データ（ローレベルデータ）を融合し、高精度の環境認識を実現します。

### LeddarVision™ (主力ソフトウェア)
Tier 1/2サプライヤーや自動車メーカー（OEM）向けに提供される、ADAS（先進運転支援システム）および自動運転（AD）向けのローレベルセンサーフュージョン・知覚ソフトウェア環境。

- **ローレベルフュージョン**: 各センサー（カメラ、レーダー、LiDAR）が物体を「認識（オブジェクト化）」する前の「生データ（ピクセル、ポイントクラウド、レーダーヒット）」の段階でデータを統合するアプローチ。
- **利点**: 各センサーが内部処理で破棄してしまう微小な情報を総合的に評価できるため、悪天候下（雪道、濃霧）や複雑な環境（センサーが個別では物体の確信度を低くみる状況）でも、システム全体として極めて高い信頼性の認識・トラッキングが可能。
- **対象レベル**: L2 / L2+ / L3 / L4 システム向け。

### LeddarEngine™ / LeddarCore (SoC & IP)
もともとのコア技術であったLiDAR信号処理技術。フラッシュLiDARなどに用いられる。
- **LCA3など**: Tier 1やLiDARメーカーが低コストなソリッドステートLiDARを独自開発できるようにするためのシステム・オン・チップ（SoC）および信号処理ソフトウェアのライセンス（IP）提供。

## これまでの主要ハードウェア製品（従来ビジネス）
産業用・交通・モビリティ向けの完成品LiDARセンサモジュール。

- **Leddar Pixell**:
  - 自動運転シャトル/ロボタクシーなどの近接監視・死角検知向け3Dソリッドステート（フラッシュ）LiDAR。
  - **FOV**: 180° x 16°
  - 可動部ゼロ、高耐久性（耐振動性）。
- **Leddar M16**:
  - 16セグメントの2D/3DフラッシュLiDARモジュール。産業・ドローン高度計・交通監視などで利用。

## Major Customers & Partners
- **ARM / TI / Renesas / NXP**: SoC環境へのLeddarVisionコンポーネントの最適化・実装においてMCUベンダーと提携。
- **Ficosa / Visteon**: Tier 1向けADASシステム統合などを志向。

## Sources
- [LeddarTech Official Website](https://leddartech.com/)
- [LeddarVision Technology Overview](https://leddartech.com/solutions/leddarvision-sensor-fusion-perception/)
