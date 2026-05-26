---
title: DDS (Data Distribution Service)
category: ROS
layout: 2017/sheet
tags: [ROS, DDS, ミドルウェア]
updated: 2026-05-26
intro: DDS（Data Distribution Service）の基本機能・QoS・準拠プロファイル・主要実装の対応状況まとめ
---

## DDSとは

- OMG（Object Management Group）が策定する、**データ中心型 Publish-Subscribe（DCPS）** の通信ミドルウェア規格。
- 分散システムのノード間を疎結合・自動発見・QoS制御つきで接続する。中央ブローカ不要のP2P型。
- **ROS 2 の標準通信ミドルウェア層**であり、`rmw`（ROS Middleware）抽象を介して各DDS実装に接続する。
- 関連メモ: [[ROS Context]] / [[rclcpp]]

---

## 基本機能（コア概念）

| 概念 | 役割（軽い説明） |
|------|------|
| **Domain / DomainParticipant** | `domain_id` で区切られた通信空間と、そこへの参加エンティティ |
| **Topic** | 「名前 + データ型」を持つ論理データチャネル |
| **Publisher → DataWriter** | 送信側。Topicへサンプルを書き込む |
| **Subscriber → DataReader** | 受信側。Topicからサンプルを読み取る |
| **型システム（IDL）** | OMG IDLでデータ型を定義し、言語非依存にシリアライズ |
| **Discovery（SPDP / SEDP）** | 参加者・エンドポイントを動的に自動発見（Discovery Serverで集中化も可） |
| **DDSI-RTPS** | ベンダ間相互運用を実現するワイヤプロトコル |
| **WaitSet / Condition / Listener** | データ到着・状態変化を待受け・通知するイベント機構 |
| **Instance / Key** | Keyフィールドで識別されるデータインスタンス（DBの行に相当） |

---

## QoSポリシー（標準22種）

DDSの中核。Writer/Reader間で **RxO（Requested ⇔ Offered）** の互換性が一致しないとマッチしない。

| QoS | 制御内容（1行） |
|------|------|
| **RELIABILITY** | 信頼配送。`BEST_EFFORT` / `RELIABLE` |
| **DURABILITY** | 後から参加したReaderへの過去データ提供。`VOLATILE` / `TRANSIENT_LOCAL` / `TRANSIENT` / `PERSISTENT` |
| **DURABILITY_SERVICE** | TRANSIENT/PERSISTENT用の履歴・リソース設定 |
| **HISTORY** | サンプル保持方式。`KEEP_LAST(depth)` / `KEEP_ALL` |
| **RESOURCE_LIMITS** | 保持できるサンプル・インスタンス数の上限 |
| **DEADLINE** | サンプル更新の最大間隔。超過で通知 |
| **LATENCY_BUDGET** | 配送遅延の許容目安（最適化ヒント） |
| **LIVELINESS** | エンティティ死活監視。`AUTOMATIC` / `MANUAL_BY_*` + lease |
| **LIFESPAN** | サンプルの有効期限。経過後は破棄 |
| **OWNERSHIP** | インスタンス更新権。`SHARED` / `EXCLUSIVE` |
| **OWNERSHIP_STRENGTH** | EXCLUSIVE時に最強Writerを決める強度値 |
| **PARTITION** | Pub/Sub内の論理パーティション名でマッチ範囲を分離 |
| **PRESENTATION** | サンプル提示の範囲・順序・一貫性（access_scope） |
| **DESTINATION_ORDER** | 複数Writer由来サンプルの論理順序。`BY_RECEPTION` / `BY_SOURCE` |
| **TIME_BASED_FILTER** | Reader側で最小受信間隔を設定し間引く |
| **TRANSPORT_PRIORITY** | トランスポート層の優先度ヒント |
| **ENTITY_FACTORY** | 生成エンティティを自動enableするか |
| **USER_DATA / TOPIC_DATA / GROUP_DATA** | 発見時に付帯情報を運ぶユーザ定義データ |
| **READER_DATA_LIFECYCLE** | Readerが保持するインスタンス状態の寿命管理 |
| **WRITER_DATA_LIFECYCLE** | Writer登録解除時のインスタンス自動dispose制御 |

> ROS 2 がプロファイルとして公開するのは **reliability / durability / history / depth / deadline / lifespan / liveliness** の7種が中心。

---

## 拡張機能① — DDS準拠プロファイル

