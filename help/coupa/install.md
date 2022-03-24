---
title: Coupa インストールガイド
description: Coupa BSM Suite とのAdobe Sign統合を有効にするためのインストールガイド
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 12c91be5-afec-4918-a8fc-ceb33bedf98b
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 6%

---

# [!DNL Coupa] インストールガイド{#coupa-installation-guide}

[**Adobe Sign サポートへのお問い合わせ**](https://adobe.com/go/adobesign-support-center_jp)

## 概要 {#overview}

この文書では、統合するようにAdobe Signアカウントを設定する方法について説明します [!DNL Coupa BSM Suite] インスタンスを使用します。

前提条件:

* Adobe Sign Enterprise のサブスクリプション [Adobe Sign Developer Edition](https://www.adobe.com/sign/developer-form.html)、または [Adobe Sign Enterprise 体験版](https://www.adobe.com/sign/business.html)
* Adobe Sign管理者アクセス
* [!DNL Coupa BSM Suite] 標準インスタンスまたは詳細インスタンス

統合を完了するための高度な手順は次のとおりです。

* で使用するAdobe Signグループの設定 [!DNL Coupa BSM Suite]
* Connect [!DNL Coupa BSM Suite] Adobe Sign
* 通知するAdobe Sign Webhook の作成 [!DNL Coupa BSM Suite] instance

## Adobe Sign Group を [!DNL Coupa BSM Suite] {#configure-adobe-sign-for-coupa}

Adobe Signを [!DNL Coupa] 組織内で、管理者はAdobe Signグループを [!DNL Coupa BSM Suite] 使用方法 このAdobe Signグループには、サービスアカウントとして機能する単一のグループ管理者ユーザーアカウントが必要です。 このサービスアカウントはすべての署名要求に使用されるため、例えば `Legal@xyz.com`, `Purchasing@xyz.com`、または `CoupaCLM@xyz.com`のような個人的なものではなく、 `Bob.Smith@xyz.com`を選択します。

### Adobe Signでのグループとユーザーの作成 {#create-sign-user-group}

Adobe Sign でユーザーを作成するには：

1. アカウント管理者として Adobe Sign にログインします。。
1. 次の場所に移動 **[!UICONTROL アカウント]** > **[!UICONTROL ユーザー]**&#x200B;を選択します。
1. 新規ユーザーを作成するには、「 ![プラスアイコンの画像](images/icon_plus.png) アイコンをクリックします。
1. 表示されたダイアログで、新しいユーザーの詳細を入力します。

   1. アクセスできる機能する電子メールを入力します。

      * このユーザーは、OAuth 関係を確立および維持します。
      * 電子メールアドレスは、検証のための実際のアドレスである必要があります。
   1. 適切な値を入力 [!UICONTROL 名] および [!UICONTROL 姓]を選択します。
   1. 」を [!UICONTROL プライマリグループ] 」フィールドで、「 **[!UICONTROL このユーザーの新しいグループを作成]**&#x200B;を選択します。
   1. 」を [!UICONTROL 新しいグループ名] フィールドに入力します。このフィールドには、 *[!DNL Coupa BSM Suite]*&#x200B;を選択します。

   ![ユーザーを作成パネル](images/create-user.png)

1. 選択 **[!UICONTROL 保存]**&#x200B;を選択します。

   詳細を保存すると、 [!UICONTROL ユーザー] ページには、新しいユーザーが [!UICONTROL 作成済み] ステータス

   ![新しく作成されたユーザーの表示](images/post-user-creation.png)

   この [!UICONTROL 作成済み] ステータスは、ユーザーが電子メールアドレスをまだ確認していないことを示します。

1. 電子メールアドレスを確認するには：
   1. 新しいユーザーの電子メールにログインします。
   2. 「Welcome to Adobe Sign」という電子メールを見つけます。 必要に応じてスパム/ジャンクフォルダーを確認します。
   3. 「**[!UICONTROL ここをクリックしてパスワードを設定します]**」というリンクをクリックします。
   4. パスワードを設定します。。

   電子メールアドレスを確認すると、ユーザーのステータスが [!UICONTROL 作成済み] を [!UICONTROL アクティブ]を選択します。

   ![新しくアクティベートされたユーザーの画像](images/active-user.png)

### 管理者権限ユーザーの定義 {#define-authenticating-user}

グループを作成し、そのグループにユーザーを作成したら、ユーザーを「グループ管理者」にする必要があります。

新しいユーザーを [!DNL Coupa BSM Suite] グループ：

1. 次の場所にある [!UICONTROL ユーザー] ページを開きます（まだ開いていない場合）。
2. ユーザーをダブルクリックします。

   開きます。 [!UICONTROL 編集] ページにユーザー権限が表示されます。

3. 「グループメンバーシップ」セクションで、 **[!UICONTROL グループ管理者]** および **[!UICONTROL 送信可能]** を選択します。
4. 選択を解除する **[!UICONTROL ユーザーはアカウント管理者]** および **[!UICONTROL ユーザーは文書に署名できる]** を選択します。
5. 「**[!UICONTROL 保存]**」をクリックします。

   ![ユーザー設定の画像](images/user-settings.png)

## 以下を設定します [!DNL Coupa BSM Suite] instance {#configure-coupa}

DITA マップの [!DNL Coupa BSM Suite ] インスタンスとAdobe Signの間に信頼関係を確立する必要があります。

を使用して、 [!DNL Coupa BSM Suite]:

1. 接続する [!DNL Coupa BSM Suite] インスタンスを作成します。
1. Adobe Sign Webhook インスタンスを作成して、Coupa BSM Suite インスタンスに契約書の更新を通知します。

接続方法の詳細については、 [!DNL Coupa BSM Suite] webhook の作成方法と登録方法については、「 [Adobe Sign Coupa BSM Suite インスタンスのサポートドキュメント](https://success.coupa.com/Support/Docs/Power_Apps/CLM_Standard/Signing_and_Approvals/Enable_E-Signatures_Through_Adobe_Sign_and_DocuSign){target=&quot;_blank&quot;}。

## 作成 [!DNL Webhook] Adobe Sign {#create-webhook}

Coupa CLM 統合では、Adobe Signからの Webhook 通知を使用して、契約書の状態に関する更新を送信します。 Webhook の設定を完了することが重要です。完了しないと、署名用に送信された契約書が不完全なままになるか、署名済みの契約書が Coupa CLM に配信されません。

Adobe Signで Webhook を作成するには：

1. 上記で作成したグループ管理ユーザーを使用して、Adobe Signにログインします。次に例を示します `coupaclm@MyDomain.com`を選択します。

1. 次の場所に移動 **グループ** > **Webhooks**&#x200B;を選択します。

   ![ユーザー設定の画像](images/webhook-login.png)

1. 新しい接続を作成するには、 ![プラスアイコンの画像](images/icon_plus.png) アイコンをクリックします。

1. 表示された作成ダイアログで、必須フィールドに入力します。

   **注意：** Webhook ハンドラーの URL を Coupa から取得する必要があります。

   ![ユーザー設定の画像](images/webhook-create.png)

1. 必要な通知パラメータを選択します。

1. 選択 **保存**&#x200B;を選択します。

## サポート {#support}

### [!DNL Coupa BSM Suite] サポート {#coupa-support}

[!DNL Coupa BSM Suite ] は統合の所有者であり、統合の範囲、機能リクエスト、日常的な統合の機能に関する問題に関する質問に対する最初の問い合わせ窓口になります。

ご不明な点については、 [Coupa サポート](https://success.coupa.com/Support/Welcome_to_Coupa_Support){target=&quot;_blank&quot;}。

### Adobe Signのサポート {#adobe-sign-support}

Adobe Signは統合パートナーであり、統合で署名を取得できなかった場合、または保留中の署名の通知が失敗した場合は、連絡を取る必要があります。

Adobe Signの使用と設定については、カスタマーサクセスマネージャー (CSM) または [Adobe Signのサポート](https://adobe.com/go/adobesign-support-center)を選択します。

Adobe Sign管理者は、ヘルプ (?) を使用してチケットを開いたり、サポートを受けたりすることもできます。 をクリックします。

![Adobe Sign Portal ヘルプの画像](images/sign-portal-help.png)
