# resume

## エンジニアとしての方向性

**技術者として常に成長し続けたい**

一技術者として、サービスで使われているありとあらゆる技術を学び続けていきたい。
計算機科学や数学の基礎知識、トレンドの技術、共に学習し続け、結果としてチームや会社に貢献できるようになりたい。

## エンジニアとしての強み

**読む力: 公式ドキュメント、ソースコード、仕様を読み込んで得た情報から、検証を行い解答を導き出す力**

## 技術スタック

<p>
  <img src="https://img.shields.io/badge/-Golang-F0FFF0.svg?logo=Go&style=plastic">
  <img src="https://img.shields.io/badge/-TypeScript-FFFFE0.svg?logo=TypeScript&style=plastic">
  <img src="https://img.shields.io/badge/-Python-FFD700.svg?logo=Python&style=plastic">
  <img src="https://img.shields.io/badge/-Java-000000.svg?logo=OpenJDK&style=plastic">
  <img src="https://img.shields.io/badge/-Groovy-E6E6FA.svg?logo=Apache%20Groovy&style=plastic">
</p>

<p>
  <img src="https://img.shields.io/badge/-AWS-FFA500.svg?logo=Amazon%20AWS&style=plastic">
  <img src="https://img.shields.io/badge/-GCP-F8F8FF.svg?logo=googlecloud&style=plastic">
  <img src="https://img.shields.io/badge/-Docker-F0F8FF.svg?logo=Docker&style=plastic">
  <img src="https://img.shields.io/badge/-Terraform-FFF0F5.svg?logo=Terraform&style=plastic">
</p>

---

## 現状持っていない経験・スキル

**(注) 本ドキュメントを採用目的で閲覧する場合、ミスマッチを防ぐために必ず目を通して頂けますようお願いします**

以下の経験・スキルは現状持っていないため、キャッチアップに一定の時間を要します。

### 大規模システムの設計・実装・運用

今までの経験が、社内システム または 小規模な公開システム に限られていたため、以下に示すような事柄は知識として多少抑えているものの、実務経験がありません。

- 大規模トラフィックを捌くためのアプリケーション・インフラ設計
- データベースのパフォーマンスチューニング
- 監視設計

### リーダー経験

今までの経験が『少人数のチームで各自がアサインされたタスクをこなしていく』というスタイルに偏っていたため、その過程で技術選定を行った経験はあるものの、明確にテックリードとしての役割を遂行した経験はありません。
『新しい技術やサービスの導入可能性を探るためにPoCを実施、結果をチームで共有、議論の上で導入する』という経験は何回かありましたが、これもテックリードとしてふるまったというには弱いと考えています。

またヒューマンマネジメントに類する経験はほとんどありません。

### 学術レベルの計算機科学の知識

競技プログラミングはやっていたものの、AtCoderのランクは緑色にとどまっており、業務に生かせるレベルには達していません。

---

## 職歴

**『詳細』をクリックすることで、各プロジェクトの詳細情報を閲覧できます**

---

### 株式会社Timers (2021/07〜2023/03): バックエンドエンジニア

---

#### 複数事業にまたがる顧客のクロスユース分析基盤の構築 (2022/05〜2022/11)

それぞれの事業部で個別に管理していた顧客データを登録するデータパイプラインを作成した。
またデータパイプラインを通して集約されたデータを元に顧客のクロスユース分析に必要な情報を提供するAPIサーバを構築した。

##### チーム構成

- PM: 1〜2人
- エンジニア: 3〜4人

##### 役割

プロジェクトをリードする立場で、技術選定 及び 1つの事業部について実用レベルに至るまでの実装を一人で担当した。
その後は、チームメンバーへの説明を行い、他の事業部についての実装をチームメンバーと共に実施した。

##### 技術スタック

- Golang
- AWS
   - ECS
   - Lambda
   - SNS
   - SQS
   - RDS
   - CDK

<details>
<summary><strong>詳細</strong></summary>

##### 課題