DDS仕様本体（v1.4）が定義する**5つのコンプライアンスポイント**。実装はどこまで満たすかで準拠範囲が決まる。

| プロファイル | 追加される機能（軽い説明） |
|------|------|
| **Minimum Profile** | 基本DCPS + 全QoSの必須部分（上記の土台） |
| **Content-Subscription Profile** | `ContentFilteredTopic`・`QueryCondition`・`MultiTopic` による内容ベース購読・SQL風フィルタ |
| **Persistence Profile** | `DURABILITY` の TRANSIENT / PERSISTENT、`DURABILITY_SERVICE` による永続データ |
| **Ownership Profile** | `EXCLUSIVE` OWNERSHIP と `OWNERSHIP_STRENGTH` による冗長Writerのフェイルオーバ |
| **Object Model Profile** | `MultiTopic` 等の高度なオブジェクトモデル機能 |

---

## 拡張機能② — DDSファミリー仕様

DDS本体を取り巻く関連OMG仕様群。

| 仕様 | 版 | 目的（軽い説明） |
|------|------|------|
| **DDS (DCPS)** | v1.4 | コアのデータ中心Pub/Subモデル |
| **DDSI-RTPS** | v2.5 | ベンダ間相互運用ワイヤプロトコル |
| **DDS-XTypes** | v1.3 | 拡張可能・動的型システム／型の表現とワイヤ表現 |
| **DDS-Security** | v1.2 | 認証・アクセス制御・暗号化（SPIプラグイン構造） |
| **IDL4** | v4.2 | 言語非依存のインタフェース定義言語（ISO/IEC 19516） |
| **IDL4-C++ / Java / C#** | – | IDL4の各言語マッピング |
| **DDS-RPC** | v1.0 | DDS上の言語非依存リモート手続き呼び出し |
| **DDS-XML / DDS-JSON** | v1.0 | QoS・型・エンティティのXML / JSON表現 |
| **DDS-WEB** | v1.0 | WebクライアントからのDDSアクセス |
| **DDS-OPCUA** | v1.0 | OPC UA とのゲートウェイ相互運用 |
| **DDS-XRCE** | v1.0 | リソース制約デバイス向け（micro-ROS / Micro XRCE-DDSの基盤） |
| **DDS-TSN** | – | Time-Sensitive Networking 上での決定論的配送 |

---

## 拡張機能の詳細解説

上の一覧の各項目について、何ができるか・どう使うかを掘り下げる。

### 準拠プロファイル詳細

#### Content-Subscription Profile（内容ベース購読）
Topic全体ではなく「興味のあるサブセット」だけを受け取るための3クラスを追加する。

- **ContentFilteredTopic** — 通常のTopicに **SQL風のフィルタ式**（`WHERE`句相当、例: `temperature > 80 AND room = %0`）を被せた仮想Topic。Reader側で宣言するが、可能なら **Writer側でフィルタ**して不要なサンプルをそもそも送らない（帯域削減）。RTPSのワイヤを通して伝播する。
- **QueryCondition** — 読み取り時に評価されるクエリ条件。`WaitSet` と組み合わせ、「条件に合うサンプルが来たら起床」といった選択的読み取りを行う。Readerに溜まったデータへのフィルタ。
- **MultiTopic** — 複数Topicを **JOIN・射影**して1つの仮想Topicに合成する（リレーショナル風）。最も高度で、多くの実装が未対応（RTI Connextでも限定的）。

> 違い: ContentFilteredTopicは「受信前/受信時の絞り込み」、QueryConditionは「保持済みサンプルへのクエリ」、MultiTopicは「複数ストリームの結合」。

#### Persistence Profile（永続化）
`DURABILITY` を VOLATILE/TRANSIENT_LOCAL より強くし、**Writerプロセスが落ちても過去サンプルを後から参加したReaderへ配送**する。

- **TRANSIENT** — Writerのライフサイクルとは独立した「durability service」（同一プロセス内 or 別デーモン）がメモリ上にサンプルを保持。
- **PERSISTENT** — ディスク等の永続ストレージに保存し、システム再起動をまたいでも提供。
- 保持量・履歴は `DURABILITY_SERVICE` QoS（HISTORY / RESOURCE_LIMITS相当）で制御する。late-joiner（後発参加者）対応の中核。

