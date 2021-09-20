---
title: Workday インストールガイド
description: Adobe Sign と Workday の統合を有効にするためのインストールガイド
uuid: 56478222-fe66-4fa5-aac3-0ecdf2863197
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 29d55a25-6e2f-4c59-ae7c-c21bb82cecba
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8f12b524-2123-45d4-98d5-b2b23580a5ea
source-git-commit: 78d6cafa720b41bd638c2ef723b2d4a2def19cd5
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 21%

---

# [!DNL Workday] インストールガイド{#workday-installation-guide}

[**Adobe Sign サポートへのお問い合わせ**](https://adobe.com/go/adobesign-support-center)

## 概要 {#overview}

このドキュメントでは、Adobe Signを[!DNL Workday]テナントに統合する方法について説明します。 [!DNL Workday]内でAdobe Signを使用するには、次のような[!DNL Workday]アイテムの作成と変更方法を知る必要があります。

* ビジネスプロセスフレームワーク
* テナントの設定と構成
* レポート作成と[!DNL Workday] studioの統合

統合を完了するための高レベルの手順は次のとおりです。

* Adobe Signで管理アカウントを有効にする（新規のお客様のみ）
* [!DNL Workday]統合ユーザーを保持するようにAdobe Signでグループを設定する
* [!DNL Workday]とAdobe Signの間のOAuth関係を確立する

## Adobe Signアカウントを有効にする {#activating-your-adobe-sign-account}

既存のアカウントを持つ既存のお客様は、「[Adobe Sign for [!DNL Workday]](#config)の設定」のトピックに進むことができます。

Adobe Signを初めて使用するお客様で、既存のログインを持たないお客様の場合、Adobeのオンボーディングスペシャリストが[!DNL Workday]のアカウントを（Adobe Signで）プロビジョニングします。 完了すると、次に示す確認の電子メールが届きます。

![Adobe Sign からのようこそメールのイメージ](images/welcome-email-2020.png)

電子メールの指示に従って、アカウントを初期化し、Adobe Sign [!UICONTROL ホーム]ページにアクセスする必要があります。

![Adobe Sign の「ダッシュボード」ページ](images/classic-home.png)

## [!DNL Workday]のAdobe Signの設定 {#config}

[!DNL Workday]用にAdobe Signを設定するには、Adobe Signシステムで次の2つの専用オブジェクトを生成する必要があります。

* **グル [!DNL Workday] ープ**: [!DNL Workday] 統合機能を有効にするには、Adobe Signアカウント内に専用の「グループ」が必要です。Adobe Signグループは、Adobe Signの[!DNL Workday]使用のみを制御するために使用します。 Salesforce.comやArribaなど、他の潜在的な使用法は影響を受けません。 [!DNL Workday]グループでは電子メール通知が抑制され、[!DNL Workday]ユーザーは[!DNL Workday]受信トレイ内でのみ通知を受け取るようになります。

* **統合キーを保持する認証ユーザー**:グル [!DNL Workday] ープには、統合キーの権限を持つグループレベルの管理者が1人だけ必要です。管理者は、個人の電子メールの代わりに`HR@MyDomain.com`などの機能的な電子メールアドレスを使用して、将来ユーザーが無効になり、統合が無効になるリスクを軽減することをお勧めします。

### Adobe Signでのユーザーとグループの作成 {#create-a-user-and-group-in-adobe-sign}

Adobe Sign でユーザーを作成するには：

1. アカウント管理者として Adobe Sign にログインします。。
1. **[!UICONTROL アカウント]** > **[!UICONTROL ユーザー]**&#x200B;に移動します。
1. ![+アイコンイメージ](images/icon_plus.png)をクリックして、新しいユーザーを作成します。

   ![新規ユーザー作成のナビゲーションパスのイメージ](images/navigate-to-group-unbranded.png)

1. 開いたダイアログで、新しいユーザーの詳細を指定します。

   * アクセス可能な機能の電子メールを入力します。
   * 適切な「名」と「姓」の値を入力します。
   * 「ユーザー・グループ」から「**[!UICONTROL このユーザーの新しいグループを作成]**」を選択します。
   * **[!UICONTROL 新しいグループ名]**&#x200B;に、*[!DNL Workday]*&#x200B;のような直感的な名前を付けます。

   ![ユーザーを作成パネル](images/create-user.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

   [!UICONTROL [ユーザー]]ページに戻り、**[!UICONTROL CREATED]**&#x200B;状態の新しいユーザーが表示されます。

   ![新しく作成されたユーザーのビュー](images/post-user-creation.png)

「作成済」ステータスのユーザーの電子メール・アドレスを確認するには、次の手順に従います。

1. 新しいユーザーの電子メールにログインします。
2. 「Adobe Signへようこそ」の電子メールを見つけます。
3. **[!UICONTROL パスワードを設定するには、ここをクリック]**&#x200B;します。
4. パスワードを設定します。

電子メールアドレスを確認すると、ユーザーの状態が[!UICONTROL CREATED]から[!UICONTROL ACTIVE]に変わります。

![新しくアクティブ化されたユーザーのイメージ](images/actived-users-575.png)

### 認証ユーザーの定義 {#define-the-authenticating-user}

[!DNL Workday]グループの新しいユーザーを昇格するには、次の手順に従います。

1. [!UICONTROL ユーザー]ページに移動します（まだ存在しない場合）。
2. [!DNL Workday]グループ内のユーザーをダブルクリックします。

   これにより、ユーザー権限の[!UICONTROL 編集]ページが開きます。

3. **[!UICONTROL Group Admin]**&#x200B;を確認します。
4. 「**[!UICONTROL 保存]**」をクリックします。

![](images/user-permissions-edit1-575.png)

## [!DNL Workday]テナントの構成 {#configure-workday}

[!DNL Workday]テナントとAdobe Signの間の接続を完了するには、サービス間に信頼関係を確立する必要があります。 完了したら、Adobe Signを使用して署名プロセスを有効にする「ドキュメントのレビュー」ステップを追加します。

>[!NOTE]
>
>Adobe Signは、[!DNL Workday]環境全体でAdobe Document Cloudとしてブランド化されています。

信頼関係を確立するには、次の手順を実行します。

1. [!DNL Workday]にアカウント管理者としてログインします。
1. [**[!UICONTROL テナントの設定の編集 – ビジネスプロセス]**]ページを開きます。
1. 「[!UICONTROL 電子サイン設定]」セクションを探します。

   ![](images/esignature_configurations.png)

1. [**[!UICONTROL Adobeで認証]**]をクリックします。

   これにより、OAuth2.0認証シーケンスが開始されます。

1. 要求されたら、前に作成したAdobe署名グループ管理者の資格情報を入力します。
1. Adobe Signへのアクセスを承認します。

>[!NOTE]
>
>続行する前に、他のAdobe Signインスタンスから完全にログアウトしてください。

接続が完了すると、Adobe構成の有効化チェックボックスが設定され、[!DNL Workday]でAdobe Signを使用できるようになります。

### ドキュメントの確認手順の構成 {#configure-review}

「ドキュメントのレビュー」ステップのドキュメントは、次のいずれかです。

* 静的ドキュメント
* 同じビジネス・プロセス内の「ドキュメントの生成」ステップで生成されたドキュメント
* [!DNL Workday]レポートデザイナで作成された書式付きレポート

[Adobe Text Tags](https://adobe.com/go/adobesign_text_tag_guide_jp)を使用して、これらのドキュメントを追加し、Adobe Signing固有のコンポーネントの外観と位置を制御できます。 文書ソースは、ビジネスプロセス定義内に指定する必要があります。ビジネスプロセスの実行中にその場で文書をアップロードすることはできません。

レビュードキュメントステップでAdobe Signを使用する場合に特有な機能は、シリアル化された署名者グループを持つ機能です。 これにより、署名の順番が決められている、役割に基づくグループを指定できます。Adobe Signは並列署名グループをサポートしていません。

ドキュメントの確認手順の構成については、[クイックスタートガイド](https://adobe.com//go/adobesign_workday_quick_start){target=&quot;_blank&quot;}を参照してください。

## サポート {#support}

### [!DNL Workday] 支援 {#workday-support}

[!DNL Workday]この統合の所有者は です。したがって、統合の範囲、機能の要求、日常的処理の問題に関して疑問点が出てきた場合は、まず Workday に問い合わせることになります。

統合のトラブルシューティングとドキュメントの生成に関する次の[!DNL Workday]コミュニティの記事を参照してください。

* [eSignature統合のトラブルシューティング](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [ドキュメントの確認手順](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [動的ドキュメント生成](https://community.workday.com/saml/login?destination=/articles/176443)
* [ドキュメント生成のヒントを提供する](https://community.workday.com/node/183242)

### Adobe Signのサポート {#adobe-sign-support}

Adobe Sign は統合パートナーです。この統合で署名を取得できない場合や、保留中の署名の通知が適切に実行されない場合は、Adobe Sign に問い合わせてください。

Adobe Sign のユーザーは、カスタマーサクセスマネージャー（CSM）に連絡してサポートを受ける必要があります。または、アドビテクニカルサポートに連絡していただくこともできます。その場合は、1-866-318-4100 に電話し、製品リストが読み上げられるのを待って、指示に従って 4、2 の順番に番号を入力します。

* [Adobeテキストタグのドキュメントへの追加](https://adobe.com/go/adobesign_text_tag_guide)
* [ドキュメントの構成と例の確認](https://www.adobe.com//go/adobesign_workday_quick_start)

## よくある質問 {#faq}

### ドキュメントが完全に署名されている場合でも、[!DNL Workday]内でステータスが更新されないのはなぜですか？ {#why-is-the-status-not-being-updated-within-workday-even-the-document-is-fully-signed}

[!DNL Workday]のドキュメントの状態は、候補者がAdobe Signでサインインした後に&#39;[!UICONTROL Submit]&#39;ボタンをクリックしない場合は反映されない可能性があります。

[!DNL Workday]タスクに従って、eSignature署名の状態を確認：プロセスを開始するには、ユーザーは関連する受信トレイタスクを送信します。

[!DNL Workday]開発に従って：元の署名は、ドキュメントに署名した後に受信トレイタスクを送信した場合にのみ、プロセスを完了します。 署名後、iframeが閉じられ、ユーザーは同じタスクにリダイレクトされ、[!UICONTROL [送信]]ボタンをクリックして処理を完了できます。
