---
title: Adobe Sign for [!DNL NetSuite]  – インストールとカスタマイズガイド(v4.0.4)
description: Adobe Sign for [!DNL NetSuite]  – インストールとカスタマイズガイド
product: Adobe Sign
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 378cac01-87c9-4288-8839-482121d49402
source-git-commit: f8d0bc748872e675dc1c638eb4050efe9e3147ef
workflow-type: tm+mt
source-wordcount: '4870'
ht-degree: 32%

---

# [!DNL NetSuite] インストールとカスタマイズガイド(v4.0.4) {#install-customize-NetSuite}

## 概要 {#overview}

[!DNL NetSuite]向けAdobe Signは、[!DNL NetSuite]との完全なeSignature統合を提供します。 [!DNL NetSuite]との統合にAdobe Signを使用すると、契約、見積書、電子署名が必要なその他の文書などの契約を[!DNL NetSuite]から直接受信者に送信できます。 お客様、リード、見積り、その他の[!DNL NetSuite]レコードからAdobe Sign契約を作成して送信できます。 Adobe Signは、契約のステータスで[!DNL NetSuite]を更新し、完全に実行された後、関連する[!DNL NetSuite]レコードと契約を保存します。 [!DNL NetSuite]から送信されたすべての契約の履歴は、製品内から表示できます。

