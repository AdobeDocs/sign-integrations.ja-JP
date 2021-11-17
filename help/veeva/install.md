---
title: '[!DNL Veeva Vault] インストールガイド'
description: Adobe Signと Veeva の統合を可能にするインストールガイド
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 5d61a428-06e4-413b-868a-da296532c964
source-git-commit: 7ded835b48519cba656f160e691c697c91e2c8d0
workflow-type: tm+mt
source-wordcount: '3131'
ht-degree: 2%

---

# [!DNL Veeva Vault] インストールガイド{#veeva-installation-guide}

[**Adobe Sign サポートへのお問い合わせ**](https://adobe.com/go/adobesign-support-center)

## 概要 {#overview}

この文書では、Adobe Signと [!DNL Veeva Vault] プラットフォーム。 [!DNL Veeva Vault] は、ライフサイエンス業界向けに構築された ECM（エンタープライズ・コンテンツ管理）プラットフォームです。 「Vault」とは、規制書類の提出、調査レポートの作成、申請書類の提出、一般契約書の作成などに使用されるコンテンツとデータのリポジトリです。 1 つの企業で複数の「ボールト」を使用し、個別に管理する必要があります。

統合を完了するための高度な手順は次のとおりです。

* Adobe Signで管理アカウントをアクティベートする（新規顧客のみ）
* オブジェクトを作成して、Vault の契約書ライフサイクルの履歴を追跡します。
* 新しいセキュリティプロファイルを作成します。
* Adobe Signで、 [!DNL Veeva Vault] 統合ユーザー。
* 文書フィールドとレンディションを作成します。
* Web アクションを設定し、ドキュメントライフサイクルを更新します。
* ドキュメントタイプのユーザーおよびユーザーロールの設定を作成します。

>[!NOTE]
>
>Adobe Sign管理者は、Adobe Sign内でAdobe Signの設定手順を実行する必要があります。

## 設定 [!DNL Veeva Vault] {#configure-veeva}

設定するには [!DNL Veeva Vault] Adobe Signとの統合のために、Vault 内の契約書ライフサイクルの履歴を追跡するのに役立つ特定のオブジェクトを作成します。 管理者は、次のオブジェクトを作成する必要があります。

* 署名
* 署名者
* 署名イベント
* Process Locker

### 署名オブジェクトの作成  {#create-signature-object}

署名オブジェクトは、契約書に関連する情報を格納するために作成されます。 Signature オブジェクトは、次の特定のフィールドに情報を格納するデータベースです。

**署名オブジェクトフィールド**

| フィールド | ラベル | タイプ | 説明 |
| --- | --- | ---| --- | 
| external_id__c | 契約書 ID | 文字列 (100) | Adobe Signの一意の契約書 ID を保持 |
| file_hash__c | ファイルハッシュ | 文字列 (50) | Adobe Signに送信されたファイルの md5 チェックサムを保持します |
| name__v | 名前 | 文字列 (128) | 契約書名を保持します |
| sender__c | 送信者 | オブジェクト（ユーザー） | 契約書を作成した Vault ユーザーへの参照を保持します |
| signature_status__c | 署名ステータス | 文字列 (75) | Adobe Signでの契約書のステータスを保持 |
| signature_type__c | 署名タイプ | 文字列 (20) | Adobe Signでの契約書の署名タイプ（手書きまたは電子サイン）を保持します。 |
| start_date__c | 開始日 | DateTime | 契約書が署名用に送信された日付 |
| cancellation_date__c | 解約日 | DateTime | 契約書がキャンセルされた日付を保持します。 |
| completion_date__c | 完了日 | DateTime | 契約が完了した日付を保持します。 |
| viewable_rendition_used__c | 表示可能なレンディション使用 | ブール値 | 表示可能なレンディションが署名用に送信されたかどうかを示すフラグ。 （デフォルトでは true） |

![署名オブジェクトの詳細の画像](images/signature-object-details.png)

### 署名者オブジェクトの作成 {#create-signatory-object}

署名者オブジェクトは、契約書の参加者に関連する情報を格納するために作成されます。 以下の特定のフィールドに情報が含まれています。

**署名者オブジェクトフィールド**

| フィールド | ラベル | タイプ | 説明 |
| --- | --- | ---| --- | 
| email__c | 電子メール | 文字列 (120) | Adobe Signの一意の契約書 ID を保持 |
| external_id__c | 参加者 ID | 文字列 (80) | Adobe Signの一意の参加者の識別子を保持します |
| name__v | 名前 | 文字列 (128) | Adobe Sign参加者の名前を保持 |
| order__c | 順序 | 数値 | Adobe Sign契約書の参加者の注文番号を保持 |
| role__c | 役割 | 文字列 (30) | Adobe Sign契約書の参加者のロールを保持 |
| signature__c | 署名 | オブジェクト（署名） | 署名の親レコードへの参照を保持します |
| signature_status__c | 署名ステータス | 文字列 (100) | Adobe Sign契約書の参加者のステータスを保持 |
| user__c | ユーザー | オブジェクト（ユーザー） | 参加者が Vault ユーザである場合、署名者のユーザレコードへの参照を保持します |

![署名者の詳細の画像](images/signatory-object-details.png)

### 署名イベントオブジェクトの作成  {#create-signature-event}

署名イベントオブジェクトは、契約書のイベント関連情報を保存するために作成されます。 以下の特定のフィールドに情報が含まれています。

| フィールド | ラベル | タイプ | 説明 |
| --- | --- | ---| --- | 
| acting_user_email__c | 代行ユーザー電子メール | 文字列 | イベントを生成する原因となったアクションを実行したAdobe Signユーザーの電子メールを保持します |
| acting_user_name__c | 代行ユーザー名 | 文字列 | イベントを生成する原因となったアクションを実行したAdobe Signユーザーの名前を保持します |
| description__c | 説明 | 文字列 | Adobe Signイベントの説明を保持します |
| event_date__c | イベント日 | DateTime | Adobe Signイベントの日時を保持します |
| event_type__c | イベントタイプ | 文字列 | Adobe Signイベントのタイプを保持します |
| name__v | 名前 | 文字列 | 自動生成されたイベント名 |
| participant_comment__c | 参加者コメント | 文字列 | Adobe Sign参加者のコメントがある場合に、コメントを保持します |
| participant_email__c | 参加者の電子メール | 文字列 | Adobe Sign参加者の電子メールを保持 |
| participant_role__c | 参加者の役割 | 文字列 | Adobe Sign参加者のロールを保持します |
| signature__c | 署名 | オブジェクト（署名） | 署名の親レコードへの参照を保持します |

![署名イベントの詳細の画像](images/signature-event-object-details.png)

### Process Locker オブジェクトの作成  {#create-process-locker}

Process Locker オブジェクトが作成され、Adobe Sign統合プロセスがロックされます。 カスタムフィールドは必要ありません。

![署名イベントの詳細の画像](images/process-locker-details.png)

## セキュリティプロファイルの作成{#security-profiles}

Vault を正常に統合するには、 *Adobe Sign統合プロファイル* が作成され、その権限が *Adobe Sign Admin Actions*&#x200B;を選択します。 Adobe Sign統合プロファイルは、システムアカウントに割り当てられ、Vault API を呼び出すときに統合によって使用されます。 このプロファイルは、次の権限を許可します。

* Vault API
* 読み取り、作成、編集、削除：署名、署名者、署名イベント、および Process Locker オブジェクト

![署名イベントの詳細の画像](images/security-profiles.png)

Vault 内のAdobe Sign履歴へのアクセスを必要とするユーザのセキュリティプロファイルには、署名、署名者、および署名イベントオブジェクトに対する読み取り権限が必要です。

![署名イベントの詳細の画像](images/set-permissions.png)

## グループの作成 {#create-group}

Adobe Signを [!DNL Vault]という新しいグループが *Adobe Sign Admin Group* が作成されます。 このグループは、Adobe Sign関連フィールドの文書フィールドレベルのセキュリティを設定するために使用され、以下を含める必要があります *Adobe Sign統合プロファイル* デフォルトです。

![署名イベントの詳細の画像](images/create-admin-group.png)

## ユーザーを作成 {#create-user}

Adobe Sign統合の Vault システムアカウントユーザは、次のことを行う必要があります。

* Adobe Sign統合プロファイルを使用
* セキュリティプロファイルの使用
* パスワードの有効期限を無効にする特定のセキュリティポリシーを設定する
* Adobe Sign Admin Group のメンバーであること。

システムアカウントユーザーが特定のドキュメントライフサイクルのAdobe Sign Admin Group に属するようにするには、ユーザーロールの設定レコードを作成する必要があります。

## アプリケーションロールの作成 {#create-application-roles}

次のアプリケーションロールを作成する必要があります： *Adobe Sign管理者ロール*&#x200B;を選択します。 この役割は、ライフサイクル署名の対象となる各文書タイプのライフサイクルで定義する必要があります。Adobe署名。 Adobe Sign固有のライフサイクル状態ごとに、Adobe Sign管理者ロールが追加され、適切な権限で設定されます。

![アプリケーションロール作成のイメージ](images/create-application-roles.png)

## 文書フィールドを作成 {#create-fields}

Adobe Signとの統合を確立するには、管理者は次の 2 つの新しい共有ドキュメントフィールドを作成する必要があります。

* 署名 (signature__c)
* Adobe Signユーザーアクションを許可する (allow_adobe_sign_user_actions__c)

![文書の詳細の画像](images/create-document-fields.png)

これらの共有フィールドは、署名の対象となるすべての文書タイプに追加する必要があります。Adobe署名。 両方のフィールドに、Adobe Sign Admin Group のメンバーのみが値を更新できる特定のセキュリティが設定されている必要があります。

![署名フィールドの詳細の画像](images/signature-field-details.png)

管理者は、既存の共有フィールドを追加する必要があります *Vault オーバーレイを無効にする (disable_vault_overlays__v)* を選択し、署名の対象となるすべての文書タイプに対して「有効」にAdobeします。 必要に応じて、Adobe Sign Admin グループのメンバーのみが値を更新できる特定のセキュリティをフィールドに設定できます。

![Adobe Sign ユーザーアクションを許可の画像](images/allow-adobe-sign-user-actions.png)

## レンディションの作成 {#create-renditions}

管理者は、 *Adobe Signレンディション (adobe_sign_rendition__c)*&#x200B;を使用して、署名済みのPDF文書をAdobe Signにアップロードします。 Adobe Signレンディションは、Adobe署名の対象となる文書型ごとに宣言する必要があります。

![レンディションの種類の画像](images/rendition-type.png)

![レンディションの種類の画像](images/edit-details-clinical-type.png)

## Web アクションの設定 {#web-actions}

Adobe Signと Vault の統合では、次の 2 つの Web アクションを作成および設定する必要があります。

* **Adobe Sign**:Adobe Sign Agreement が作成または表示されます。

   種類：文書のターゲット：Vault URL 内に表示： <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

* **Adobe Sign**:Adobe Signの既存の契約書をキャンセルし、文書の状態を最初の状態に戻します。

   種類：文書のターゲット：Vault URL 内に表示：: <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement/cancel?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

## ドキュメントライフサイクルの更新 {#document-lifecycle}

ライフサイクル署名の対象となる各文書タイプについて、対応する文書Adobeを、新しいライフサイクルの役割および状態を追加して更新する必要があります。

### ライフサイクルロール {#lifecycle-role}

アプリケーション署名の対象となる文書で使用されるすべてのライフサイクルに、Adobe Sign管理者アプリケーションのロールを追加するAdobeが必要です。 この役割は、次のオプションを使用して作成する必要があります。

* 動的アクセス制御を有効にする
* ドキュメントタイプグループのみを含むドキュメント共有ルール

![ライフサイクル管理ロールのイメージ](images/document-lifecycle-admin-role.png)

### ライフサイクル状態 {#lifecycle-states}

Adobe Sign契約書のライフサイクルには、次の状態があります。

* ドラフト
* AUTHORING または DOCUMENTS_NOT_YET_PROCESSED
* OUT_FOR_SIGNATURE または OUT_FOR_APPROVAL
* 署名済みまたは承認済み
* キャンセル済み
* 期限切れ

Vault ドキュメントをAdobe Signに送信する場合、その状態は契約書の状態に対応している必要があります。 これを行うには、ライフサイクル署名の対象となる文書で使用されるすべてのライフサイクルに、次のAdobeを追加します。

* **署名Adobe前** （確認）:これは、ドキュメントをAdobe Signに送信できる状態のプレースホルダー名です。 ドキュメントタイプに基づいて、「ドラフト」状態または「レビュー済み」状態にすることができます。 ドキュメント状態ラベルは、お客様の要件に合わせてカスタマイズできます。 Adobe署名前の状態では、次の 2 つのユーザーアクションを定義する必要があります。

   * ドキュメントの状態を *Adobe Sign Draft* を選択します。 このユーザアクションの名前は、すべてのライフサイクルのすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * Web アクションを&#39;Adobe Sign&#39;と呼び出すアクション。 この状態には、Adobe Sign管理者ロールが次の操作を実行できるセキュリティが必要です。ドキュメントの表示、コンテンツの表示、フィールドの編集、関係の編集、ソースのダウンロード、表示可能なレンディションの管理、状態の変更を行います。

      ![ライフサイクルステータス 1 のイメージ](images/lifecycle-state1.png)

* **Adobe Sign Draft**:これは、ドキュメントが既にAdobe Signにアップロードされ、その契約書がドラフト状態であることを示す、状態のプレースホルダー名です。 必須状態です。 この状態では、次の 5 つのユーザーアクションを定義する必要があります。

   * ドキュメントの状態を *Adobe Sign Authoring* を選択します。 このユーザアクションの名前は、すべてのライフサイクルのすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * ドキュメントの状態を *署名Adobe状態*&#x200B;を選択します。 このユーザアクションの名前は、すべてのライフサイクルのすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * ドキュメントの状態を *Adobe Sign Cancelled* を選択します。 このユーザアクションの名前は、すべてのライフサイクルのすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * Web アクション「Adobe Sign」を呼び出すアクション。
   * Web アクション「Adobe Signをキャンセル」を呼び出すアクション。 この状態には、Adobe Sign 管理者ロールが次の操作を実行できるセキュリティが必要です。ドキュメントの表示、コンテンツの表示、フィールドの編集、関係の編集、ソースのダウンロード、表示可能なレンディションの管理、状態の変更を行います。

      ![ライフサイクルステータス 2 のイメージ](images/lifecycle-state2.png)

* **Adobe Sign Authoring**:これは、文書が既にAdobe Signにアップロードされており、その契約書の状態が AUTHORING または DOCUMENTS_NOT_YET_PROCESSED であることを示す、ステートのプレースホルダー名です。 必須状態です。 この状態には、次の 4 つのユーザーアクションを定義する必要があります。

   * ドキュメントの状態を「Adobe Sign Cancelled」状態に変更するアクション。 このユーザーアクションの名前は、ライフサイクルに関係なくすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * ドキュメントの状態を「署名中」状態に変更するAdobeです。 このユーザーアクションの名前は、ライフサイクルに関係なくすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * Web アクション「Adobe Sign」を呼び出すアクション
   * Web アクション「Adobe Signをキャンセル」を呼び出すアクション。 この状態には、Adobe Sign 管理者ロールが次の操作を実行できるセキュリティが必要です。ドキュメントの表示、コンテンツの表示、フィールドの編集、関係の編集、ソースのダウンロード、表示可能なレンディションの管理、状態の変更を行います。

      ![ライフサイクルステータス 3 のイメージ](images/lifecycle-state3.png)

* **署名Adobe**:これは、文書がAdobe Signにアップロードされ、その契約書が既に参加者に送信されていることを示す状態（OUT_FOR_SIGNATURE または OUT_FOR_APPROVAL 状態）のプレースホルダー名です。 必須状態です。 この状態には、次の 5 つのユーザーアクションを定義する必要があります。

   * ドキュメントの状態を「Adobe Sign Cancelled」状態に変更するアクション。 このアクションのターゲット状態は、顧客の要件に応じて異なる場合があります。 このユーザーアクションの名前は、ライフサイクルに関係なくすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * ドキュメントの状態を「Adobe Sign Rejected」状態に変更するアクション。 このアクションのターゲット状態は、顧客の要件に応じて異なる場合があります。 このユーザーアクションの名前は、ライフサイクルに関係なくすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * ドキュメントの状態を署名済みAdobeに変更する操作。 このアクションのターゲット状態は、顧客の要件に応じて異なる場合があります。 ただし、このユーザーアクションの名前は、ライフサイクルに関係なくすべてのドキュメントタイプで同じである必要があります。 必要に応じて、このアクションの条件を「Adobe Signユーザーアクションを許可する」が「はい」に設定できます。
   * Web アクションを呼び出すアクション *Adobe Sign*&#x200B;を選択します。
   * Web アクションを呼び出すアクション *Adobe Sign*&#x200B;を選択します。 この状態には、Adobe Sign 管理者ロールが次の操作を実行できるセキュリティが必要です。ドキュメントの表示、コンテンツの表示、フィールドの編集、関係の編集、ソースのダウンロード、表示可能なレンディションの管理、状態の変更を行います。

      ![ライフサイクルステータス 4 のイメージ](images/lifecycle-state4.png)

* **Adobe署名済み（承認済み）**:これは、文書がAdobe Signにアップロードされ、契約書が完了したことを示す状態（署名済みまたは承認済みの状態）のプレースホルダー名です。 これは必須の状態であり、「承認済み」などの既存のライフサイクル状態にすることができます。
この状態では、ユーザー操作は必要ありません。 この状態には、Adobe Sign管理者の役割で次の操作を実行できるセキュリティが必要です。文書の表示、コンテンツの表示、フィールドの編集ができます。

次の図は、Adobe Sign契約書と Vault ドキュメント状態のマッピングを示しています。この場合、「Adobe署名前」状態は「ドラフト」です。

![Adobe Sign Vault マッピングのイメージ](images/sign-vault-mappings.png)

## ドキュメントタイプグループとユーザーロールの設定の作成  {#document-type-group-user-role}

### ドキュメントタイプグループの作成 {#create-document-type-group}

管理者は、「Adobe Sign Document」という名前の新しいドキュメントタイプグループレコードを作成する必要があります。 このドキュメントタイプグループは、Adobe Signプロセスに適格なすべてのドキュメント分類に追加されます。 ドキュメントタイプグループプロパティは、タイプからサブタイプまたはサブタイプから分類レベルに継承されないため、Adobe Signに適格な各ドキュメントの分類に対して設定する必要があります。

![ドキュメントタイプの画像](images/document-type.png)

![ドキュメントタイプの画像](images/document-edit-details.png)

### ユーザーロール設定の作成 {#create-user-role-setup}

ライフサイクルが適切に設定されたら、Adobe Signプロセスの対象となるすべての文書に対して、Adobe Sign Admin ユーザーが DAC によって追加されるようにします。 これを行うには、次を指定する適切なユーザーロール設定レコードを作成します。

* 「Adobe Sign Document」としてのドキュメントタイプグループ、
* 「Adobe Sign管理者ロール」としてのアプリケーションロール
* 統合ユーザー。

![ユーザーロール設定のイメージ](images/user-role-setup.png)

>[!NOTE]
>
>ユーザーロール設定オブジェクトに、文書型グループオブジェクトを参照するフィールドが含まれていない場合は、このフィールドを追加する必要があります。

## Connect [!DNL Veeva Vault] ミドルウェアを使用してAdobe Signに {#connect-middleware}

のセットアップ完了後 [!DNL Veeva Vault] とAdobe Sign Admin アカウントを使用する場合、管理者はミドルウェアを使用して 2 つのアカウント間の接続を作成する必要があります。 この [!DNL Veeva Vault] Adobe Signアカウントの接続はAdobe Sign Identity によって開始され、Veeva Vault ID の保存に使用されます。
システムのセキュリティと安定性を確保するため、管理者は専用の [!DNL Veeva Vault] システム/サービス/ユーティリティアカウント ( `adobe.for.veeva@xyz.com`のような個人ユーザーアカウントの代わりに、 `bob.smith@xyz.com`を選択します。

Adobe Signアカウント管理者が接続するには、次の手順に従う必要があります [!DNL Veeva Vault] ミドルウェアを使用してAdobe Signするには、次の手順に従います。

1. 次の [Adobe Sign [!DNL Veeva Vault] ホームページ](https://static.adobesigncdn.com/veevavaultintsvc/index.html)を選択します。
1. 選択 **[!UICONTROL ログイン]** を選択します。

   ![ミドルウェア・ログインのイメージ](images/middleware_login.png)

1. 開いたAdobe Signログインページで、アカウント管理者の電子メールアドレスとパスワードを入力し、「 **[!UICONTROL 歌う]**&#x200B;を選択します。

   ![画像](images/middleware-signin.png)

   ログインに成功すると、以下に示すように、関連付けられている電子メール ID と「設定」タブがページに表示されます。

   ![画像](images/middleware_settings.png)

1. ツールバーの「 **[!UICONTROL 設定]** タブを選択します。

   次に示すように、設定ページには使用可能な接続が表示され、最初の接続が設定されている場合は「なし」と表示されます。

   ![画像](images/middleware_newconnection.png)

1. 選択 **[!UICONTROL 接続の追加]** をクリックして、新しい接続を追加します。

1. 表示された接続を追加ダイアログで、必要な詳細情報 ( [!DNL Veeva Vault] 資格情報。

   Adobe Signの資格情報は、最初のAdobe Signログインから自動的に入力されます。

   ![画像](images/middleware_addconnection.png)

1. 選択 **[!UICONTROL 検証]** 」をクリックして、アカウントの詳細を確認します。

   検証が成功すると、次に示すように「ユーザーが正常に検証されました」という通知が表示されます。

   ![画像](images/middleware_validated.png)

1. 特定のAdobe Signグループのみに使用を制限するには、 **[!UICONTROL グループ]** 」ドロップダウンリストを開き、使用可能なグループのいずれかを選択します。

   ![画像](images/middleware_group.png)

1. 選択 **[!UICONTROL 保存]** 」をクリックして新しい接続を保存します。

   新しい接続が「設定」タブに表示され、 [!DNL Veeva Vault] Adobe Sign

   ![画像](images/middleware_setup.png)

## パッケージ展開のライフサイクル {#deployment-lifecycle}

### 一般的な展開ライフサイクル {#general-deployment}

**手順 1.** 「Adobe Sign Admin Role」という新しいアプリケーションロールを作成します。

**手順 2.** 「Adobe Sign Document」という名前の新しいドキュメントタイプグループを作成します。

**手順 3.** [パッケージのデプロイ](https://helpx.adobe.com/content/dam/help/en/PKG-AdobeSign-Integration.zip)を選択します。

**手順 4.** 「Adobe Sign Admin Group」という名前の新しいユーザー管理グループを作成します。

**手順 5.** セキュリティプロファイル「Adobe Sign統合プロファイル」を使用して統合ユーザープロファイルを作成し、Adobe Sign Admin Group に割り当てます。

**手順 6.** Vault 内のAdobe Sign履歴へのアクセスを必要とするユーザの署名、署名者、署名イベントオブジェクトに、すべてのセキュリティプロファイルの読み取りアクセス権を割り当てます。

**手順 7.** Adobe署名の対象となる各文書タイプのライフサイクルで、Adobe Sign管理者ロールを定義します。 Adobe Sign固有のライフサイクル状態ごとに、このロールが追加され、適切な権限で設定されます。

**手順 8.** Adobe Sign Rendition を、署名の対象となる各文書タイプに対してAdobeします。

**手順 9.** ライフサイクル署名の対象となる各文書タイプについて、Adobeの新しいロールと状態を追加して、対応する文書ライフサイクルを更新します。

**手順 10.** Adobe Signプロセスの対象となるすべての文書分類に、「Adobe Sign Document」という文書タイプグループを追加します。

**手順 11.** すべての設定が完了したら、Adobe Signプロセスの対象となるすべての文書に対して DAC がAdobe Sign Admin ユーザーを追加します。 そのためには、適切なユーザーロールの設定レコードを作成し、文書型グループを「Adobe Signドキュメント」、アプリケーションロールを「Adobe Sign管理者ロール」、統合ユーザーに指定します。

### 特定の導入ライフサイクル {#specific-deployment}

**手順 1.** 「Adobe Sign Admin Role」という新しいアプリケーションロールを作成します。

**手順 2.** 「Adobe Sign Document」という名前の新しいドキュメントタイプグループを作成します。

**手順 3.** [パッケージのデプロイ](https://helpx.adobe.com/content/dam/help/en/PKG-AdobeSign-Integration.zip)を選択します。

**手順 4.** 「Adobe Sign Admin Group」という、ユーザーが管理する新しいグループを作成します。

**手順 5.** セキュリティプロファイル「Adobe Sign統合プロファイル」を持つ統合ユーザープロファイルを 1 つ作成し、Adobe Sign Admin Group に割り当てます。
