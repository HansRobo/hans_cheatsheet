---
created: 2026-02-14
tags: [LiDAR, Hesai, Sensor, Hardware]
---

# Hesai Technology

Hesai Technology (禾賽科技) は、グローバルで高いシェアを持つLiDARメーカー。自動運転車、ロボティクス、ADAS向けに高性能なLiDARを提供する。

## Automotive Long-Range (Hybrid / Solid-State)

### AT128
ADAS/自動運転向けの車載グレード長距離LiDAR。多くの量産車に採用されているハイブリッド・ソリッドステートモデル。

- **方式**: Hybrid Solid-State (1D Rotating Mirror + Laser Array)
- **チャンネル数**: 128
- **最大距離**: 200m @ 10% reflectivity (Max 260m)
- **FOV (水平 x 垂直)**: 120° x 25.4°
- **解像度**: 0.1° (H) x 0.2° (V)
- **点群レート**: ~1,536,000 pts/sec (Single Return)
- **サイズ**: 137 x 112 x 48 mm (Compact)
- **消費電力**: ~17 W
- **リリース**: 2021年8月発表, 2022年後半量産開始
- **用途**: Automotive ADAS (Front facing)

### ET25
超薄型設計でフロントガラス裏（キャビン内）への設置に最適化されたモデル。

- **リリース**: 2023年発表 (CES 2024 Innovation Award受賞)
- **方式**: Solid-State
- **高さ**: 25 mm (Ultra-thin)
- **最大距離**: 250m (225m behind windshield @ 10% reflectivity)
- **FOV**: 120° x 25°
- **解像度**: 最少 0.05° x 0.05°
- **動作音**: < 25 dB (静音設計)
- **消費電力**: ~12 W

## Blind Spot / Short-Range (Solid-State)

### FT120
完全ソリッドステートの近距離・死角検知用LiDAR。可動部なし。

- **方式**: Fully Solid-State (Flash technology likely)
- **最大距離**: 100m (30m @ 10% reflectivity estimated)
- **FOV**: 100° x 75° (Ultra-wide)
- **解像度**: 160 (H) x 120 (V) pixels
- **点群レート**: ~192,000 pts/sec
- **用途**: Blind spot detection, Near-field sensing

## Mechanical Spinning LiDAR (Pandar Series)

### Pandar128
L4/L5自動運転開発向けのフラッグシップ機械式LiDAR。

- **リリース**: 2020年9月
- **チャンネル数**: 128
- **最大距離**: 200m @ 10% reflectivity
- **FOV**: 360° x 40° (-25° ~ +15°)
- **解像度**: 0.1° (H) x 0.125° (V)
- **点群レート**: ~3,456,000 pts/sec (Single), ~6,912,000 pts/sec (Dual)
- **用途**: Robotaxi, Autonomous Trucking

### PandarXT (XT-16 / XT-32)
コストパフォーマンスに優れたミドルレンジLiDAR。ロボティクスや産業用途に人気。

- **モデル**: XT-16 (16ch) / XT-32 (32ch)
- **最大距離**: 80m @ 10% reflectivity (Max 120m)
- **FOV**: 360° x 30° (+15° ~ -15°)
- **精度**: ±1 cm (Typical)
- **最小検知距離**: 0.05 m (Zero blind zone range capability)
- **チップセット**: 自社製ASIC搭載で低コスト・高性能化

### PandarQT
超広角垂直FOVを持つ近距離用64チャンネルLiDAR。

- **チャンネル数**: 64
- **最大距離**: 60m (20m @ 10% reflectivity)
- **FOV**: 360° x 104.2° (-52.1° ~ +52.1°)
- **解像度**: 1.45° (V, Finest)
- **用途**: Blind spot coverage, Indoor robotics

## Major Customers
- **Li Auto (理想汽車)**: L9, L8, L7などでAT128を標準採用。
    - 出典: [Hesai Press Release - Li Auto](https://www.hesaitech.com/hesai-lidar-standard-on-li-auto-l9/)
- **Lotus**: Eletre (一部市場/構成) やEmeyaなどで採用。
    - 出典: [Hesai News - Lotus](https://www.hesaitech.com/lotus-eletre-equipped-with-hesai-lidar/)
- **Xiaomi EV**: SU7にAT128を搭載。
    - 出典: [Hesai News - Xiaomi](https://www.hesaitech.com/hesai-lidar-powers-xiaomi-su7/)
- **Changan (長安汽車)**: 複数の新モデルでパートナーシップ。
    - 出典: [Hesai Press Release - Changan](https://www.hesaitech.com/hesai-technology-partners-with-changan-automobile/)
- **NVIDIA**: DRIVE Hyperionプラットフォームのパートナー。
    - 出典: [NVIDIA DRIVE Ecosystem](https://developer.nvidia.com/drive/ecosystem-hesai)

## Sources
- [Hesai Technology Official Website](https://www.hesaitech.com/)
- [Hesai AT128 Product Page](https://www.hesaitech.com/product/at128/)
- [Hesai Pandar Series](https://www.hesaitech.com/product/pandar128/)
- [Hesai FT120 Product Page](https://www.hesaitech.com/product/ft120/)

