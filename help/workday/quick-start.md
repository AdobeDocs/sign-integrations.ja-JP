---
title: Workday クイックスタートガイド
description: Adobe Signを職場環境で使用するお客様向けのクイックスタートガイド。
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
source-git-commit: 5ac9dc27dcdb6cab19281e6aafd4ea0524cc01d6
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 25%

---

# [!DNL Workday] クイックスタートガイド{#workday-quick-start-guide}

[**Adobe Sign サポートへのお問い合わせ**](https://www.adobe.com/go/adobesign-support-center)

## 概要 {#overview}

このドキュメントは、[!DNL Workday]管理者が、Adobe署名を含めて電子署名を取得する[!DNL Workday]ビジネスプロセスをカスタマイズする方法を理解するのに役立ちます。 [!DNL Workday]内でAdobe Signを使用するには、次のような[!DNL Workday]アイテムの作成と変更の方法を知っている必要があります。

* [!UICONTROL ビジネスプロセスフレームワーク]
* テナントの設定と構成
* レポート作成と[!DNL Workday] Studio統合

##  内で Adobe Sign にアクセスする[!DNL Workday] {#access-adobe-sign}

[!UICONTROL Adobe署名の電子署名機能は、ビジネ] スプロセスフレームワーク(BPF)内の「ドキュメントのレビュー」ステップアクションとして、 [!UICONTROL およびドキュメントの配布]   タスクとして提供されています。

## [!UICONTROL 「Review Document（文書を確認）」ステップ] {#review-document-step}

[!DNL Workday]のAdobe Signは、[!UICONTROL ドキュメントのレビュー手順]を通じて公開され、[!DNL Workday]内で400を超えるビジネスプロセスに追加できます。[!UICONTROL オファー]、[!UICONTROL ドキュメントとタスクの配布]、[!UICONTROL 報酬の提案]など。

[!UICONTROL レビュードキュメントの手順]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)に関する[[!DNL Workday] コミュニティの記事を参照してください。

[!UICONTROL [!UICONTROL ドキュメントのレビュー手順]]とAdobe Signとの請求可能なトランザクションとの間には、1対1の関係があります。 複数のドキュメントを1つの[!UICONTROL レビュードキュメントステップ]内で組み合わせ、署名用の単一のパッケージとして表示できます。

**注**:特定の「ドキュメントのレビ ** ュー」ステップ内で参照できるのは、1つの [!UICONTROL Dynamicdocumentだけです]。

機能[!UICONTROL ドキュメントのレビュー手順]を定義するには、次の手順に従います。

1. [!UICONTROL レビュードキュメントステップ]を挿入します。
1. [!UICONTROL ドキュメントのレビュー手順]に対して実行できるグループ（ロール）を指定します。

![ビジネスプロセスのステップ](images/insert-review-doc-steptornm-575.png)

[!UICONTROL ドキュメントのレビュー手順]を構成するには：

1. *[!UICONTROL eSignature Integration type]*&#x200B;を&#x200B;*[!UICONTROL eSign by Adobe]*&#x200B;として指定します。

1. 署名グリッドに行を追加します。

   * 署名グリッドには、署名するために文書を送る順序を指定します。各行には、1 つ以上の役割が含まれており、各行は署名プロセスの 1 つのステップを表しています。。
   * 特定のステップ内のロールのすべてのメンバに、署名イベントが保留中であることが通知されます。
   * ロール記号から1人のユーザーが入力すると、行の手順が完了し、ドキュメントが次の行の手順に移動します。
   * すべての行に署名が付いたら、[!UICONTROL ドキュメントのレビュー手順]が完了します。

1. 署名する文書を指定します。ドキュメントが[!UICONTROL BP]を提供する場合は、「ドキュメントを生成」ステップから使用できます。 それ以外の場合は、既存の文書またはレポートを選択します。

1. 必要な数の文書に対して手順 3 を繰り返します。。

   ![「Review Document（文書を確認）」ステップの設定](images/configure-rd-stepsmaller-575.png)

1. 必要に応じて、「署名を拒否」するアクションをキャプチャする「リダイレクトユーザー」を追加します。 ユーザーが辞退した場合、[!DNL Workday]は構成されたセキュリティグループにドキュメントを再ルーティングして確認します。

[!UICONTROL 「ドキュメントのレビュー手順]」の関連アクションメニューから、**[!UICONTROL 「ビジネスプロセス]**」>「**[!UICONTROL リダイレクトの保守]**」を選択します。 次に、次のいずれかを選択します。

* **[!UICONTROL 返信]**:セキュリティグループメンバが、業務プロセスの前のステップにステップバックを送ることを可能にする。ビジネスプロセスはそのステップから再開します。
* **[!UICONTROL 次のステップに移動]**:セキュリティグループのメンバが、ビジネスプロセスの次のステップにステップを転送できるようにする。
* **[!UICONTROL セキュリティグループ]**:ビジネス・プロセス・フロー内のステップをリダイレクトする。このプロンプトに表示されるセキュリティグループは、[リダイレクト]セクションのビジネスプロセスセキュリティポリシーで選択されます。

## 業務プロセスの手順に関するメモ {#business-process-step-notes}

[!UICONTROL ビジネス・プロセス・フレ] ームワークは強力で、ただし、次の点を確認する必要があります。

* すべてのビジネス・プロセスには完了ステップが必要です。これは、ビジネス・プロセスの最後の段階にあるのが理想的です。

* 検索アイコンの関連するアクションメニューには、完了ステップが設定されます。 これは、BPを「表示」している場合にのみ可能で、「編集」している場合は可能ではありません。

* ビジネス・プロセスの各ステップが順次実行される。

   ステップの順序は、順序の値を変更することで変更できます。 たとえば、項目&quot;c&quot;と&quot;d&quot;の間にステップを挿入するには、新しい項目を&quot;ca&quot;と指定します。

### 例：申し出 {#example-offer}

オファーBPは、オファーBPを実行するように構成する必要がある[!UICONTROL ジョブアプリケーション動的BP]のサブプロセスです。 ジョブアプリケーションの状態が&quot;[!UICONTROL Offer]&quot;または&quot;[!UICONTROL Make Offer]&quot;に移動されると、これがトリガーされます。

次の例では、[!UICONTROL ドキュメントのレビュー手順]で、北米と日本の両方に対してダイナミックドキュメント手順を使用しています。

![[!DNL Workday] ビジネスプロセスの例](images/bp-for-offersmaller-575.png)

この BP では、以下の処理をおこないます。

* BPの開始者に対し、候補者に対する補償の提案を求める（ステップb）。
* 現在の国が日本国でないかどうかを調べるステップ条件を使用します。

   trueの場合、英語のドキュメントを使用するステップ&quot;ba&quot;が実行されます。

   falseの場合、日本語のドキュメントを使用するステップ&quot;bb&quot;が実行されます。

* [!UICONTROL ドキュメントのレビュー手順] &quot;bc&quot;で署名プロセスを定義します。
* 必要な完了ステップ「d」でオファーを行う際の決定ポイントを定義します。

ステップ「ba」で生成される動的な文書は「[!UICONTROL Offer Letter（オファーレター）]」と呼ばれ、「[!UICONTROL Rapid Offer（迅速なオファー）]」という名前の単一のテキストブロックを含んでいます。ヘッダー、あいさつ文、報酬、株式、決算、条件など、必要に応じて複数のテキスト・ブロックを追加できます。

![[!DNL Workday] ドキュメントページの表示](images/offer-letter-575.png)

次の動的な提供文字は、[!DNL Workday]リッチテキストエディタで作成されます。 *グレー*&#x200B;でハイライト表示された項目は、コンテキストデータを参照する[!DNL Workday]提供されたオブジェクトです。

{{括弧内}} の項目は、[アドビのテキストタグ](https://adobe.com/go/adobesign_text_tag_guide_jp)です。

![動的フォームの例](images/script.png)

[!UICONTROL ドキュメントのレビュー手順]内では、動的ドキュメントは前の手順から参照され、2つの署名グループを介して連続署名プロセスを定義します。

次に示す動作は、動的に生成されたドキュメントを最初に採用マネージャに、次に候補者にルーティングします。

![[!DNL Workday] 署名グループの定義](images/configure-rd-stepsmaller-575.png)

### 例：ドキュメントの配布 {#example-distribute-documents}

[!DNL Workday] 30で導入された「ドキュメントの一括配布」または「タスク」タスクを使用して、1つのドキュメントを各署名者の大きなグループ(&lt;20K)に送信できます。 文書 1 件あたり署名 1 件に制限されます。配布物の作成は、検索バーから「[!UICONTROL ドキュメントの配布またはタスクの作成]」アクションにアクセスして実行します。

例：[!UICONTROL グローバル・モダン・サービス]を持つすべてのマネージャに、従業員の自己資本選択フォームを送信します。 必要に応じて、個々のマネージャにフィルタを適用することもできます。

**[配布ドキュメントの表示]または[タスク**]レポートにアクセスして、配布の進行状況を追跡することもできます。

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

## 署名付きドキュメント {#signed-documents}

[!DNL Workday]署名サイクルは、Adobe Signによるすべての電子メール通知を抑制します。 [!DNL Workday]受信トレイ内の保留中の操作がユーザーに通知されます。

すべての署名グループがドキュメントに署名すると、署名済みドキュメントのコピーが電子メールで署名グループのすべてのメンバに配布されます。

この動作を抑制するには、[!UICONTROL Adobe Sign Success Manager]または[Adobe Sign Supportチーム](https://adobe.com/go/adobesign-support-center)に問い合わせてください。

[!DNL Workday]内では、完全なプロセスレコード上の署名済みドキュメントにアクセスできます。 次の情報が表示されます。

* 作業者プロファイルの作業者ドキュメント
* 候補者プロファイルの候補文書（提出書）。

次の図は、候補のChris Foxxに対する署名済みのオファー・レターを示しています。

![オファー [!DNL Workday] レターの例](images/offer.png)

## サポート {#support}

### [!DNL Workday] 支援 {#workday-support}

[!DNL Workday]この統合の所有者は です。したがって、統合の範囲、機能の要求、日常的処理の問題に関して疑問点が出てきた場合は、まず Workday に問い合わせることになります。

[!DNL Workday]コミュニティには、統合のトラブルシューティングとドキュメントの生成に関する優れた記事がいくつかあります。

* [電子サイン統合のトラブルシューティング](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [「Review Document（文書を確認）」ステップ](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [動的な文書の生成](https://community.workday.com/node/176443)
* [オファー文書生成の設定のヒント](https://community.workday.com/node/183242)

### Adobe Signのサポート {#adobe-sign-support}

Adobe Sign は統合パートナーです。この統合で署名を取得できない場合や、保留中の署名の通知が適切に実行されない場合は、Adobe Sign に問い合わせてください。

Adobe Signのお客様は、Customer Success Managerにお問い合わせください。 また、[!UICONTROL Adobeテクニカルサポート]に電話で連絡することもできます。1-866-318-4100。製品リストを待ってから、次のように入力します。4、2の順に入力します（プロンプトが表示されます）。

* [文書へのアドビのテキストタグの追加](https://www.adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
