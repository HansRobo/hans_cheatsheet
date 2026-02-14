---
created: 2024-01-11 03:00:17
tags: [LiDAR, RoboSense, Sensor, Hardware]
---

# RoboSense (Suteng Innovation Technology)

RoboSense (Suteng Innovation Technology) は、深圳を拠点とするLiDARセンサーメーカー。機械式LiDARからMEMSソリッドステートLiDARまで幅広い製品ラインナップを持つ。

## Solid-State LiDAR (MEMS)

車載グレードのMEMSミラー方式LiDAR。

### RS-LiDAR-M3 (New!)
CES 2024で発表されたMプラットフォームの次世代超長距離モデル。

- **リリース**: 2024年発表
- **波長**: 940 nm
- **最大距離**: 300m @ 10% reflectivity
- **FOV**: 120° x 25°
- **解像度**: 0.05° x 0.05° (ROI equivalent to 500 beams)
- **特徴**: 従来の1550nm製品に対し、940nm技術で同等の性能を低コスト・低消費電力・小型サイズで実現。
- **用途**: L3+ Autonomous Driving (Highway pilot at 120km/h)
- **出典**: [RoboSense M3 Press Release](https://www.robosense.ai/en/news-view-100) (CES 2024 Launch)

### RS-LiDAR-M1
世界初の車載グレード量産MEMS LiDAR。

- **方式**: MEMS Solid-State
- **波長**: 905nm (推定)
- **最大距離**: 200m (150m @ 10% reflectivity)
- **FOV (水平 x 垂直)**: 120° x 25°
- **解像度 (水平 x 垂直)**: 0.2° x 0.2° (average)
- **点群レート**: ~750,000 pts/sec (Single), ~1,500,000 pts/sec (Dual)
- **サイズ / 重量**: コンパクト設計
- **データポート**: 1000 Mbps Ethernet

- **リリース**: 2021年6月 (Mass Production Start)
- **用途**: Automotive ADAS, Autonomous Driving

### RS-LiDAR-M2 / M2 Plus
M1の進化版。M Platformファミリー。

- **リリース**: M1の後継として順次展開
- **方式**: MEMS Solid-State (2D mechanical scanning described in some contexts)
- **最大距離**:
    - M2: 200m
    - M2 Plus: 300m
- **FOV (水平 x 垂直)**:
    - M2: 360° x 30° ではなく、通常は前方監視型。資料によっては360度メカニカルとしての記述と混同される場合あり。※要確認: Mシリーズは通常Sector LiDAR。
    - *Correction*: Mシリーズは通常前方監視用。360度は回転式。
- **点群レート**:
    - M2: ~1,500,000 pts/sec
    - M2 Plus: >2,500,000 pts/sec
- **用途**: Automotive

## Mechanical Spinning LiDAR

### RS-Helios Series
新世代の機械式LiDAR。近距離の不感帯を減らした設計などが特徴。

#### RS-Helios-16P
- **リリース**: 2021年10月 (Helios-5515発表時期)
- **ビーム数**: 16
- **最大距離**: 150m (110m @ 10% reflectivity)
- **FOV**: 360° x 30° (-15° ~ +15°)
- **精度**: Up to 1 cm
- **点群レート**: ~576,000 pts/sec (Dual Return)
- **接続**: 100Base-T1 (Automotive Ethernet)
- **保護等級**: IP67

#### RS-Helios-5515
- **ビーム数**: 32
- **最大距離**: 150m (80m @ 10% reflectivity)
- **FOV**: 360° x 70° (-55° ~ +15°)
- **特徴**: 垂直70度の広視野角により、車両直近の死角を大幅に削減。
- **点群レート**: ~1,152,000 pts/sec (Dual Return)

### RS-LiDAR-16
定番の16線LiDAR。Velodyne VLP-16の競合。

- **リリース**: 初期モデルとしてはRoboSenseの最初期製品の一つ
- **ビーム数**: 16
- **最大距離**: 150m (80m @ 10% reflectivity)
- **FOV**: 360° x 30° (+15° ~ -15°)
- **解像度**: 垂直 2.0°
- **精度**: ±2 cm (Typical)
- **点群レート**: ~300,000 pts/sec (Single), ~600,000 pts/sec (Dual)
- **回転速度**: 300/600/1200 rpm (5/10/20 Hz)
- **接続**: 100 Mbps Ethernet

### RS-LiDAR-32
32線モデル。高密度な点群が必要なロボティクス用途など。

- **ビーム数**: 32
- **最大距離**: 200m (150m @ 10% reflectivity)
- **FOV**: 360° x 40° (+15° ~ -25° などのバリエーションあり)
- **解像度**: 垂直 最少0.33° (Middle part)
- **点群レート**: ~600,000 pts/sec (Single), ~1,200,000 pts/sec (Dual)
- **精度**: ±3 cm (Typical)

## Short-Range / Blind Spot LiDAR

### RS-Bpearl
半球状の超広角FOVを持つ近距離LiDAR。ロボットや車両の死角検知用。

- **方式**: Mechanical Spinning (Super-wide FOV)
- **最大距離**: 100m (30m @ 10% reflectivity)
- **FOV**: 360° x 90°
- **最小検知距離 (Blind spot)**: < 0.1 m
- **点群レート**: ~576,000 pts/sec (Single), ~1,152,000 pts/sec (Dual)
- **用途**: Low-speed logistics robots, Blind spot detection
- **出典**: [RoboSense RS-Bpearl Product Page](https://www.robosense.ai/en/rslidar/RS-Bpearl)

## Major Customers
- **BYD**: 複数の車種で採用 (e.g., YangWang U8, Denza N7)。
    - 出典: [RoboSense Press Release - BYD Partnership](https://www.robosense.ai/en/news-view-100)
- **Lotus**: Eletreなどのモデルに搭載。
    - 出典: [RoboSense Press Release - Lotus Eletre](https://www.robosense.ai/en/news-view-89)
- **Lucid Motors**: Lucid Airへの搭載。
    - 出典: [RoboSense News](https://www.robosense.ai/en/news-view-68)
- **XPeng**: G9などでMシリーズを採用。
    - 出典: [RoboSense News](https://www.robosense.ai/en/news-view-85)
- **Toyota (FAW Toyota)**: bZ4X robotaxi projectなどで協力。
    - 出典: [RoboSense News](https://www.robosense.ai/en/news-view-96)

## Sources
- [RoboSense Official Website](https://www.robosense.ai/en)
- [RoboSense M Platform](https://www.robosense.ai/en/rslidar/RS-LiDAR-M1)
- [RoboSense Helios Series](https://www.robosense.ai/en/rslidar/RS-Helios)
- [RoboSense Mechanical Series](https://www.robosense.ai/en/rslidar/RS-LiDAR-16)