各事業部毎に顧客データを様々な場所に(ex. RDS、スプレッドシート)、様々なフォーマットで管理していた。
クロスユース分析を行う際には、これらのデータを手動でスプレッドシートにコピーした上で、ユーザ毎のデータを集計していた。

##### 解決策

各事業部のデータソースを登録するためのデータパイプラインを実装した。
データパイプラインは、『ブリッジ』『イベントローダ』『APIサーバ』の3つのコンポーネントから成り立つ。

【ブリッジ】

ブリッジは、各サービスで登録された顧客データを、イベントローダが解釈可能なメッセージに変換した上で、イベントローダのインターフェースとなるSNSに送信する。

ブリッジは、データソース毎に異なる実装を持たせた。これはデータソース毎の違いを吸収するためである。
例えば、データソースがWebサービス化されている場合は、SQSとLambdaを用いてリアルタイムにデータ登録を行う。一方、データソースがスプレッドシートの場合は、LambdaとEventBridgeを用いて日時でデータ登録を行う。

【イベントローダ】

イベントローダは、ブリッジから受信したメッセージを元に登録APIを実行する。

イベントローダはブリッジからのメッセージを受信するSNS、SNSからメッセージを受け取りデータを処理するSQSとLambdaにより構成される。
SNSのメッセージフィルターを使って事業部毎に異なるLambdaが呼び出す事により、データソース毎に異なる処理を実行できるようにした。

【APIサーバ】

APIサーバは、イベントローダから呼び出される登録API、及び登録したデータを参照する参照APIを持つ。

クロスユース分析を実現するためには名寄せが必要だったため、Eメールを用いて名寄せした。
登録時に複数の事業部で同じEメールを用いた顧客が存在した場合、APIサーバ上では単一のユーザとみなされる。

また、Eメールをキーとして検索APIを実行することで、顧客が利用している事業部(=サービス)を取得できるようにレスポンスを設計した。
取得したデータには登録日時が含まれており、クロスユース分析をする際に必要な情報を提供する。

##### 技術選定

『Golang』で実装したAPIサーバを『ECS』でデプロイするという組み合わせは、既に社内で実績があったため、同じ構成であれば大きな問題にはならないだろうと判断して採用した。

一方、各種AWSリソースの作成には社内で実績がまだない『AWS CDK』を採用することとした。
私自身がまだAWSに不慣れであり、Terraform/CloudFormation など抽象度の低いIaCツールでは構築が難しいのではないかと考えた。
一方、CDKであれば抽象度の高いL2、L3コンストラクタを使う事で素早く構築できる、ドキュメントやCDK自体のコードを読む事でAWSに関する知識も得る事が期待できた。

##### 成果

顧客データが一箇所に集約されてAPIで取得できるようになったことにより、クロスユース分析の手順が省力化された。

##### 工夫した点

リアルタイムにデータ登録を行うブリッジには、データの検証及び補正を行うバッチを日時で実行するようにした。
これにより、ブリッジからイベントローダへのメッセージ送信が何らかの理由で失敗しても、手動での修正が不要になった。

</details>

---

#### セキュアに複数のAWSアカウントを扱うための環境整備 (2022/12〜2023/01)

Well-Architectedに従ったマルチアカウントの管理、複数のセキュリティサービスが生成する検出情報の一元管理 など、
セキュアに複数のAWSアカウントを扱うための環境整備を行った。

##### チーム構成

- PM: 1〜2人
- エンジニア: 2〜3人

##### 役割

プロジェクトをリードする立場で、技術選定、技術調査、実施まで一貫して行った。
その後は、ドキュメントの作成を行い、チームメンバーに作業を引き継げる状態とした。

##### 技術スタック

- AWS
   - Control Tower
   - Organizations
   - Security Hub
   - GuardDuty

<details>
<summary><strong>詳細</strong></summary>

##### 課題

セキュリティ観点から、1つのAWSアカウントに同居している本番環境と開発環境をアカウントレベルで分離したいという要求があった。

##### 解決策