#### Ownership Profile（所有権と冗長化）
- `OWNERSHIP = EXCLUSIVE` のとき、各インスタンス（Key単位）は **最も `OWNERSHIP_STRENGTH` が高いWriter 1つだけ**が更新できる。
- アクティブなWriterが `DEADLINE` 失効・`LIVELINESS` 喪失などで脱落すると、次に強いWriterへ **自動フェイルオーバ**する。
- 用途: センサ/制御系の **ホットスタンバイ冗長**（主系・従系を同一Topicに出し、Readerは常に最強系のデータを見る）。

#### Object Model Profile
`MultiTopic` など、リレーショナル/オブジェクトモデル寄りの高度機能群。実用上は実装サポートが薄く、利用頻度は低い。

### ファミリー仕様詳細

#### DDS-XTypes（拡張可能・動的型）
型をバージョン進化させても通信を壊さないための仕組み。型ごとに **拡張性種別（extensibility kind）** を宣言する。

| 種別 | 意味 | 互換性 |
|------|------|------|
| **FINAL** | メンバの追加・削除・並べ替え不可 | 送受信で厳密一致が必要 |
| **APPENDABLE** | 末尾へのメンバ追加（または末尾削除）のみ可 | 前方/後方互換（既定値） |
| **MUTABLE** | 各メンバに安定IDを付与し、追加・削除・並べ替えが自由 | 最も柔軟（IDで突き合わせ） |

- **TypeObject / TypeIdentifier** — IDLの代わりに型情報を表現するデータ構造。`MinimalTypeObject`（互換性判定に必要な最小情報）と `CompleteTypeObject`（完全情報）があり、**Discovery時に自動交換**してReader/Writerの **型割当可能性（assignability）** を判定する。
- **XCDR2（Extensible CDR v2）** — 拡張型に対応したワイヤ表現。MUTABLE型はメンバID付きで符号化される。
- **動的型（Dynamic Types）** — 実行時に型を構築・検査するAPI。事前のコード生成なしに未知の型を扱える（汎用ツール・ブリッジで有用）。ROS 2では `rmw_fastrtps_dynamic_cpp` がこれを活用。

#### DDS-Security（5つのSPIプラグイン）
**SPI（Service Plugin Interface）** 構造で、暗号方式や認証基盤を差し替え可能にしている。

| プラグイン | 役割 |
|------|------|
| **Authentication** | 参加者の身元検証。X.509証明書/PKIによる相互認証ハンドシェイクと共有秘密の確立 |
| **Access Control** | 認証済み参加者の権限制御（参加可能ドメイン・Pub/Sub可能Topic）。署名付きの **Governance / Permissions** 文書で定義 |
| **Cryptographic** | 暗号化・復号・ハッシュ・署名（AES-GCM等）。実際の暗号処理を担う |
| **Logging** | セキュリティ関連イベントの監査ログ |
| **Data Tagging** | データサンプルへのセキュリティラベル付与 |

> ROS 2 の **SROS2** はこのDDS-Securityをラップし、鍵・証明書・Governance/Permissionsの生成を自動化する。

#### DDS-RPC（リモート手続き呼び出し）
DDSのPub/Sub上に **Request/Reply（サービス呼び出し）** モデルを構築する仕様。IDLの `interface` でサービスを定義し、内部的にはRequest用/Reply用のTopicペアで実現する。ROS 2のService/Actionは独自実装だが思想的に近い。

#### DDS-XRCE（リソース制約環境向け）
**eXtremely Resource Constrained Environments**。マイコン等の非力なデバイス向けに、**Client ⇄ Agent** モデルを採る。軽量なXRCE Clientがエージェント（フルDDS参加者）経由でDDSネットワークに接続する。**micro-ROS / Micro XRCE-DDS** の基盤技術。

#### DDS-TSN
**IEEE 802.1 TSN（Time-Sensitive Networking）** と組み合わせ、ネットワーク層で帯域予約・時刻同期を行い **決定論的・低遅延な配送** を実現する。車載・産業制御向け。

#### DDS-WEB / DDS-OPCUA / DDS-XML / DDS-JSON
- **DDS-WEB** — REST/WebSocket等でブラウザ・Webクライアントから DDS に読み書きするゲートウェイ仕様。
- **DDS-OPCUA** — 産業オートメーション標準 OPC UA と DDS を相互接続するゲートウェイ。
- **DDS-XML / DDS-JSON** — QoS・型・エンティティ構成を XML / JSON で外部記述する仕様（設定の外出し・ツール連携）。

---

## 主要実装と実装状況

