# resume

## 職歴

---

### 株式会社Timers (2021/07〜2023/03)

---

#### 複数事業にまたがる顧客のクロスユース分析基盤の構築

それぞれの事業部で個別に管理していた顧客データを登録するデータパイプライン 及びデータパイプラインを通して集約されたデータを元に顧客のクロスユース分析に必要な情報を提供するAPIサーバを構築した。

##### チーム構成

- PM: 1〜2人
- エンジニア: 3〜4人

##### 役割

プロジェクトをリードする立場で、技術選定 及び 1つの事業部について実用レベルに至るまでの実装を一人で担当した。
その後は、チームメンバーへの説明を行い、他の事業部についての実装をチームメンバーと共に実施した。

##### 使用技術

- Golang
- AWS ECS
- AWS Lambda
- AWS SNS
- AWS SQS
- AWS RDS

---

#### 外部監査に対応するためのAWS環境の整備

本番/開発環境のアカウントレベルでの分離、AWS Well-Architectedに従ったマルチアカウントの管理、複数のセキュリティサービスが生成する検出情報の一元管理、リリース証跡の検証手順の確立 など、外部監査に対応するために必要なAWS環境の整備を行った。

##### チーム構成

- PM: 1〜2人
- エンジニア: 2〜3人

##### 役割

プロジェクトをリードする立場で、技術選定、技術調査、実施まで一貫して行った。
その後は、ドキュメントの作成を行い、チームメンバーに作業を引き継げる状態とした。

##### 使用技術

- AWS Control Tower
- AWS Security Hub
- AWS GuardDuty

---

### 株式会社シンクロア(現 Kii株式会社) (2010/10〜2021/06)

---

#### 課題管理簿(社外)とissueトラッカー(社内)を連携するシステムの開発 (2011/02〜2011/04)

社外からメールで送信されてくる課題管理簿と社内のissueトラッカーを連携するシステムを開発した。

##### チーム構成

- PM: 1人
- エンジニア: 2〜3人

##### 役割

要求ヒアリング、仕様策定、実装、テストまで全て一人で対応した。
その後は、チームメンバーからのレビューを受けての修正、追加要件への対応を行った。

##### 使用技術

- Python
- Redmine

---

#### テスト実装言語の移行 (2015〜2020)

QAテストを実装するプログラミング言語を、Java => Groovy => Pythonと移行した。

##### チーム構成

- PM: 1人
- エンジニア: 2〜3人

##### 役割

移行するプログラミング言語の選定を行い、移行計画を作成した。
その後は、チーム全員で新しい言語への移行を実施した。

##### 使用技術

- Java
- Groovy
- Python

---

#### デプロイパイプラインによる社内ドキュメントの自動公開 (2021/02〜2021/04)

社内ドキュメントをIP制限をかけて公開した上で、ドキュメントの変更を自動で反映するようにした。

##### チーム構成

- PM: 1人
- エンジニア: 2〜3人

##### 役割

プロジェクトをリードする立場で、技術選定 及び 実用レベルに至るまでの実装を担当した。
その後は、ドキュメント作成などを行い、チームでの運用態勢を確立した。

##### 使用技術

- Terraform
- Kubernetes
- GCP

---

#### CI環境の整備 (2015/04〜2019/05)

QAテストを実行するCI環境のInfrastructure as Code(IaC)、クラウド上への移行を実施した。

##### チーム構成

- PM: 1人
- エンジニア: 2〜3人

##### 役割

プロジェクトをリードする立場で、技術選定 及び 実用レベルに至るまでの実装を担当した。
その後は、ドキュメント作成などを行い、チームでの運用態勢を確立した。

##### 使用技術

- Ansible
- Terraform
- Docker
- GCP

---

### 株式会社NTTデータ (2009/04〜2010/09)

---

#### 大規模データの分散処理フレームワークの研究調査 (2009/10〜2010/03)

大規模データの分散処理フレームワークである『Hadoop』の研究調査 及び 報告書作成を行うプロジェクトに参加した。

##### チーム構成

- PM: 2〜3人
- エンジニア: 5〜6人

##### 役割

Hadoop管理ノードの冗長化に関する調査を担当した。

##### 使用技術

- Java
- Hadoop
- [DRBD](https://github.com/LINBIT/drbd): データを冗長化するミドルウェア
- [Heartbeat(現Pacemaker)](https://github.com/ClusterLabs/pacemaker): サーバプロセスを冗長化するミドルウェア

---

## 個人での経験

- オープンソースへのコミット
   - [Github PR](https://github.com/pulls?q=is%3Apr+author%3AFGtatsuro+-org%3AFGtatsuro)
   - [Vim Patch](https://github.com/vim/vim/commit/4f8301f6415e86631dadbc19066ba0bc8550df49)
      - Githubでホスティングされるより前にメーリングリストに投稿したパッチに相当するコミット
- Neovimプラグイン
   - [Scrapboxにバッファの内容を投稿するプラグイン](https://github.com/FGtatsuro/scrapbox.nvim)
   - [バッファで開いているファイルをGithubのWebUIで閲覧するプラグイン](https://github.com/FGtatsuro/github.nvim)
- Ansible
   - [Roleリポジトリ](https://github.com/FGtatsuro?tab=repositories&q=ansible&type=&language=)
   - [Ansible Galaxy](https://galaxy.ansible.com/FGtatsuro)
- 競技プログラミング
   - [AtCoderユーザーページ](https://atcoder.jp/users/fgtatsuro)
   - [解答した問題のコード](https://github.com/FGtatsuro/myatcoder)
- 執筆
   - [Hadoop徹底入門 第2版 オープンソース分散処理環境の構築](https://www.amazon.co.jp/dp/479812964X)

## その他

- [インフラ構築](./infra.md)
- [社内システム/ツール開発](./for_company.md)
- [QA](./qa.md)
- [チームへのスクラム導入](./management.md)