Well-Architectedに従ったマルチアカウント環境を作成するマネージドサービスであるControl Towerを導入した。
Control Tower導入後、本番環境を含むAWSアカウント、用意はされていたが使われていない開発用のAWSアカウントをそれぞれControl Tower配下に登録した。

##### 技術選定

マルチアカウント管理は今までに全くやっていなかったため、マネージドサービスである『Control Tower』を使用する決断は自然に行われた。
ただし、Control Towerから新規アカウントを作成するのではなく、既存アカウントをControl Towerに登録するため、
既存アカウントに与える影響に関しては、事前にAWSのソリューションアーキテクトに相談するなど慎重に調査した。

##### 成果

本番アカウント/開発アカウントをControl Towerに登録、開発者が利用できる環境を整備した。

その後、Security Hub/GuardDutyをOrganizationsと統合する事で、Control Tower配下の全メンバーアカウント/全リージョンの検出結果を、AuditアカウントのSecurity Hubの集約リージョンに集約した。
これにより、本番アカウント/開発アカウントで起こっている全ての問題を、一箇所で確認、通知できるようになった。

また、リージョン拒否コントロールを有効にする事で、本番アカウント/開発アカウントで利用できるリージョンを制限した。
これにより、Auditアカウントに集約した検出結果の総数が減り、状況を確認しやすくなった。

一通りメンバーアカウントのセキュリティ設定を行った後に、本番アカウントにある開発環境のリソースを開発アカウントに移行する計画を作成した。(計画を実施する前に、離職が決定したため実施には立ちあっていない。)

##### 工夫した点

既存アカウントをControl Towerに登録する必要があったため、事前に作成したテストアカウントで、既存アカウントの登録手順を検証しドキュメント化した。
特にAWS Config回りでエラーが発生する事が多く、事前にそれらの問題の大部分を洗い出せたため良い判断だったと考える。

また、リージョン拒否コントロール等の比較的新しいサービスを、慎重に検証した上で導入する事ができた。
ただ新しいからという理由でなく、公式ドキュメントを中心に調査を行い、組織に取って有用だと判断した上で適用することができた。

##### 今後の改善点

Control Tower配下のメンバーアカウントに関してはセキュアに管理する態勢が整ったが、Control Tower管理アカウントに関してはもう少し検討の余地がある。
Control Tower管理アカウントは、リージョン拒否コントロールが効かないため、全リージョンでセキュリティサービスを有効にする必要があるなど。

また、OU毎に適用するコントロールの精査も今後の課題である。現状は必須コントロールしか適用していないため、統制が不十分である。

</details>

---

### 株式会社シンクロア(現 Kii株式会社) (2010/10〜2021/06): QAエンジニア

---

#### CI環境の整備 (2015/04〜2016/04)

QAテストを実行するCI環境のコード化を行った。

##### チーム構成

- PM: 1人
- エンジニア: 2〜3人

##### 役割

プロジェクトをリードする立場で、技術選定 及び 実用レベルに至るまでの実装を担当した。
その後は、ドキュメント作成などを行い、チームでの運用態勢を確立した。

##### 技術スタック

- Ansible
- Terraform
- Docker
- Packer

<details>
<summary><strong>詳細</strong></summary>

##### 課題

QAテストを実行するCI環境として、Jenkinsを使っていた。Jenkinsはmaster/slave構成を取り、masterノードは1台だが、slaveノードは複数台ある。
slaveノードを増やす事で一度に実行できるジョブを増やすことができるが、手動で環境を構築していたため作業コストが高かった。
テストの実行時間を短縮するためには、slaveノードを手軽に増やすことができる状態が望ましかった。

##### 解決策

masterノード用とslaveノード用のコンテナイメージを作成することとした。
これにより、slaveノードを増やす場合はslaveノード用のイメージを使ってコンテナを追加するだけで良くなった。

コンテナの起動にDocker composeを使用していたため、数行追加するだけでslaveノードを増やせるようになった。

##### 技術選定

