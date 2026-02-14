---
created: 2026-02-14
tags: [LiDAR, Livox, Sensor, Hardware]
---

# Livox Technology

Livoxは、DJIの関連会社として設立されたLiDARメーカー。独自の非反復走査パターン（Non-repetitive Scanning）技術により、低コストかつ高密度な点群取得を実現している。

## Industrial / Robotics / Mapping

### Mid-360
360度FOVを持つコンパクトなLiDAR。ロボティクスや産業用途に特化。

- **リリース**: 2023年1月
- **方式**: 3D Spinning (Non-repetitive)
- **最大距離**: 70m @ 80%, 40m @ 10% reflectivity
- **FOV**: 360° x 59° (-7° ~ +52°)
- **点群レート**: 200,000 pts/sec (Single)
- **最小検知距離**: 0.1m
- **サイズ**: 65 x 65 x 60 mm (Ultra-compact)
- **重量**: 265g
- **出典**: [Livox Mid-360 Product Page](https://www.livoxtech.com/mid-360)

### Mid-70
垂直視野角を広げた近距離・死角検知向けモデル。

- **最大距離**: 260m @ 80%, 90m @ 10% reflectivity
- **FOV**: 70.4° (Circular)
- **最小検知距離**: 0.05m
- **精度**: ≤ 2 cm
- **用途**: Blind spot detection, Low-speed robotics
- **出典**: [Livox Mid-70 Product Page](https://www.livoxtech.com/mid-70)

### Avia
ドローン搭載や測量・マッピング向けの軽量・高性能モデル。

- **最大距離**: 450m @ 80%, 190m @ 10% reflectivity
- **FOV**:
    - Non-repetitive: 70.4° x 77.2°
    - Repetitive: 70.4° x 4.5°
- **点群レート**: Max 720,000 pts/sec (Triple return)
- **重量**: 498g
- **用途**: Mapping, Power line inspection
- **出典**: [Livox Avia Product Page](https://www.livoxtech.com/avia)

## Automotive Grade

### HAP (Horizon Automotive Product)
車載グレードの量産向けLiDAR。Xpengなどの市販車に採用実績あり。

- **リリース**: 2021年量産開始 (Xpeng P5搭載), 2022年7月一般受注開始
- **方式**: Rotating Mirror (Livox customized)
- **最大距離**: 150m @ 10% reflectivity
- **FOV**: 120° x 25°
- **解像度**: 0.18° x 0.23°
- **点群レート**: ~452,000 pts/sec (Single)
- **サイズ**:
    - HAP (T1): 105 x 131.6 x 65 mm
    - HAP (TX): 116 x 116 x 76 mm
- **出典**: [Livox HAP Product Page](https://www.livoxtech.com/hap)

## Major Customers
- **XPeng (小鵬汽車)**: P5などにHAP (Horizon) を採用。世界初の量産車搭載事例の一つ。
    - 出典: [Livox Press Release - Xpeng](https://www.livoxtech.com/news/12)
- **DJI**: 親会社/関連会社であり、ドローン（Matriceシリーズ等）やEcosystemで採用。
    - 出典: [DJI Enterprise](https://enterprise.dji.com/)
- **Kodiak Robotics**: 自動運転トラックのカバレッジ補完などに採用事例あり。
    - 出典: [Kodiak Robotics Blog](https://kodiak.ai/blog/)
