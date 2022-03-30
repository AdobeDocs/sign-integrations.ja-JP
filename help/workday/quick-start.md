---
title: Workday クイックスタートガイド
description: Workday環境でAdobe Signを使用するお客様向けのクイックスタートガイドです。
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 25%

---

# [!DNL Workday] クイックスタートガイド{#workday-quick-start-guide}

[**Adobe Sign サポートへのお問い合わせ**](https://www.adobe.com/go/adobesign-support-center)

## 概要 {#overview}

この文書は、 [!DNL Workday] 管理者は、 [!DNL Workday] 電子サインを取得するためのAdobe Signを含むビジネスプロセス。 Adobe Signを [!DNL Workday]を作成する方法と変更する方法を知っている必要があります [!DNL Workday] 項目：

* [!UICONTROL ビジネスプロセスフレームワーク]
* テナントのセットアップと構成
* レポートと [!DNL Workday] Studio Integration

##  内で Adobe Sign にアクセスする[!DNL Workday] {#access-adobe-sign}

[!UICONTROL Adobe Signの電子サイン機能] は [!UICONTROL 「Review Document」ステップ] 内のアクション [!UICONTROL ビジネスプロセスフレームワーク (BPF)] 「文書の配布」タスクとして実行できます。

## [!UICONTROL 「Review Document（文書を確認）」ステップ] {#review-document-step}

Adobe Sign [!DNL Workday] は、 [!UICONTROL 「Review Document」ステップ] 400 を超えるビジネスプロセスを [!DNL Workday]を含む [!UICONTROL 提案], [!UICONTROL ドキュメントとタスクの配布], [!UICONTROL 報酬の提案]など )。

詳しくは、 [[!DNL Workday] 関する地域社会の記事 [!UICONTROL 「Review Document」ステップ]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)を選択します。

A と B の間には 1 対 1 の関係がある [!UICONTROL [!UICONTROL 「Review Document」ステップ]s] また、Adobe Signとの請求可能な取引を確認できます。 複数の文書を 1 つの [!UICONTROL 「Review Document」ステップ] 署名用の単一のパッケージとして表示されます。

**注意**:単一の *動的* ドキュメントは、 [!UICONTROL 「Review Document」ステップ]を選択します。

機能を定義するには [!UICONTROL 「Review Document」ステップ]:

1. 挿入 [!UICONTROL 「Review Document」ステップ]を選択します。
1. 次の条件に従って動作するグループ（役割）を指定します。 [!UICONTROL 「Review Document」ステップ]を選択します。

![ビジネスプロセスのステップ](images/insert-review-doc-steptornm-575.png)

を使用して、 [!UICONTROL 「Review Document」ステップ]:

1. 次の *[!UICONTROL 電子サイン統合タイプ]* を *[!UICONTROL Adobe]*&#x200B;を選択します。

1. 署名グリッドに行を追加します。

   * 署名グリッドには、署名するために文書を送る順序を指定します。各行には、1 つ以上の役割が含まれており、各行は署名プロセスの 1 つのステップを表しています。。
   * 特定のステップ内のロールのすべてのメンバーに、署名イベントが保留中であることが通知されます。
   * ロールの 1 人のユーザーが署名すると、行ステップが完了し、文書が次の行ステップに移動します。
   * すべての行が署名されると、 [!UICONTROL 「Review Document」ステップ] が完了しました。

1. 署名する文書を指定します。文書が [!UICONTROL BP を提供]を使用する場合は、「文書を生成」ステップから使用できます。 それ以外の場合は、既存の文書またはレポートを選択します。

1. 必要な数の文書に対して手順 3 を繰り返します。。

   ![「Review Document（文書を確認）」ステップの設定](images/configure-rd-stepsmaller-575.png)

1. 必要に応じて、「署名を拒否」アクションをキャプチャする「ユーザーをリダイレクト」を追加します。 ユーザーが辞退すると、 [!DNL Workday] ドキュメントをレビュー用に構成されたセキュリティグループに再ルーティングします。