コンテナイメージの作成は『Ansible』『Packer』を使用した。
コンテナ環境だけでなく実マシンへのプロビジョニングもできるようにして欲しいとの要求を受けたため、Dockerfileによるプロビジョニングをメインの手段として採用しなかった。
また、Puppet/ChefなどAnsible以外の選択肢も検討したが、どちらもAnsibleよりもチームメンバの学習コストが高いと判断して採用しなかった。(Puppetは独自のDSLが、ChefはRuby自体がチームメンバーの学習障壁になると考えた)

コンテナオーケストレーションの選択肢が、当時は『Docker compose』ぐらいしか知りうる限りではなかったため、この判断は特に迷う事はなかった。

##### 成果

slaveノードを簡単に増やせるようになり、テストの実行時間を短縮しやすくなった。
また、各ノードの設定がコード化されたことにより、master/slave環境に変更を加える前にPRでレビューができるようになった。

##### 工夫した点

Dockerfileではなく敢えてAnsibleによりコンテナをプロビジョニングすることで、コンテナのプロビジョニング と 実マシンへのプロビジョニングの両立を達成した。
コンテナイメージのレイヤが増えてしまうことは分かっていたが、要求を解決するために最適な手段を取る事ができたと考える。

##### 今後の改善点

当時は、コンテナの思想(ex. なるべく小さなサイズで、1コンテナ-1サービス、など)を理解しておらず、仮想マシンの延長で考えてしまった。
そのため、 テストに必要なランタイムを全て1つのイメージに詰め込んでしまいサイズが肥大化しビルド時間が長くなった。
各テストで必要なランタイムは異なっていたため、ランタイム毎に別イメージを作成するなどすれば、この問題は解決できると思われる。

また、全てのコンテナを1台のマシン上で起動するため、slaveの数をある程度増やすためにはかなり性能の良いマシンが求められた。
ECS、EKS(Kubernetes)上で実行できるようにすれば、この問題は解決できると思われる。

</details>

---

#### 課題管理簿(社外)とissueトラッカー(社内)を連携するシステムの開発 (2011/02〜2011/04)

社外からメールで送信されてくる課題管理簿と社内のissueトラッカーを連携するシステムを開発した。

##### チーム構成

- PM: 1人
- エンジニア: 2〜3人

##### 役割

要求ヒアリング、仕様策定、実装、テストまで全て一人で対応した。
その後は、チームメンバーからのレビューを受けての修正、追加要件への対応を行った。

##### 技術スタック

- Python

<details>
<summary><strong>詳細</strong></summary>

##### 課題

Excelファイルで作成された課題管理簿を社外とメールでやり取りしていた。
一方、社内では課題管理にissueトラッカーを採用しており、以下の手順で内容を転記していた。

1. 社外から課題管理簿を添付したメールが担当者に届く。
2. 担当者は課題管理簿(パスワード付きzipで圧縮されている)を解凍し、内容を確認する。
3. 内容を確認した後に、課題管理簿を更新し、社外へのメールに添付する。
4. 社内のissueトラッカーに課題管理簿の内容を転記する。

上記の手順は相応の工数がかかっていたため、社内の担当者の工数を削減したいという要望があった。

##### 解決策

課題で挙げた手順のうち、1、2、4は社内で閉じた手順であり自動化が可能だろうと考えた。
これらの手順を自動化するために、以下の処理を実行するプログラムを実装した。

1. 課題管理簿の受信を検知する。
2. 課題管理簿の内容を解析し、issueトラッカーに登録する。既にissueが作成してある課題管理簿に対して返信があった場合、該当するissueに対してコメントで追記する。
3. 課題管理簿をやり取りするメールの内容により、該当するissueをクローズする。

実装したプログラムは、社内サーバのCronに登録して定期的に実行することとした。

##### 技術選定

『実行環境(Linux)、開発環境(OSX)ともにデフォルトでインストールされている』、『内容を考えると高い処理性能は不要である』、『インタプリタ言語故にトライアンドエラーがしやすい』という点により、『Python』を実装言語に採用した。

