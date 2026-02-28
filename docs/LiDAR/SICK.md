---
created: 2026-02-28
tags: [LiDAR, SICK, Sensor, Hardware, Industrial, FA]
---

# SICK

ドイツを拠点とする世界的な産業用センサーメーカー。AGV（無人搬送車）やAMR（自律移動ロボット）、ファクトリーオートメーション（FA）、安全管理（セーフティ）向けの2D/3D LiDARおよびレーザスキャナ市場で圧倒的なシェアを持つ。

## 主要製品シリーズ

### TiMシリーズ
小型・軽量・低消費電力で、屋内外のモバイルロボット（AGV/AMR）や侵入検知向けの主力2Dレーザスキャナ。

- **最大距離**: 10m ~ 25m (モデルによる, e.g., TiM5xx)
- **FOV**: 270°
- **スキャン周波数**: 15 Hz ~ 25 Hz
- **インターフェース**: Ethernet, USB
- **特徴**: ROSドライバなどのサポートが充実しており、研究開発から量産まで幅広く活用されている。[TiM581]などの型番が代表的。

### LMSシリーズ
中長距離向けで、屋外環境にも強く、港湾、交通、監視、大型AGVなどで使用される高性能2Dレーザスキャナ。

- **最大距離**: 20m ~ 80m+ (LMS1xx, LMS5xx)
- **FOV**: 270° / 190° 等（モデルによる）
- **スキャン周波数**: 25 Hz ~ 100 Hz
- **特徴**: 悪天候（雨、霧、雪）に強いマルチエコー技術を搭載。

### セーフティレーザスキャナ (microScan3 / S3000)
人協働ロボットやAGVの安全防護領域（セーフティゾーン）を設定・監視するための機能安全認証（SIL, PL）を取得したモデル。

- **microScan3**: 最新世代のセーフティレーザスキャナ。safeHDDMスキャン技術により、汚れや外乱光に対して非常に強い耐性を持つ。保護フィールド範囲は最大9m（モデルによる）、スキャン角度 275°。
- **用途**: AGVの衝突防止、産業用ロボットの周囲安全確保。

## メカニズム・技術
- **Time-of-Flight (ToF)**: ほとんどの製品は2Dの回転ミラーを用いたToF方式を採用。
- **HDDM (High Definition Distance Measurement)**: 光のパルスを連続して多重に照射し、平均化等を行うことで測定の確実性を高めるSICK独自の技術。
- **ROS対応**: 公式またはコミュニティ製の `sick_scan` や `sick_tim` パッケージが提供されており、ROS 1 / ROS 2環境で非常に扱いやすい。

## Major Customers & Partners
- 世界中の製造業、物流システム構築メーカー、ロボティクス関連企業（KUKA, Omron, MiR (Mobile Industrial Robots) をはじめとする各種AGV/AMRメーカーなど）。

## Sources
- [SICK LiDAR Sensors](https://www.sick.com/ag/en/lidar-sensors/c/g177111)
- [SICK Safety Laser Scanners](https://www.sick.com/ag/en/safety-laser-scanners/c/g115933)