の関連アクションメニューから [!UICONTROL 「Review Document」ステップ]で、 **[!UICONTROL ビジネスプロセス]** > **[!UICONTROL リダイレクトの管理]**&#x200B;を選択します。 次に、次のいずれかを選択します。

* **[!UICONTROL 返信]**:セキュリティ・グループ・メンバーが、ステップをビジネス・プロセスの前のステップに戻すことができるようにする。 ビジネスプロセスはそのステップから再開します。
* **[!UICONTROL 次のステップに移動]**:セキュリティ・グループ・メンバーがステップをビジネス・プロセスの次のステップに転送できるようにする。
* **[!UICONTROL セキュリティグループ]**:ビジネス・プロセス・フローのステップをリダイレクトします。 このプロンプトを表示するセキュリティグループは、[ リダイレクト ] セクションのビジネスプロセスセキュリティポリシーで選択します。

## ビジネスプロセスステップのメモ {#business-process-step-notes}

[!UICONTROL ビジネスプロセスフレームワーク] は強力だ。ただし、次のことを確認する必要があります。

* すべてのビジネス・プロセスには完了ステップが必要です。これは、理想的にはビジネス・プロセスの最後です。

* 完了ステップは、検索アイコンの関連アクションメニューに設定されます。 これは、BP を「表示」している間にのみ可能であり、「編集」している間は可能ではありません。

* ビジネスプロセスの各ステップは順番に実行されます。

   順序の値を変更することで、ステップの順序を変更できます。 例えば、「c」と「d」の間にステップを挿入するには、新しいアイテムを「ca」と指定します。

### 例：オファー {#example-offer}

「Offer」BP は、 [!UICONTROL 求人動態血圧] 「Offer」BP を実行するように設定する必要があります。 ジョブ・アプリケーションの状態が「[!UICONTROL 提案]&quot;または&quot;[!UICONTROL 提案]&quot;.

次の例では、 [!UICONTROL 「Review Document」ステップ] では、北米と日本の両方でダイナミックドキュメントのステップを使用しています。

![[!DNL Workday] ビジネスプロセスの例](images/bp-for-offersmaller-575.png)

この BP では、以下の処理をおこないます。

* BP の開始者に、候補に対する補償の提案を求めます（ステップ b）。
* ステップ条件を使用して、現在の国が日本ではないかどうかをテストします。

   true の場合、英語のドキュメントを使用するステップ「ba」が実行されます。

   false の場合は、日本語ドキュメントを使用するステップ「bb」が実行されます。

* 署名プロセスを [!UICONTROL 「Review Document」ステップ] &quot;bc&quot;
* 必要な完了ステップ「d」でオファーを行う決定ポイントを定義します。

ステップ「ba」で生成される動的な文書は「[!UICONTROL Offer Letter（オファーレター）]」と呼ばれ、「[!UICONTROL Rapid Offer（迅速なオファー）]」という名前の単一のテキストブロックを含んでいます。必要に応じて、ヘッダー、あいさつ、報酬、株式、期末、条件などの複数のテキストブロックを追加できます。

![[!DNL Workday] ドキュメントページの表示](images/offer-letter-575.png)

以下の動的なオファーレターは、 [!DNL Workday] リッチテキストエディター、 ハイライトされた項目 *グレー* は [!DNL Workday] コンテキストデータを参照する提供されたオブジェクト。