##### 成果

- 前述の手順1、2、4が自動化され、担当者の手間が大きく削減された。
- 担当者の裁量で転記していた内容が全てissueトラッカー上に集約されることになり、課題内容を把握・整理する必要があったQAチームのリーダに喜ばれた。

##### 学び

- Shift-JIS(課題管理簿)、euc-jp(動作環境のサーバ)、ISO-2022-JP(メール本文)、UTF-8(その他)、といった複数の文字符号化方式を扱う経験を得た。
- 当時のPython(2.x)はマルチバイト文字列の処理が今と比べてやや煩雑であり、その点は苦労した。後に文字列処理に関してブログにまとめた。
   - Python2: https://qiita.com/FGtatsuro/items/cf178bc44ce7b068d233
   - Python3: https://qiita.com/FGtatsuro/items/f45c349e06d6df95839b

##### 今後の改善点

- 手順3を自動化する
   - issueに対して返信すると、その内容を含んだ課題管理簿を生成、メールで送信する といった実装が考えられる
- issueのClose判定の偽陽性率/偽陰性率を下げる
   - Close判定は正規表現によるテキストマッチングでの実装だったため、偽陽性率/偽陰性率がそれなりに高かった。Close判定に関する学習を実装する、といった解決策を検討する。
- 責任分割を行い、コードの可読性/メンテナンス性を向上させる
   - 開発に慣れていなかったため、メイン関数にかなりの責任が含まれてしまった

</details>

---

#### パブリックネットワーク上での社内限定のドキュメント公開 (2021/02〜2021/04)

社内ドキュメントをアクセス制限をかけて公開した。また、ドキュメント変更を自動で反映するデプロイパイプラインを整備した。

##### チーム構成

- PM: 1人
- エンジニア: 2〜3人

##### 役割

個人プロジェクトから始め、技術選定 及び 実用レベルに至るまでの実装を担当した。
その後は、ドキュメント作成などを行い、チームでの運用態勢を確立した。

##### 技術スタック

- Terraform
- Kubernetes
- GCP
   - Cloud Build
   - Container Registry
   - Cloud Armor
   - Identity-Aware Proxy

<details>
<summary><strong>詳細</strong></summary>

##### 課題

社内サーバで社内限定のドキュメントを公開していたが、オフィス縮小に伴い社内サーバを撤去することになった。
前述のとおり社内限定公開だったため、パブリックネットワークで公開する場合はアクセス制限が必須であった。

##### 解決策

https://cloud.google.com/kubernetes-engine/docs/tutorials/gitops-cloud-build を参考に、ドキュメント変更を自動でデプロイするパイプラインを整備した。

- Githubに『ドキュメントリポジトリ』と『デプロイリポジトリ』を用意する。
- ドキュメントリポジトリの変更をトリガとして Cloud Buildのビルドを実行する。
   - Githubのコミットハッシュをタグに含めた上で、ドキュメントのコンテナイメージを作成する。作成したコンテナイメージはContainer RegistryにPushする。
   - デプロイリポジトリをCloneする。Kubernetesマニフェストを上記タグを参照するよう変更した上で、Kubernetesマニフェストリポジトリにコミットする。
- デプロイリポジトリの変更をトリガとして、Cloud Buildのビルドを実行する。
   - Terraformをapplyして、GCPのリソースを更新する。Cloud Armor(IPアドレス) と Identity-Aware Proxy(Google Workspaceドメイン)により、アクセス制限を達成する。
   - Kubernetesマニフェストをapplyして、ドキュメントをKubernetes上に公開する。

##### 技術選定

ドキュメントを公開するプラットフォームとして『Kubernetes』を採用した。
ドキュメントの公開だけ見るとKubernetesであるべき技術要求はないが、テストの実行時間の短縮のための並列実行を行う事を検討しており、実行するプラットフォームとしてKubernetesを候補として考えていた。
そのため、Kubernetesに慣れるためのPoCとしての意味が強かった。