REP-2000 で **Tier 1**（最高位）の3実装が ROS 2 の主力。Tierは Jazzy / Kilted / Rolling 共通。

| 実装 | RMWパッケージ | ライセンス | REP-2000 Tier | XTypes | DDS-Security | Content-Filtered Topic | Discovery Server |
|------|------|------|------|:--:|:--:|:--:|:--:|
| **eProsima Fast DDS** | `rmw_fastrtps_cpp` | Apache-2.0 | **Tier 1**（ROS 2既定） | ✅ | ✅ | ✅ | ✅ |
| **Eclipse Cyclone DDS** | `rmw_cyclonedds_cpp` | EPL-2.0 / EDL | **Tier 1** | ✅ (0.9+) | ✅ | ✅ | －（P2P発見） |
| **RTI Connext DDS** | `rmw_connextdds` | 商用 | **Tier 1**（Ubuntu/Win/macOS） | ✅ | ✅ | ✅ | ✅ |
| GurumNetworks GurumDDS | `rmw_gurumdds_cpp` | 商用 | Tier 3 | ✅ | ✅ | ✅ | 要確認 |
| OpenDDS（参考・非ROS既定） | – | OSS（要CMakeラッパ） | – | ✅ | ✅ | ✅ | － |

凡例: ✅ 対応 / － 非対応・非該当 / 要確認 = 公式情報未確認

### 補足
- **既定実装**: ROS 2 のデフォルトは Fast DDS（`RMW_IMPLEMENTATION=rmw_fastrtps_cpp`）。
- **Tier 2**: `rmw_fastrtps_dynamic_cpp`（XTypes動的型を活用するFast DDSの別ビルド）。
- **Zenoh**: Kilted で `rmw_zenoh_cpp` が Tier 1 入りしたが、これは **DDSではない**別プロトコル（参考）。
- **QoS実装差**: Fast DDS は `DESTINATION_ORDER` / `LATENCY_BUDGET` / `PRESENTATION` / `TIME_BASED_FILTER` / `READER_DATA_LIFECYCLE` / `DURABILITY_SERVICE` を未実装扱い（公式ドキュメント記載）。RTI Connext は商用の参照実装に近く全プロファイルを広くカバー。OpenDDS は「全オプションプロファイル準拠」を公称。
- Cyclone DDS は Fast DDS 型の集中Discovery Serverを持たず、ピア指定によるP2P発見が基本。

---

## 参考リンク

- [REP-2000 — ROS 2 Releases and Target Platforms](https://reps.openrobotics.org/rep-2000/)
- [OMG DDS Specification v1.4](https://www.omg.org/spec/DDS/1.4/)
- [DDS Foundation — What's in the DDS Standard?](https://www.dds-foundation.org/omg-dds-standard/)
- [Fast DDS — Standard QoS Policies](https://fast-dds.docs.eprosima.com/en/latest/fastdds/dds_layer/core/policy/standardQosPolicies.html)
- [Fast DDS — XTypes](https://fast-dds.docs.eprosima.com/en/latest/fastdds/xtypes/xtypes.html)
- [Fast DDS — Discovery Server](https://fast-dds.docs.eprosima.com/en/latest/fastdds/discovery/discovery_server.html)
- [Eclipse Cyclone DDS — QoS](https://cyclonedds.io/docs/cyclonedds/latest/api/qos.html)
- [Eclipse Cyclone DDS — ROADMAP / XTypes](https://github.com/eclipse-cyclonedds/cyclonedds/blob/master/ROADMAP.md)
- [OpenDDS — Introduction（準拠プロファイル）](https://opendds.readthedocs.io/en/latest-release/devguide/introduction.html)
- [RTI Connext — ContentFilteredTopic / QoS Reference](https://community.rti.com/)
- [ROS 2 — About Quality of Service Settings](https://docs.ros.org/en/rolling/Concepts/Intermediate/About-Quality-of-Service-Settings.html)
- [OMG DDS-Security Specification v1.1](https://www.omg.org/spec/DDS-SECURITY/1.1/PDF)
- [Fast DDS — Security（5プラグイン解説）](https://fast-dds.docs.eprosima.com/en/latest/fastdds/security/security.html)
- [ROS 2 — DDS-Security integration（SROS2）](https://design.ros2.org/articles/ros2_dds_security.html)
- [OpenDDS — XTypes（FINAL/APPENDABLE/MUTABLE・TypeObject・XCDR2）](https://opendds.readthedocs.io/en/master/devguide/xtypes.html)