詳細は、[Adobe Sign for [!DNL NetSuite] リリースノート](https://experienceleague.adobe.com/docs/sign-integrations/using/netsuite/release-notes.html?lang=en)を参照してください。

## バンドルをインストールし、OAuthを構成します {#install}

[!DNL NetSuite]管理者のみがバンドルをインストールまたは更新できます。 OAuthを設定するには、[!DNL NetSuite]管理者がAdobe Signに対する管理者アクセス権を持っている必要があります。 本番アカウントにバンドルをインストールする前に、[!DNL NetSuite] Sandboxアカウントにバンドルをインストールし、テストする必要があります。

テストの詳細については、「[Adobe署名契約の作成](#createagreement)」を参照してください。

>[!CAUTION]
>
>v4.0.4にアップグレードするお客様は、既存のAPIキーを削除しないでください。
>
>APIキーの使用方法の詳細は、[「カスタムプリファレンスを設定する](#configure)」を参照してください。

### バンドルを初めてインストールする

1. [!UICONTROL **Customization／SuiteBundler／Search &amp; Install Bundles**] に移動します。

1. *「バンドルの検索とインストール*」ページで、キーワードとして&#x200B;**Adobe Sign**&#x200B;を入力し、**[!UICONTROL 「検索]**」を選択します。

1. **Adobe Sign**&#x200B;バンドル名を選択します。

   ![バンドルの検索](images/search-for-the-bundle.png)

1. [*[!UICONTROL バンドルの詳細]*]ページで、[**[!UICONTROL インストール]**]を選択します。
1. 「*[!UICONTROL バンドルのプレビュー]*」ページで、「**[!UICONTROL バンドルのインストール]**」を選択します。

   （ページ上のデフォルト値を変更する必要はありません）。

   ![バンドルのインストール](images/bundle-details-install.png)

1. 表示される[インストール]ダイアログで、[**[!UICONTROL OK]**]を選択して続行します。

   インストールプロセスの実行中、バンドルのステータスには「*[!UICONTROL Pending]*」と表示されます。

   ![バンドルのインストール](images/installing-bundles.png)

1. 更新された状態を表示するには、[**[!UICONTROL 更新]**]を選択します。

   バンドルのインストールが完了すると、*[!UICONTROL Installed Bundles]* ページに *Adobe Sign for[!DNL NetSuite]* が表示されます。

   ![インストール済みバンドル](images/installed-bundles.png)

1. すでにAdobe Signのお客様アカウントをお持ちの場合は、](#oauth)をインストールまたはアップグレードした後、[「OAuthを構成する」の手順に従ってください。

   Adobe Signアカウントをお持ちでない場合は、[エンタープライズ試用版](https://esign.adobe.com/adobe-sign-[!DNL NetSuite]-trial-registration.html)アカウントにサインアップして、システムをテストできます。 オンラインの登録手順に従って、Adobe Sign アカウントを有効にしてください。

## インストールまたはアップグレード後にOAuthを構成する {#oauth}

Adobe SignはOAuth 2.0を使用して、[!DNL NetSuite]内でAdobe Signアカウントを認証します。

このプロトコルは、インストール済みの[!DNL NetSuite]バンドルが、パスワードを要求せずにAdobe Signと通信することを許可します。 アプリケーション間で機密情報が直接共有されないので、アカウントが危険にさらされる可能性が低くなります。

この認証は実装に影響を与えませんが、本番アカウントまたはサンドボックスアカウントにバンドルをインストールまたはアップグレードした後、1回限りの構成を行う必要があります。

OAuthを構成する[!DNL NetSuite]管理者は、Adobe Signに対するアカウントレベルの管理者アクセス権も持っている必要があります。

1. [!DNL NetSuite]で、*Adobe Sign Config*&#x200B;のリストページに移動します。

1. ヘッダーの「検索」フィールドを使用して、**[!UICONTROL Adobe Sign Config]** （カスタムレコードタイプ）を検索します。

1. 「検索結果」ページで、*Adobe署名構成*&#x200B;レコードに対して「**表示**」を選択します。

   ![Search for Adobe Sign](images/search-for-adobesignconfig.png)

1. 「Adobe Sign Config List」ページで、「*Using OAuth to Access Adobe Sign APIs*」レコードに「**[!UICONTROL View]**」を選択します。

   ![Adobe Sign の設定リスト](images/adobe-sign-configlist.png)

1. Adobe Sign Configページで、「**[!UICONTROL Adobe Signでログイン]**」を選択します。

   ![ログイン ](images/log-in-with-adobesign.png)

1. 表示されるAdobe署名のログインページで、資格情報を入力し、[**[!UICONTROL サインイン]**]を選択します。

   ![Adobe Sign での認証](images/8-authenticate-toadobesign-2020.png)

1. 表示される[アクセスの確認]ページ（OAuthの場合）で、[**[!UICONTROL アクセスの許可]**]を選択します

   ![アクセスを許可](images/confirm-access.png)

1. 認証が完了すると、次に示すように、[!DNL NetSuite]のAdobe Sign Configページにリダイレクトされます。

   ![成功した OAuth](images/successful-oauth.png)

   >[!NOTE]
   >
   >SandboxアカウントでOAuthを構成する際に、承認が完了すると、「Could not determine customer comp ID」というエラーが表示される場合があります。
   >
   >
   >続行するには、URL （システム）のアカウントドメイン部分を変更する必要があります。[!DNL NetSuite].com)を使用して、次のようにサンドボックスを指 [!DNL NetSuite] すようにします。
   >
   >
   >変更:
   >
   >
   >system.[!DNL NetSuite].com/app/site/hosting/scriptlet.nl?script=745&amp;deploy=1&amp;web_access_point=https://echosign.com
   >
   >
   >宛先 :
   >
   >
   >システム&#x200B;**sandbox.**[!DNL NetSuite].com/app/site/hosting/scriptlet.nl?script=745&amp;deploy=1&amp;web_access_point=https://echosign.com

## バンドルの更新（既存のユーザー）

[!DNL NetSuite] バンドルの更新は、Adobe社が定期的にリリースします。[!DNL NetSuite]統合用のAdobe Signの既存のユーザは、最新のバンドルに更新できます。

>[!CAUTION]
>
>新しいバージョンにアップグレードするユーザーは、既存の API キーを削除しないでください。
>
>API キーの仕組みに関する詳細については、「[カスタム環境設定の指定](#configure)」を参照してください。

### 前提条件 {#prerequisites}

v4.0.4バンドルの更新に必要な時間は、現在「署名に対して送信」ステータスの免除承諾の数に依存します。 通常、100件の契約を更新するには7～10分かかります。 アップデート時間を見積もるレコード数をメモします。

署名のために締め出された基本契約の数を決定する手順は、次のとおりです。

1. **[!UICONTROL [カスタマイズ]>[リスト、レコード、およびファイル]>[レコードの種類]]**&#x200B;に移動し、*Adobe Sign Agreementを探します。*

   または、検索バーでAdobe Sign Agreementsを検索します。

1. [!UICONTROL Adobe Sign Agreements]レコードに対して、**[!UICONTROL 「検索」]**&#x200B;を選択します。

   ![レコードタイプの検索](images/search-adobe-signagreements.png)

1. [**[!UICONTROL 状態]**]ドロップダウンから、[署名&#x200B;]**]に[**[!UICONTROL &#x200B;送信]を選択し、[**[!UICONTROL 送信]**]を選択します。

   ![「署名用に送信」を選択して送信](images/submit-search-foragreements.png)

   アップデート時間を見積もるレコード数をメモします。

   ![数をメモ](images/search-results.png)

### バンドルの更新 {#updating-the-bundle}

1. **[!UICONTROL [カスタマイズ]>[SuiteBundler]>[検索とインストール]>[リスト]]**&#x200B;に移動し、次に示すように現在のバンドルを探します。

   >[!NOTE]
   >
   >新しいバージョンのバンドルが存在する場合は、現在のバンドルの&#x200B;*バージョン*&#x200B;番号の右側に感嘆符アイコンが表示されます。

1. [操作]ドロップダウンメニューから、[**[!UICONTROL 更新]**]を選択します。

   ![アップデートのアクション](images/update-action.png)

1. 「バンドル更新のプレビュー」ページで、ページに表示されるデフォルト値を変更せずに「**[!UICONTROL バンドルの更新]**」を選択します。

   インストール中、バンドルのステータスは&#x200B;*保留*&#x200B;と表示されます。

   ![バンドルアップデートのプレビュー](images/preveiw-bundles-update.png).

   >[!NOTE]
   >
   >バンドルを更新する際に、次のような警告メッセージが表示される場合があります。 [!DNL NetSuite] eSignatureレコードをカスタマイズしていない場合は、続行できます。 不明な場合は、本番アカウントのバンドルを更新する前に、まずSandboxアカウントにバンドルをインストールしてテストすることをお勧めします。

   ![エラーメッセージ](images/netsuite-error.png)

1. 更新された状態を表示するには、[**[!UICONTROL 更新]**]を選択します。

   ![アップグレードのインストール](images/installing-upgrade.png)

   >[!NOTE]
   >
   >*「署名*&#x200B;の送信」ステータスとの合意が複数あるため、更新に時間がかかる場合は、*Adobe Sign Bundle Installation*&#x200B;スクリプトの「**[!UICONTROL 実行ログ]**」サブタブを確認して、更新の進行状況を確認できます。 詳細は、[更新の進行状況の確認](#determineprogress)を参照してください。

   バンドルアップデートの完了後、*Installed Bundles* ページに「*Adobe Sign for[!DNL NetSuite]*」が表示されます。

   ![インストール済みパッケージ](images/4-installed-bundles.png)

## バンドルの構成 {#configure}

### カスタム環境設定の設定  {#set-custom-preferences}

カスタムプリファレンスを使用して、免除承諾の作成方法と[!DNL NetSuite]への保存方法を指定できます。 また、*「Adobe Sign*&#x200B;のユーザーの自動プロビジョニング」環境設定では、[!DNL NetSuite]から契約を送信する際に、[!DNL NetSuite]ユーザーが署名サービスで自動プロビジョニングを行うかどうかを指定できます。

1. **[!UICONTROL Setup／Company／General Preferences]** に移動します。
1. ページを下にスクロールし、「**[!UICONTROL カスタムプリファレンス]**」サブタブを選択します。

   ![カスタム環境設定](images/custom-preferences.png)

1. 必要に応じて、Adobe Signの環境設定を有効にし、設定します。

   * **アカウントのEchoSign APIキーを入力**:このフィールドの値を追加または編集しないでください。
   * **親レコードの連絡先を署名者として使用**:有効にすると、基本契約の作成時に、親レコードの連絡先が最初の署名者として既定で設定されます。送信者は、契約書を送信する前に、容易にデフォルト署名者を削除または編集したり、その他の署名者を追加したりできます。
   * **Use Trans.署名者として連絡する（存在する場合）**:この設定は、*[親レコードの連絡先を署名者として使用*]設定も有効になっている場合にのみ有効です。 有効な場合、取引レコード（Quoteなど）から基本契約を生成する際に、主要取引担当者が最初の署名者としてデフォルト設定されます。 詳細は、[Transaction Records](#transrecords)を参照してください。 主要な取引担当者が存在しない場合、または[!DNL NetSuite]オブジェクト・レコード（顧客レコード、パートナー・レコードなど）から送信する場合、デフォルトの受信者は顧客の電子メールの主要な担当者です。 送信者は、契約書を送信する前に、容易にデフォルト署名者を削除または編集したり、その他の署名者を追加したりできます。
   * **受信者を承認者としてマークする**:有効にすると、送信者は受信者を承認者としてマークできます。承認者としてマークされた受信者は契約書を確認して承認できますが、署名する必要はありません。承認者は、承認プロセス中にフィールドへのデータの入力を求められることがあります。
   * **優先契約フォルダID**:最終署名済み契約を保存するフォルダを指定します。このフィールドに値を設定しない場合は、最終的な署名済み契約書はデフォルトで元の文書ファイルと同じフォルダーに保存されます。フォルダー ID は数値でなければなりません。
   * **トランザクションの自動添付PDF**:有効にすると、トランザクションPDFは、トランザクションレコードから新しい契約が作成されるときに、自動的に契約に添付されます。
   * **署名付きPDFを追加（添付ファイルまたはリンク）**:ドロッ ** プダウンから「リスト」を選択すると、署名付きPDFがファイルへのリンクとして自動的に追加されます。ドロップダウンから「*Attachment*」を選択した場合は、署名済み PDF が契約レコードの添付ファイルとして に保存されます。[!DNL NetSuite]
   * **契約付きの監査証跡PDFを含む**:有効にすると、契約に署名した後、監査証跡のPDFが自動的に契約レコードに添付されます。
   * **本人確認方法の適用先**:識別確認方法を有効にすると、識別確認方法が適用されるユーザーが決まります。*すべての署名者、外部署名者のみ*、*内部署名者のみ*&#x200B;を選択できます。

   **Identity Verification Methods** {#identity-verification-methods}

   契約書を作成するときに有効にする ID 確認方法を選択できます。ここで複数のID確認方法を有効にした場合、Adobe Sign Agreementページに「署名者IDの確認&#x200B;]**」オプションが表示されます。**[!UICONTROL 

   * **署名に必要なパスワードを有効にする**:指定したワンタイムパスワードの入力を署名者に要求します。

   * **ナレッジベース認証の有効化**:署名者に、SSNの名前、住所、およびオプションでSSNの最後の4桁を入力し、入力した情報を確認する質問のリストに回答するように要求します。米国でのみ使用できます。

   * **Web ID認証を有効にする**:次のサイトのいずれかにサインインして、署名者に本人確認を要求する：Facebook、Google、LinkedIn、Microsoft Live、Twitter、またはYahoo!

   * **Adobe Signでのユーザーの自動プロビジョニング**:有効にすると、で契約を送信するユーザーは、Adobe Signユ [!DNL NetSuite] ーザーアカウントを使用して自動的にプロビジョニングされます。


1. 「**[!UICONTROL 保存]**」を選択して、環境設定を保存します。

## 自動状態更新の構成 {#asu}

Adobe Sign統合バンドルを使用すると、[!DNL NetSuite]から送信された契約のステータスに関する更新を[!DNL NetSuite]で自動的に受け取ることができます。 この機能が有効な場合、[!DNL NetSuite]は常に契約の状態を反映します。 自動ステータス更新を有効にするには、以下のことを実行します。

1. **[!UICONTROL 「設定」>「会社」>「機能の有効化」]に移動します。**
1. **[!UICONTROL SuiteCloud]**&#x200B;サブタブを選択します。
1. 以下のオプションを有効にします。

   * 「SuiteBuilder」セクションで、「**[!UICONTROL Custom Records]**」オプションを有効にします。

   * 「SuiteScript」セクションで、「**[!UICONTROL Client SuiteScript]**」オプションと「**[!UICONTROL Server SuiteScript]**」オプションを有効にし、両方の利用規約に同意します。

1. **[!UICONTROL 保存]**&#x200B;を選択します。

   オプションは、図に示すように設定されます。

   ![SuiteCloud 機能の有効化](images/enable-suitecloudfeatures.png)

## オブジェクトとレコードタイプ {#objects}

Adobe Sign統合バンドルでは、Adobe Sign Agreementオブジェクトが既に公開されており、次のような多数の標準[!DNL NetSuite]オブジェクトが含まれています。お客様、見積もり、リード、オポチュニティ、パートナーの各レコード カスタムレコードも含め、これ以外のレコードタイプでも Adobe Sign バンドルを使用できます。

「承諾」タブは、次の2種類の[!DNL NetSuite]レコードで表示できます。エンティティおよびトランザクションレコード。 通常、トランザクションレコードは、PDFドキュメントに変換できるレコード（見積もりなど）であると想定します。一方、EntityレコードはPDFに変換できません。

## トランザクションレコード {#transrecords}

取引レコードから契約を作成する場合、契約レコードの最初の文書は、取得元のレコードのPDFバージョンで、最初の受信者はレコードの電子メールアドレスです。 最初のドキュメントを元のレコードのPDFバージョンにしない場合は、**[!UICONTROL 「設定」>「会社」>「一般設定」>「カスタム・プリファレンス」サブタブ]**&#x200B;に移動し、**[!UICONTROL 「トランザクションPDFの自動添付」]**&#x200B;オプションを無効にします。 詳細は、[カスタムプリファレンスの設定](#configure)を参照してください。

「Custom Preferences」で「**[!UICONTROL Use Trans.Contact as First Signer]**」環境設定を有効にして、トランザクションの主担当者を自動的に最初の署名者として追加することもできます。トランザクションレコードに関連付けられている場合は、**[!UICONTROL 契約]**&#x200B;と&#x200B;**[!UICONTROL 署名用に送信]**&#x200B;ボタンが表示されます。

![見積](images/quote.png)

## エンティティレコード {#entity-records}

契約がエンティティ・レコードから作成される場合、最初の受信者はレコードの電子メール・アドレスです。 エンティティレコードに関連付けられている場合は、「Agreements」タブだけが表示されます。

## バンドルのカスタマイズ {#customize}

バンドルのカスタマイズには、以下の作業が含まれます。

* 適切なレコードタイプに、「Agreements」サブタブと「Send for Signature」ボタンのスクリプトを導入します。
* Adobe Sign レコードタイプの役割権限を設定します。
* 権限を変更して、「*Agreements*」サブタブと「*Send for Signature*」ボタンへのアクセスを許可します。

![スクリプト](images/scripts.png)

### 追加のレコードの種類に対するAdobe Sign契約の設定  {#configuring-adobe-sign-agreements-for-additional-record-types}

適切なレコード・タイプに対して&#x200B;*「契約*」サブタブと&#x200B;*「署名用に送信*」ボタンを配置するには、次の手順に従います。

1. **[!UICONTROL Customization／Scripting／Scripts] に移動します。**

1. 表示される&#x200B;*スクリプト*&#x200B;のリストページで、配備する必要のあるスクリプトを探し、****[!UICONTROL [表示]]****&#x200B;を選択します。

   * *「署名用に送信」*&#x200B;ボタンを追加するには、**[!UICONTROL 「Adobe署名の見積もり」ボタン]**&#x200B;スクリプトを選択します。

   * *「契約*」タブを追加するには、**[!UICONTROL Adobe Sign Agreement Loader]**&#x200B;スクリプトを選択します。

1. [スクリプト]ページで、[**[!UICONTROL スクリプトの展開]**]を選択します。

   ![スクリプトの導入](images/deploly-script.png)

1. Script Deployment ページで、以下のようにします。

   * *Applies To* リストからレコードのタイプを選択します。
   * オプションで、スクリプト導入 ID を入力することもできます

      詳細については、[!DNL NetSuite]ヘルプ・センターの「*カスタム・スクリプト展開ID*&#x200B;の作成」を参照してください。 ID を入力しなかった場合は ID が生成されます。

   * 「**[!UICONTROL Deployed]**」チェックボックスをオンにします。

   ![スクリプトの導入](images/execute-as-admin.png)

   * 「*Status*」を「**[!UICONTROL Released]**」に設定します。

      *イベントの種類*&#x200B;または&#x200B;*ログレベル*&#x200B;を指定しないでください。

   * 「[!UICONTROL *役割として実行]*」ドロップダウンから、「**[!UICONTROL 管理者として実行]**」を選択します。

   * 「**[!UICONTROL 対象ユーザー]**」サブタブをアクティブにした状態（デフォルトではアクティブ）で、アクセスを許可する特定のロールまたはユーザーを選択します。 すべての役割およびユーザーにアクセスを許可する場合は、それぞれ「**[!UICONTROL Select all]**」オプションを有効にします。

   * **[!UICONTROL 保存]**&#x200B;を選択します。 変更の確認が表示されたら、[**[!UICONTROL 戻る]**]を選択します。


1. [スクリプトの展開]ページの上部で[**[!UICONTROL リスト]**]を選択し、[*スクリプト*]リストページに戻ります。
1. 他のスクリプトに対しても上記の手順 2 と手順 3 を繰り返します。

## Adobe Sign レコードタイプの役割権限の設定 {#setting-role-permissions-for-adobe-sign-record-types}

ほとんどの[!DNL NetSuite]ロールは、追加のカスタマイズを行わずにAdobe Signを使用する権限を持つ必要があります。 ただし、作成された追加のカスタムロールに対しては、パーミッションを付与する必要があります。

1. **[!UICONTROL Customization／Lists, Records, &amp; Files／Records Types]** に移動します。

   ![SiteBuilder の「Custom Records」](images/sitebuilder-customrecords.png)

   >[!NOTE]
   >
   >「*Record Types*」アイテムが表示されない場合は、**[!UICONTROL Setup／Company／Enable Features／「Suite Cloud」]**&#x200B;タブに移動して「*Custom Records*」オプションを有効にします。

1. [*レコードの種類*]ページで、[**[!UICONTROL Adobe署名契約]**]を選択して選択します

   ![契約レコードタイプ](images/search-adobe-signagreementsforedit.png)

1. [*カスタムレコードの種類*]ページで、[*アクセスの種類*]ドロップダウンリストから[**[!UICONTROL アクセス許可リスト]**&#x200B;を使用]を選択します。

   ![カスタムレコードタイプ](images/custom-record-type.png)

   >[!NOTE]
   >
   >「*Use Permission List*」アクセスタイプを必要とする Adobe Sign レコードタイプは、「*Adobe Sign Agreement*」レコードタイプだけです。
   >
   >
   >その他の Adobe Sign レコードタイプのアクセスタイプを設定する手順については、手順 6 を参照してください。

1. [**[!UICONTROL 権限]**]サブタブを選択します。

   役割と権限のリストが表示されます。

   ![役割と権限](images/roles-and-permissions.png)

1. 「[!UICONTROL Adobe Sign Agreement]」レコード・タイプに追加された追加のカスタム・ロールに対して、次の権限を設定します。

   >[!NOTE]
   >
   >カスタム・レコード・タイプの&#x200B;*[権限リストの設定](https://system)を参照してください。[!DNL NetSuite]詳細については、ヘルプセンターのトピ* ック。com/app/help/helpcenter.nl?fid=section_N2879931.html) [!DNL NetSuite] を参照してください。

   1. 「*Role*」リストから役割を選択します。
   1. *レベル*&#x200B;を&#x200B;**[!UICONTROL 完全]**&#x200B;に設定します。
   1. *既定のフォーム*&#x200B;を&#x200B;**[!UICONTROL カスタムEchoSign契約フォーム]**&#x200B;に設定します。
   1. [**[!UICONTROL フォームを制限]**]チェックボックスをオンにします。
   1. [**[!UICONTROL 追加]**]を選択して、役割行の変更を保存します。

   ![権限の設定](images/set-permissions.png)

   新しい行が次のように表示されます。

   ![契約レコードタイプの権限の設定](images/set-permissions-foragreementrecordtype.png)

   他のカスタム役割についても上記の手順 a から手順 e を繰り返します。

   * すべてのロールに対する権限が設定されたら、[*カスタムレコードの種類*]ページで[**[!UICONTROL 保存]**]を選択します。
   *[!UICONTROL 「Customer Record Type」]*&#x200B;ページが再表示されます。

1. 他のすべての Adobe Sign レコードタイプについても上記の手順 1 から手順 3 を繰り返して、「*Access Type*」を

   **[!UICONTROL 権限は必要ありません]。**」に設定します。以下のレコードタイプが対象となります。

   * Adobe Sign Config
   * Adobe Sign 文書
   * Adobe Sign Event
   * Adobe Sign Language
   * Adobe Sign Script Errors
   * Adobe Sign Signed Agreement
   * Adobe Sign Signer

### [契約]タブと[署名用に送信]ボタンへのアクセスを許可する  {#granting-access-to-the-agreement-tab-and-send-for-signature-button}

Adobe Sign統合バンドルは、多くの標準[!DNL NetSuite]オブジェクト（お客様、見積もり[見積]、リードなど）を含むAdobe Sign Agreementオブジェクトを既に公開しています。 「*Agreement*」サブタブは、以下のタイプのオブジェクトで自動的に有効になります：カスタマー、リード、商談、パートナー、見込み客、見積、ベンダー請求書。

*[!UICONTROL [署名の送信]]*&#x200B;ボタンは、Quoteオブジェクト&#x200B;]**に対してのみ** o[!UICONTROL 自動的に有効になります。

[!DNL NetSuite] 管理者は、機能を拡張して追加の CRM オブジェクトに契約書を作成できるようにできます。それには、CRM オブジェクトに「*Agreement*」サブタブ、「*Send for Signature*」ボタン、またはその両方を追加できるように権限を変更します。

#### 権限を変更して「Send for Signature」ボタンへのアクセスを許可  {#modifying-permissions-to-grant-access-to-the-send-for-signature-button}

1. **[!UICONTROL Customization／Scripting／Scripts]** に移動します。

   *Scripts* リストページが表示されます。

   * 必要に応じて、フィルタを使用してAdobe Signスクリプトを検索します

1. *スクリプト*&#x200B;ページで、*Adobe Sign Estimate Button*&#x200B;スクリプトを探し（*署名の送信*&#x200B;ボタンを制御）、**表示**&#x200B;を選択します。

   ![「View Adobe Sign Estimates」ボタン](images/view-adobe-sign-estimatesbutton.png)

1. *Script* ページで、以下のようにします。

   * [**[!UICONTROL 配置]**]サブタブを選択します。

   * 「*適用先*」で、変更するエンティティのリンクを選択します。

      * この例では&#x200B;**[!UICONTROL 見積]**&#x200B;です。

   ![[配置]サブタブを選択します。](images/click-the-deploymentssub-tab.png)

   * *スクリプト展開*&#x200B;ページの&#x200B;**[!UICONTROL 「]**&#x200B;を編集」ボタンを選択します

   ![スクリプト導入を編集](images/edit-script-deployment.png)

   * [**[!UICONTROL 対象ユーザー]**]サブタブをアクティブにし、アクセスを許可する特定のロールまたはユーザーを選択します。

      * すべての役割およびユーザーにアクセスを許可する場合は、それぞれ「**[!UICONTROL Select all]**」オプションを有効にします。
   * **[!UICONTROL 保存]**&#x200B;を選択

   ![特定の役割の選択](images/save-script-deployment-quote.png)

#### 権限を変更して「Agreements」タブへのアクセスを許可  {#modifying-permissions-to-grant-access-to-the-agreements-tab}

1. **[!UICONTROL Customization／Scripting／Scripts]** に移動します。
1. [[!UICONTROL スクリプト]]ページで、*[!UICONTROL Adobe Sign Agreement Loader]*&#x200B;スクリプト（*[契約]タブ*&#x200B;を制御）を見つけ、[**[!UICONTROL 表示]**]を選択します。
1. *Script* ページで、以下のようにします。

   1. [**[!UICONTROL 配置]**]サブタブを選択します
   1. 「*[!UICONTROL 適用先]*」で、アクセス権を変更するエンティティのリンクを選択します
   1. [*[!UICONTROL スクリプト展開]*]ページで、[**[!UICONTROL 編集]**]ボタンを選択します
   1. 「**[!UICONTROL Audience]**」サブタブがアクティブな状態で（デフォルトでアクティブになっています）、アクセスを許可する役割またはユーザーを選択します。すべての役割およびユーザーにアクセスを許可する場合は、それぞれ「**[!UICONTROL Select all]**」オプションを有効にします。
   1. **[!UICONTROL 保存]**&#x200B;を選択

## [!DNL NetSuite]バンドル用のAdobe Signの使用

[!DNL NetSuite]から契約を送信し、その契約の更新を受け取るには、[!DNL NetSuite]とAdobe Signで同じログインID （電子メールアドレス）を使用する必要があります。

### Adobe Sign 契約書の作成

サンドボックスまたは本番アカウントで新しいバンドルをインストールした後、新しい契約書を作成してバンドルをテストしてください。Adobe Sign 契約書は、エンティティレコードまたはトランザクションレコードから、あるいはスタンドアロンの契約書として作成できます。

>[!NOTE]
>
>契約書の作成プロセスは、どの方法で作成するかによって若干異なります。一般的なプロセスとしては、契約書のオプションを指定し、1つまたは複数の契約書文書を追加し、受信者を指定します。以下に説明するプロセスでは、カスタマーレコードから契約書を作成する場合を想定しています。

1. 契約を送信する顧客レコードを選択または作成するか、「契約」タブが有効になっている別の[!DNL NetSuite]レコード・タイプを選択できます。

1. レコードから、「**[!UICONTROL 契約]**」サブタブを選択します。
1. **[!UICONTROL 新しい契約]**&#x200B;を選択します。

   ![新規契約書](images/new-agreement.png)

1. *[!UICONTROL Adobe署名契約]*&#x200B;ページで、[**[!UICONTROL 編集]**]を選択します。

   ![新規契約書の編集](images/edit-new-agreement.png)

1. 契約書のオプションを次のように指定します。

   * **「契約名** 」(Agreement Name) – 免除承諾の名前を入力します。
   * **「メッセージ**」(Message) – 受信者のカスタムメッセージを入力します。
   * **Signature Type -**&#x200B;文書で受け付ける署名タイプを選択します。オプションは、*e-Signature*&#x200B;と&#x200B;*Fax Signature*&#x200B;です。

   * **「この契約に署名する必要があります** 」 – 送信者も契約に署名する必要があることを示すには、このオプションを有効にします。
   * **署名の順序**- 「この契約に署名する *必要がある」オプシ* ョンが有効な場合は、送信者と受信者が署名する順序を選択します。オプションには、「I sign, then recipients sign」、「Recipients sign, then I sign」と「None」があります。

   * **ドキュメントまたは職位署名（またはフォームフィールド）**  – 送信者が契約をプレビューし、受信者に送信する前に承諾にフィールド（ドラッグアンドドロップ署名、初期フィールド、およびその他のフォームフィールド）を追加できるようにする場合に、このオプションを有効にします。
   * **「署名者のIDの確認** 」 – このオプションを有効にして、次のID確認オプションの1つを選択します

      * このオプションは、以下に示す 3 つの ID 確認方法のうち 2 つ以上が「Custom Preferences」で有効にされている場合にのみ表示されます。（詳細は、[カスタムプリファレンスの設定](#customize)を参照してください）。 有効になっている環境設定が 1 つしかない場合は、「**[!UICONTROL Verify Signer Identity]**」オプションは表示されません。

   **Identity Verification Methods**

   * **「署名に必要なパスワード** 」 – 署名者に、指定したワンタイムパスワードの入力を要求します。
   * **知識ベース認証**  – 署名者に、SSNの名前、住所、およびオプションでSSNの最後の4桁を入力し、提供された情報を確認する質問のリストに回答する必要があります。米国でのみ使用できます。
   * **Web ID認証**  – 次のサイトの1つにサインインして、署名者にIDの確認を要求します。Facebook, Google, LinkedIn, Twitter, Yahoo!または Microsoft Live です。
   * **「PDFを表示するためのパスワードが必要** 」 – 受信者が契約または署名済みの契約のPDFを開く前にパスワードを入力することを要求する場合は、このオプションを有効にします。すべてのユーザーに送信されるPDFファイルは暗号化され、開くにはパスワードが必要です。 パスワードは復元できないので、忘れないように注意してください。パスワードを失った場合は、そのトランザクションを削除し、再び開始する必要があります。
   * **「パスワード/パスワードの確認** 」 – 「 ** PDFの表示に必要なパスワード」オプションが有効になっている場合、免除承諾の表示に使用するパスワードを入力します。
   * **「署名する受信者に通知** 」 – 受信者に通知を送信するかどうか、および送信する頻度を指定します。オプションには、「*Never*」、「*Daily*」と「*Weekly*」があります。
   * **言語：** 署名ページと電子メール通知を受信者に表示する言語を指定します。
   * **「最初の署名者のホスト署名** 」 – このオプションを有効にすると、送信者ホストが最初の署名者に対して直接署名できます。
   * **「署名期限までの日数** 」 – 契約の署名期限（今日の日付+日数）を示す整数を入力します。
   * **「親レコード** 」(Parent Record) – オプションで、親レコードを選択して基本契約にリンクします。

   ![契約書の設定](images/configure-agreement-2.png)

1. [**[!UICONTROL ドキュメント]**]タブを選択します。

   ![「Documents」タブ](images/documents-tab.png)

1. 「*ドキュメント*」サブタブで、「*Adobe署名ドキュメント*」ドロップダウンを使用して、ファイルキャビネットから既存のドキュメントを添付し、「**[!UICONTROL 添付]**」を選択します。

   または、**[!UICONTROL 「新規Adobe署名ドキュメント]**」をクリックして&#x200B;*[!UICONTROL Adobe署名ドキュメント]*&#x200B;ページにアクセスし、[!DNL NetSuite]ファイルキャビネットでドキュメントの名前を入力し、トランザクションレコードからファイルを選択するか、新しいドキュメントを添付します。

   1 つの契約書に複数の文書を追加できます。

1. [**[!UICONTROL 受信者]**]サブタブを選択し、連絡先リストから選択するか、電子メールアドレスを入力して受信者を指定します。

   ![受信者の追加](images/add-recipients.png)

   受信者はそれぞれ、署名者または CC としてマークできます。「*Allow Marking Recipients as Approvers Signers*」カスタム環境設定が有効な場合は、受信者を承認者としてマークすることもできます。詳細は、[カスタムプリファレンスの設定](#customize)を参照してください。

   * **署名者**&#x200B;は、契約書に署名する必要があります。
   * **承認者** は承認する必要がありますが、契約に署名しないでください。また、必要に応じて、契約にデータを追加する必要があります。
   * **CCの受信者には、** 契約の更新と契約の署名と完了が通知されます。CC 受信者は、署名または承認プロセスの参加者ではありません。

      「*Use Parent Record Contact as Signer*」カスタム環境設定が単独で、または「*Use Trans.Contact as Signer*」環境設定と共に有効にされている場合、最初の受信者はデフォルトで決定されますが、変更も可能です。

1. 各受信者を入力した後、**[!UICONTROL [追加]]**&#x200B;を選択します。

1. 「**[!UICONTROL 保存]**」を選択して、契約を保存します。

### 署名の契約を送信

契約を送信する準備が整ったら、[**[!UICONTROL 署名用に送信]**]ボタンを選択します。

* *[文書または位置の署名のプレビュー]*&#x200B;オプションが有効な場合は、[**[!UICONTROL 署名用に送信]**]をクリックします。 開いたウィンドウで、ドキュメントをプレビューするか、フォームフィールドをドキュメントにドラッグしてから送信します。 [**[!UICONTROL 送信]**]を選択して、契約を受信者に送信します。

* *[!UICONTROL [最初の署名者のホスト署名]*]オプションが有効な場合は、[**[!UICONTROL 署名の送信]**]をクリックします。 開いたウィンドウで、署名者が送信者が存在するドキュメントに署名できるようにします。

   「*Host Signing for First Signer*」フィールドの隣に表示される「*Host Signing for Current Signer*」リンクは、文書に署名し終わるまで使用できます。このリンクを使用して、複数の署名者に契約書に署名してもらったり、ポップアップウィンドウを誤って閉じてしまった場合は開き直したりできます。

契約が送信されると、受信者は署名待ちの文書を通知する電子メールを受け取ります。

受信者が文書に署名し終わると、送信者は、文書が署名されたことを知らせる電子メールを受信します。

#### 見積もりから送信

Adobe Signは、[!DNL NetSuite]のQuoteと直接統合されているため、QuoteのPDFが自動的に生成され、契約レコードに添付されます。

Quoteを表示する場合は、「**[!UICONTROL Send for Signature]**」を選択します。 契約に添付された見積もりを生成し、表示します。 「*Send for Signature*」ボタンは、他のトランザクションレコードタイプにも追加できます詳細は、[オブジェクトとレコードの種類](#objects)を参照してください。

![見積の「Send for Signature」](images/quote-send-forsignature.png)

### 状況の追跡とアラームの送信

契約書を送信した後：

* 契約書の詳細セクションで、文書のステータスが「*Out for Signature*」に変化します。
* [*署名を送信*]ボタンは、次の3つのボタンに置き換えられます。

   * **「ステータスの更新** 」(Update Status) – ステータスの更新が構成されていない場合に、ステータスを手動で更新します。詳細は、[自動ステータス更新の構成](#asu)を参照してください。
   * **「アラームを送信** 」 – 現在の署名者にアラームを送信します。
   * **契約の取消**  – 契約を取り消します。契約書を署名用に送信した後でも、まだすべての受信者が署名していなければ、キャンセルできます。

![署名用に送信](images/out-for-signature.png)

新しい「*Events*」サブタブが契約レコードに表示され、ここで契約書のステータスをトラックできます。

契約イベントの履歴が表示され、契約書が送信、表示および署名された日付などの情報を確認できます。

![署名済み契約書のイベント](images/agreement-events.png)

契約書が署名された後：

* ステータスが「*Signed*」に変化します。。
* リンクを使用して、この契約の親レコードにリンクできます。
* 「署名付きドキュメント」と「監査証跡」の下の「ダウンロード」リンクを使用して、これらのドキュメントにアクセスできます。
* 署名されたドキュメントのサムネイルを表示するには、追加の&#x200B;*署名されたドキュメント*&#x200B;サブタブが表示されます。

![署名済み契約](images/signed-agreement.png)

>[!NOTE]
>
>署名の契約が送信された後は、レコードを編集できません。 これは、イベントの記録を保持するためです。

## バンドルのアンインストール

バンドルをアンインストールするには、[!DNL NetSuite]ヘルプの手順に従います。 詳細については、[!DNL NetSuite]ヘルプセンターのトピック「*[バンドルのアンインストール](https://docs.oracle.com/cloud/latest/[!DNL NetSuite]cs_gs/NSBDL/NSBDL.pdf)*」を参照してください。

バンドルをアンインストールすると、署名されていない免除承諾が削除されます。 署名済みの契約と対応する監査PDFファイルは影響を受けません。

未署名の契約を保持する必要がある場合は、バンドルをアンインストールしないでください。

## トラブルシューティング

### 更新の進行状況を確認します

アップデートに長い時間がかかっている場合は、Adobe Sign Bundle Installation スクリプトの「Execution Log」サブタブでアップデートの進行状況を確認できます。それには以下を実行します。

1. **[!UICONTROL Customization／Scripting／Scripts]** に移動します。
1. 「[!UICONTROL スクリプト]」ページで、*[!UICONTROL Adobe Sign Bundle Installation]*&#x200B;スクリプトを探し、**[!UICONTROL 「編集]**」を選択します。
1. [[!UICONTROL スクリプト]]ページで、[**実行ログ**]サブタブを選択します。
1. **更新**&#x200B;を選択します。

   実行ログが更新され、ステータスが反映されます。 「*Details*」列に、契約書の更新状況が表示されます。

   ![進行状況の更新](images/refresh-progress.png)

### アクセストークンの問題の解決

契約との対話中に、「指定されたアクセストークンは無効か、期限切れです」というメッセージが表示される場合があります。

これには以下の理由が考えられます。

* OAuthを構成した[!DNL NetSuite]/Adobe Sign管理者がアクセストークンを取り消しました
* 過去60日間に[!DNL NetSuite]から契約が送信されなかったため、アクセストークンの有効期限が切れました
* [!DNL NetSuite]/Adobe Sign管理者は、初期OAuth構成を正常に完了しませんでした

この問題を解決するには、OAuth構成プロセスを再度実行します。 詳細については、「[インストールまたはアップグレード後の OAuth の設定](#oauth)」を参照してください。

![無効なトークン](images/invalid-token.png)

### ドキュメントの状態に関する問題の解決 {#resolvestatus}

[自動ステータス更新](#asu)が構成されていて、契約の送信後に契約のステータスが更新されない場合は、次の操作を行ってください。

1. *Adobe Sign External Update* スクリプトの導入実行ログで、Adobe Sign からの呼び出しを受信できているか確認します。それには以下を実行します。

   1. **[!UICONTROL Customization／Scripting／Script Deployments]** に移動します。
   1. *「スクリプトの展開*」ページで、*Adobe Sign External Update*&#x200B;スクリプトを探し、**[!UICONTROL 「編集]**」を選択します
      1. [*[!UICONTROL スクリプト展開]*]ページで、[**[!UICONTROL 実行ログ]**]サブタブを選択します。
      * 各契約IDに&#x200B;*更新された契約レコード*&#x200B;のエントリが表示されます


1. *Adobe Sign Update Agreements* スクリプトの導入実行ログを調べてエラーがないか確認します。それには以下のようにします。

   1. **[!UICONTROL [カスタマイズ]>[スクリプト]>[スクリプトの展開]]**&#x200B;に移動します。
   1. 「[!UICONTROL スクリプトの展開]」ページで、「[!UICONTROL スケジュール]」ステータスの&#x200B;*[!UICONTROL Adobe Sign Update Agreements]*&#x200B;スクリプトを探し、**[!UICONTROL 「編集]**」を選択します。
   1. [[!UICONTROL スクリプト展開]]ページで、[**[!UICONTROL 実行ログ]**]サブタブを選択します。
   1. [[!UICONTROL 型]]で、[**[!UICONTROL エラー]**]を選択して結果をフィルタします。

1. 最後に、上記の手順 2 の説明に従い、*Adobe Sign Manager* スクリプトの実行ログでエラーがないか確認します。

### MIMEタイプエラーの解決  {#resolving-mime-type-errors}

免除承諾の送信時にMIMEタイプのエラーが発生した場合は、「ファイル名」(File Name)フィールドの名前が、アップロードされたファイルのファイル名と拡張子と一致しない可能性があります。 「ファイル名」(File Name)フィールドを空白のままにすると、正しいファイル名と拡張子が自動的に入力されます。

### スクリプトログの表示 {#viewing-script-logs}

導入実行ログは、文書ステータスの問題に関連しないスクリプトに対しても表示することができます詳細は、[ドキュメントの状態に関する問題の解決](#resolvestatus)を参照してください。

1. **[!UICONTROL Customization／Scripting／Scripts]** に移動します。

   *Scripts* リストページが表示されます。必要に応じて、フィルターを使って適切なスクリプトを見つけます。

1. 対応するスクリプトの&#x200B;**[!UICONTROL View]**&#x200B;を選択します。

1. ページの「**[!UICONTROL 実行ログ]**」サブタブを選択し、スクリプト・ログを表示します。

## サポート {#support}

FAQ、ドキュメント、ナレッジベース記事、またはAdobeサポートに問い合わせるには、[Adobe Sign Supportポータル](https://adobe.com/go/adobesign-support-center)にアクセスしてください。