Kubernetesクラスタを独自に構築・運用する事はコスト的に許容しづらく、マネージメントサービスの採用はほぼ必須であった。
チームは以前GCPの経験があったため、『GKE』を採用することとした。連携の容易さを考慮して、他に必要なサービス(Cloud Build、Container Registry、Cloud Armor、 Identity-Aware Proxy)もGCPのものを採用した。

GCPのリソース作成には『Terraform』を使用した。こちらもチームの以前の経験を考慮して採用した。
KubernetesリソースとしてGCPリソースを管理する[Config Connector](https://cloud.google.com/config-connector/docs/overview)も検討したが、
学習コストが高い、比較的新しいツール故に参考になる事例が少ない、といったことを考慮して採用しなかった。

##### 成果

要求どおり、パブリックネットワーク上に適切なアクセス制限をかけて社内限定ドキュメントを公開できた。
また、ドキュメントの更新を自動で反映する仕組みを整備して、小さなToil(手動でのマニフェスト更新->デプロイ)を削減する事ができた。

##### 今後の改善点

現状は Terraform/Kubernetesの設定に固有情報がベタ書きされている。
これを外部に切り出す事で、今回のユースケース以外にも汎用に使える仕組みにできるのではないかと考えている。

- Terraform: [Modules](https://www.terraform.io/docs/language/modules/index.html)
- Kubernetes: [Kustomize](https://kubectl.docs.kubernetes.io/references/kustomize/)

</details>

---

#### テスト実装言語の移行 (2015〜2020)

APIサーバのQAテストを実装するプログラミング言語を、JavaからGroovyに移行した。

##### チーム構成

- PM: 1人
- エンジニア: 2〜3人

##### 役割

移行するプログラミング言語の選定を行い、移行計画を作成した。
その後は、チーム全員で新しい言語への移行を実施した。

##### 技術スタック

- Java
- Groovy

<details>
<summary><strong>詳細</strong></summary>

##### 課題

元々APIサーバのQAテストはJavaで実装していたが、 当時のJava(1.5、1.6)は現在のバージョンと比べてボイラープレートが多く、テストコードが冗長になりやすい傾向にあった。冗長なテストコードでは、何をテストしているのかがテストコード上から追いにくくなるため、同じ処理を簡潔に記述できる言語に移行したいと考えた。

また異常系を考えるとテストは様々な入力を扱う事になるため、(Javaが持つような)堅牢性よりも柔軟性を優先したい場面が多かった。

##### 技術選定

『Groovy』を移行先の言語として採用した。
『Javaとの相互呼び出しが簡単に行える』『ファイルの拡張子を変更するだけで、大部分のコードが移行できる』など、他のJVM言語と比較してもJavaとの親和性が高く、移行コストを抑えつつもスクリプト言語のような柔軟性をテスト実装に導入できると考えた。

##### 工夫した点

前述の『ファイルの拡張子を変更するだけで、大部分のコードが移行できる』特性を生かして、既存のコードを書き直す前に拡張子のみ変更して、Groovyで動作する事を確認した。その後、特に冗長になっている部分を優先して変更し、変更する度にテストが再実行できるかを検証した。
これにより、段階的にJavaからGroovyに移行する事ができ、日々のQAに大きな影響を及ぼさずに移行を終えることができた。

</details>

---

### 株式会社NTTデータ (2009/04〜2010/09): システムエンジニア

---

#### 大規模データの分散処理フレームワークの研究調査 (2009/10〜2010/03)

大規模データの分散処理フレームワークである『Hadoop』の研究調査 及び 報告書作成を行うプロジェクトに参加した。

##### チーム構成

- PM: 2〜3人
- エンジニア: 5〜6人

##### 役割

Hadoop管理ノードの冗長化に関する調査を担当した。

##### 技術スタック

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

(*)一部トップページと重複した記述あり

- [インフラ構築](./infra.md)
- [社内システム/ツール開発](./for_company.md)
- [QA](./qa.md)
- [チームへのスクラム導入](./management.md)
