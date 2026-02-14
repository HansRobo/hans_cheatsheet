---
created: 2026-02-14
tags: [LiDAR, Ouster, Velodyne, Sensor, Hardware]
---

# Ouster (inc. Legacy Velodyne)

OusterはデジタルLiDAR技術（SPAD + VCSEL）を特徴とするメーカー。2023年にVelodyne Lidarと合併し、Velodyneの製品ラインもサポートしている（一部はLast Time BuyまたはEoL）。

## Ouster Digital LiDAR (REV7 Series)
Ousterの現行主力製品。デジタルアーキテクチャによる高い信頼性と、L3チップ搭載による高性能が特徴。

### OS1 (Mid-Range)
バランスの取れたミッドレンジモデル。自動運転、ロボティクス、マッピングなど多用途。

- **リリース**: REV7は2022年10月発表、2022年Q4出荷開始
- **方式**: Digital Flash (SPAD + VCSEL) w/ Spinning mechanism
- **チャンネル数**: 32 / 64 / 128
- **最大距離**: 200m+ (90m @ 10% reflectivity)
- **FOV**: 360° x 45°
- **点群レート**: ~5,242,880 pts/sec (Max)
- **接続**: Gigabit Ethernet
- **保護等級**: IP68, IP69K
- **出典**: [Ouster OS1 Product Page](https://ouster.com/products/hardware/os1-lidar-sensor)

### OS0 (Ultra-Wide)
超広角FOVを持つ近距離・ナビゲーション・障害物回避向け。

- **最大距離**: 100m+ (35m @ 10% reflectivity)
- **FOV**: 360° x 90° (Vertical 90°!)
- **チャンネル数**: 32 / 64 / 128
- **用途**: Autonomous Mobile Robots (AMR), Indoor mapping
- **出典**: [Ouster OS0 Product Page](https://ouster.com/products/hardware/os0-lidar-sensor)

### OS2 (Long-Range)
高速自動運転向けの長距離モデル。

- **最大距離**: 400m+ (200m @ 10% reflectivity)
- **FOV**: 360° x 22.5°
- **チャンネル数**: 64 / 128
- **出典**: [Ouster OS2 Product Page](https://ouster.com/products/hardware/os2-lidar-sensor)

## Legacy Velodyne Products
現在はOuster傘下。市場に広く普及している定番モデル。新規採用はOusterシリーズへの移行が推奨される場合がある。

### VLP-16 (Puck)
LiDARの代名詞的存在。研究開発から製品まで幅広く利用されている。

- **リリース**: 2014年発表、2016年頃から広く普及
- **方式**: Mechanical Spinning
- **チャンネル数**: 16
- **最大距離**: 100m (Typical)
- **FOV**: 360° x 30° (+15° ~ -15°)
- **解像度**: 2.0° (Vertical)
- **点群レート**: ~300,000 pts/sec (Single), ~600,000 pts/sec (Dual)
- **精度**: ±3 cm
- **出典**: [Velodyne VLP-16 Datasheet](https://velodynelidar.com/products/puck/)

### VLP-32C (Ultra Puck)
32チャンネルの高解像度モデル。

- **チャンネル数**: 32
- **最大距離**: 200m
- **FOV**: 360° x 40° (+15° ~ -25°)
- **精度**: ±3 cm
- **出典**: [Velodyne Ultra Puck Datasheet](https://velodynelidar.com/products/ultra-puck/)

### VLS-128 (Alpha Prime)
長距離・高解像度のハイエンドモデル。

- **チャンネル数**: 128
- **最大距離**: 300m (245m typical)
- **FOV**: 360° x 40°
- **解像度**: 0.11° (Vertical Min)
- **用途**: Highway Autonomous Driving
- **出典**: [Velodyne Alpha Prime Datasheet](https://velodynelidar.com/products/alpha-prime/)

## Major Customers & Partners
- **Industrial / Robotics Focus**: Factory automation, AGVs, AMRs.
    - 出典: [Ouster Industrial Page](https://ouster.com/industries/industrial)
- **Serve Robotics**: Uber Eatsなどの配送ロボットに採用。
    - 出典: [Ouster Press Release](https://ouster.com/company/press/serve-robotics-selects-ouster-lidar-for-next-generation-delivery-robots)
- **Motional**: Robotaxi (Legacy Velodyne partnership).
    - 出典: [Velodyne Press Release](https://velodynelidar.com/press-release/motional-selects-velodyne-lidar-for-driverless-vehicles/)
- **May Mobility**: Autonomous shuttles.
    - 出典: [Ouster Press Release](https://ouster.com/company/press/may-mobility-selects-ouster-lidar)

## Sources
- [Ouster Official Website](https://ouster.com/)
- [Velodyne Lidar (Legacy)](https://velodynelidar.com/)