{{括弧内}} の項目は、[アドビのテキストタグ](https://adobe.com/go/adobesign_text_tag_guide_jp)です。

![動的フォームの例](images/script.png)

内 [!UICONTROL 「Review Document」ステップ]を使用すると、動的な文書が前の手順から参照され、2 つの署名グループによる順次署名プロセスが定義されます。

以下に示す動作は、動的に生成された文書を最初に採用マネージャーに転送し、次に候補者に転送します。

![[!DNL Workday] 定義されている署名グループ](images/configure-rd-stepsmaller-575.png)

### 例：文書の配布 {#example-distribute-documents}

導入 [!DNL Workday] 30、「文書またはタスクの一括配布」タスクを使用して、1 つの文書を大きなグループ (&lt;20K) の個々の署名者に送信できます。 文書 1 件あたり署名 1 件に制限されます。ディストリビューションの作成は、「[!UICONTROL 配布文書またはタスクの作成]」アクションを入力します。

例：従業員の格差選択フォームをすべてのマネージャーに送信 [!UICONTROL Global Modern Services]を選択します。 必要に応じて、さらに個々のマネージャーにフィルターできます。

また、 **表示/文書またはタスクの配布** 配布の進行状況を追跡するレポート。

![](images/create-distributedocumentsortasks.png)

### 例：レポート {#example-reporting}

[!DNL Workday] は、優れたレポートインフラストラクチャを備えています。Adobe Sign プロセスの詳細を確認するには、「*Review Document Event*（文書イベントを確認）」の要素を調査します。

以下に、Adobe Sign トランザクションおよびそのステータスを必要とするすべての BP に対して実行できる、シンプルなカスタムレポートを示します。

![[!DNL Workday] カスタムレポートの例](images/review-document-eventsmaller-575.png)

以下のレポートは、実装テナント内の「Offer（オファー）」、「Onboarding（オンボーディング）」および「Propose Compensation（報酬を提案）」の各 BP を参照して生成されています。

以下の内容を確認できます。

* 署名用に送信される文書
* 関連する BP ステップ
* 署名を待っている次のユーザー

![[!DNL Workday]3 つのオブジェクトを使用した レポートの例](images/workday-reportsmaller-575.png)

## 署名済み文書 {#signed-documents}

この [!DNL Workday] 署名サイクルでは、Adobe Signによるすべての電子メール通知が抑制されます。 ユーザーには、自分の [!DNL Workday] 受信トレイ。

文書がすべての署名グループによって署名されると、署名された文書のコピーが署名グループのすべてのメンバーに電子メールで配布されます。

この動作を抑制するには、 [!UICONTROL Adobe Sign Success Manager] または [Adobe Sign Support team](https://adobe.com/go/adobesign-support-center)を選択します。

範囲内 [!DNL Workday]をクリックすると、すべてのプロセスレコードで署名済み文書にアクセスできます。 次のことが分かります。

* 作業者プロファイルの作業者ドキュメント
* 候補者プロファイルの候補文書（オファーレター）。

以下の画像は、候補者 Chris Foxx の署名済みのオファーレターを示しています。

![例 [!DNL Workday] オファーレター](images/offer.png)

## サポート {#support}

### [!DNL Workday] サポート {#workday-support}

[!DNL Workday]この統合の所有者は です。したがって、統合の範囲、機能の要求、日常的処理の問題に関して疑問点が出てきた場合は、まず Workday に問い合わせることになります。

この [!DNL Workday] コミュニティには、統合のトラブルシューティング方法やドキュメントの生成方法に関する次のような優れた記事があります。

* [電子サイン統合のトラブルシューティング](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [「Review Document（文書を確認）」ステップ](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [動的な文書の生成](https://community.workday.com/node/176443)
* [オファー文書生成の設定のヒント](https://community.workday.com/node/183242)

### Adobe Signのサポート {#adobe-sign-support}

Adobe Sign は統合パートナーです。この統合で署名を取得できない場合や、保留中の署名の通知が適切に実行されない場合は、Adobe Sign に問い合わせてください。

Adobe Signのお客様は、カスタマーサクセスマネージャーに連絡してサポートを受ける必要があります。 または、 [!UICONTROL Adobeテクニカルサポート] 電話番号：1-866-318-4100, wait for product list then enter:プロンプトに従って 4 と 2

* [文書へのアドビのテキストタグの追加](https://www.adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
