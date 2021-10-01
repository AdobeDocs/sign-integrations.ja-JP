---
title: NetSuite 用 Adobe Sign リリースノート
description: 'NetSuite向けAdobe Sign統合の現在のリリースに含まれる新機能と変更点について説明します。  '
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
source-git-commit: 924813403d8e13f816347dd548a68a16d78d866e
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 68%

---


# NetSuite 用 Adobe Sign リリースノート

## パッケージv4.0.4に更新

v4.0.4 は、新しく生成されたすべてのトラフィックにアカウント固有のドメインを使用するように完全に調整されています。

Adobe Sign アイコンが新しいグラフィックに更新されました。

## 過去のリリースノート

### NetSuite 4.0.4 用 Adobe Sign

v4.0.4 は、新しく生成されたすべてのトラフィックにアカウント固有のドメインを使用するように完全に調整されています。

Adobe Sign アイコンが新しいグラフィックに更新されました。

### NetSuite 4.0.2 用 Adobe Sign

**Adobe Sign**（*Adobe Document Cloud eSignサービス*&#x200B;から）に再ブランド化\
以前に&#x200B;*Adobe eSign Services*&#x200B;を再ブランド化の証拠として見た&#x200B;*Adobe Sign*&#x200B;が表示されます。

### NetSuite 4.0.1 用 Adobe Sign

NetSuite がプラットフォームを更新際、API に以前にはなかったバグが生じました。この対策として、新しいパッケージ（v4.0.1）をリリースしました。

お客様は最新パッケージへと更新することをお勧めします。

### NetSuite 4.0 用 Adobe Sign

**NetSuite を介したユーザーの自動プロビジョニングの追加**

v4.0　に新しいカスタムの環境設定が追加されました。この設定を有効にすると、NetSuite で契約書を送信するユーザーは Adobe Document Cloud 電子サインサービスのユーザーアカウントで自動プロビジョニングされます。

**「NetSuite用に構築」で認定**

このバージョンは、「Built for NetSuite」の認定を受けており、NetSuite の設計に関する最新のすべてのベストプラクティスに準拠しています。

**Adobe Document Cloud eSignサービス（EchoSignから）に再ブランド化**

リブランディングの証拠として、以前 Adobe EchoSign と表示されていたところが Adobe Document Cloud 電子サインサービス（または Adobe 電子サインサービス）と表示されるようになります。

**OAuth を使用して強化されたセキュリティを実装**

データセキュリティを強化するために、電子サインサービスでは OAuth 2.0 を使用して NetSuite で Adobe Document Cloud 電子サインサービスアカウントを認証します。この新しいプロトコルを使用することで、電子サインサービスのパスワードを要求しなくても NetSuite が電子サインサービスと対話できるようになります。アプリケーション間で機密情報が直接共有されないので、アカウントが危険にさらされる可能性が低くなります。この強化は現在の実装には影響しませんが、ワンタイムセットアップを実行して、Adobe Document Cloud とやり取りする NetSuite パッケージを認証する必要があります。このセットアップはインストールプロセス中に実行されます。パッケージの以前のバージョン（v3.5.9 以前）からアップグレードするお客様の場合、以前使用されていた API キーは、認証プロセスの過程で生成された OAuth トークンに置き換えられます。

**SOAP API から REST API への電子サインサービスの移行**

効率、柔軟性、処理速度を向上させるため、Adobe Document Cloud eSignサービス、およびNetSuiteのv4.0統合は、SOAPベースのAPIからRESTベースのAPIに移行されました。

### NetSuite 3.0 用 Adobe Sign

**高度な参加者の役割 - 承認者**

* 契約書で 1 人以上の受信者を承認者としてマークすることができます
* 承認者は、ドキュメントを確認して承認する必要があります
* 承認者に対し、承認前に契約書にデータを入力するよう要求することもできます

**送信前に文書をプレビュー、またはフォームフィールドをドラッグ＆ドロップ**

署名を送信する前に、契約をプレビューするか、フォームフィールドをドラッグアンドドロップします

**現在の署名者にリマインダーを送信**

現在の署名者にすぐにリマインダーを送信する

**署名者認証ポリシーの詳細設定**

* **ナレッジベース認証：署名** 者のIDを確認するための質問に回答
   * 署名者は、数百のパブリックデータベースおよび商用データベースから取得した質問に回答することで、身元を証明する必要があります。
   * 署名の名前はユーザーの認証済みの名前から取得され、署名時に変更することはできません。
   * RSA を利用
   * ナレッジベース認証の使用は、アカウントごと、1 ヶ月ごとに制限されます。詳しくは、営業担当にお問い合わせください。

* **Web ID：署名** する前に、Facebook、LinkedIn、Google、または他のサードパーティWebサービスでサインインします。

   * 署名者は、サードパーティのWebサービスを使用して本人確認を行った後にのみ署名できます。
   * 署名の名前はユーザーの Web サービスプロファイルから取得され、署名時に変更することはできません。
   * 監査記録は、ID 検証情報を取得します。

* **ワンタイムパスワード**
   * 内部の署名者や外部の署名者、またはすべての署名者の認証方法を適用します。外部署名者はパスワードを使用するか、知識ベース認証を使用する必要がありますが、内部署名者は使用しません

**その他のカスタムプリファレンス**

* 署名付きPDFを！le URLへのリンクまたはNetSuiteでホストされる添付ファイルとして追加
* 契約書に署名した後で、契約書レコードに監査記録を追加します。
* 顧客電子メールではなく、トランザクションの担当者をデフォルトの第一署名者として使用します。
* 署名者に対し、受信者を承認者としてマークするオプションを提供します。

**トランザクションファイル**

現在のトランザクションから添付するファイルを選択するには、新しい[トランザクションファイル]ドロップダウンリストを使用します。

**すべての EchoSign 文書用の Adobe PDF 証明書**

* EchoSignから送信またはダウンロードされたすべてのPDFファイルは、Adobe EchoSignデジタル証明書で認証されます
* AcrobatまたはReaderは、ドキュメントが改ざんされていないことを保証する証明書を表示し、信頼と安心を確保します

**サポートドキュメントの収集**

* 送信者は、署名時に署名者から、追加サポート文書（運転免許証や登記証など）を収集することができます。
* 収集された文書は署名済み契約書の正式な記録の一部となります。

**条件付きデータフィールド**

* 契約書フィールドの条件付きロジックを定義します。
* 条件は、契約書の 1 つ以上の値を元にすることができます。
* 条件は、フォームオーサリング UI のドラッグ＆ドロップ、またはテキストタグによって定義できます。
* 署名者は、!ned条件に基づいてドキュメントに署名する際に、適切なフィールドを表示します。

**その他の EchoSign フォームフィールドの機能強化**

* ドロップダウンメニュー
* フィールドマスク
* ラジオボタン
* 文書構造を保持するよう、短いテキストタグを作成