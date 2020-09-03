---
title: SharePoint ソリューションのトラブルシューティング |Microsoft Docs
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Tools.SharePoint.Errors.Debugging
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, troubleshooting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: fcb30056021a865d0b0e605de462ff72ced5a383
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "73661893"
---
# <a name="troubleshoot-sharepoint-solutions"></a>SharePoint ソリューションのトラブルシューティング
  以下の問題または警告は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーを使用して SharePoint ソリューションをデバッグするときに発生することがあります。 詳細については、「 [SharePoint 2007 ワークフローソリューションのデバッグ](https://msdn.microsoft.com/3a5392f3-66f3-48be-956e-02de23fa6247)」を参照してください。

## <a name="token-restrictions-in-sandboxed-visual-web-parts"></a>サンドボックス化される視覚的 web パーツでのトークン制限
 サンドボックス ソリューションの視覚的 Web パーツは、SharePoint ランタイムでサポートされる $SPUrl などの標準トークンを処理できません。 そのため、URL は解決されず、次の例のように、スクリプト要素でこのトークンを直接参照する場合、視覚的 Web パーツ デザイナーのデザイン ビューでコンテンツをプレビューできません。

```xml
<script src="<% $SPUrl:~site/SiteAssets/ListOperations.js %>"></script>
```

 この制限を回避し、トークンを解決するには、次のようにリテラルを使用してトークンを参照します。

```xml
<asp:literal ID="Literal1" runat="server" Text="<script src='" />
<asp:literal ID="Literal2" runat="server" Text="<% $SPUrl:~site/SiteAssets/ListOperations.js %>" />
<asp:literal ID="Literal3" runat="server" Text="' type='text/javascript' ></script>" />
```

## <a name="character-restrictions-in-names-of-projects-and-project-items"></a>プロジェクトとプロジェクトアイテムの名前の文字制限
 プロジェクトとプロジェクト アイテムの名前には、SharePoint 2010 の配置パスで有効な文字だけを使用できます。 他の文字は使用できません。

### <a name="error-message"></a>エラー メッセージ
 "無効な文字" エラーメッセージ。

### <a name="resolution"></a>解決方法
 SharePoint のプロジェクトとプロジェクト アイテムの名前では、次の文字だけを使用してください。

- ASCII 英数字

- Space

- ピリオド (.)

- コンマ (,)

- アンダースコア (_)

- ダッシュ (-)

- 円記号 (\\)

  プロジェクトがパッケージされるとき、検証規則により、配置される各ファイルの配置パス プロパティに有効な文字だけが含まれていることが確認されます。

## <a name="errors-when-creating-custom-fields"></a>カスタムフィールドの作成時のエラー
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、カスタム フィールドは、XML で定義されます。 フィールドが特定の形式で定義または参照されていない場合、エラーが発生する可能性があります。

### <a name="error-message"></a>エラー メッセージ
 パッケージ化時の "無効な文字" エラーメッセージ。

### <a name="resolution"></a>解決方法
 フィールド定義の ID には、次の例のように、中かっこで囲まれた GUID を指定する必要があります。

```xml
<Field ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Type="Note"
    Name="PatientName"
    DisplayName="Patient Name"
    Group="A Custom Group">
</Field>.
```

 次の例に示すように、コンテンツ型のフィールド参照は、 \<FieldRef /> start/end 要素 () を使用するのではなく、空の要素形式 () を使用して定義する必要があり \<FieldRef> \</FieldRef> ます。

```xml
<FieldRef ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Name="PatientName"
    DisplayName="Patient Name"
    Required="TRUE"/>
```

 フィールドのソース XML の形式が間違っている場合、有効な XML ファイルでない場合、またはその他の問題がある場合、"ファイルを解析できません" エラーが発生します。

## <a name="new-non-english-site-definitions-do-not-appear-in-site-creation-page-after-deployment"></a>英語以外の新しいサイト定義が、展開後にサイトの作成ページに表示されない
 英語以外のバージョン (つまり、ロケールが1033以外のバージョン) を使用してサイト定義を作成および展開した後 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] 、[Sharepoint の **カスタマイズ** ] タブが **テンプレート選択** ボックスに表示されず、新しいサイトテンプレートが [ **新しい sharepoint サイト** ] ページに表示されません。

### <a name="error-message"></a>エラー メッセージ
 なし。

### <a name="resolution"></a>解決方法
 この問題は、 *webtemp_SiteDefinitionProject1.xml*などの webtemp サイト定義構成ファイルの**Path**プロパティの値が正しくないことが原因で発生します。 **配置場所**の下にある webtemp ファイルの**Path**プロパティで、1033を適切なロケールに変更し [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] ます。 たとえば、日本語のロケールを使用する場合は値を 1041 に変更します。 詳細については、「 [Microsoft によって割り当てられているロケール ID](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)」を参照してください。

## <a name="error-appears-when-a-workflow-project-is-deployed-on-a-clean-system"></a>クリーンシステムにワークフロープロジェクトが配置されるときにエラーが表示される
 この問題は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のワークフロー プロジェクトをクリーン システムに配置した場合に発生します。 クリーン システムとは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] と SharePoint の新しいインストールが含まれているが、ワークフロー プロジェクトは配置されていないコンピューターです。

### <a name="error-message"></a>エラー メッセージ
 SharePoint リストが見つかりません: ワークフローの履歴。

### <a name="resolution"></a>解決方法
 このエラーが発生するのは、ワークフローの履歴リストがないからです。 開発環境がクリーン システムの場合、ワークフローが配置されていないため、ワークフローの履歴リストはまだ存在しません。 この問題を解決するには、ワークフロー ウィザードをもう一度開きます。これにより、ワークフローの履歴リストが作成されます。

##### <a name="to-reenter-the-workflow-wizard"></a>ワークフロー ウィザードを再実行するには

1. **ソリューションエクスプローラー**で、[ワークフロー] ノードを選択します。

2. [ **プロパティ** ] ウィンドウで、省略記号ボタンがあるプロパティの省略記号ボタン ([...]) を選択します。

## <a name="user-must-refresh-application-page-in-browser-while-debugging-to-view-updated-image"></a>更新されたイメージを表示するにはデバッグ中にブラウザーのアプリケーションページを更新する必要があります
 デバッグしている SharePoint ソリューションに、イメージを表示するコントロール ([!INCLUDE[TLA2#tla_html](../sharepoint/includes/tla2sharptla-html-md.md)] Image コントロールなど) を含むアプリケーション ページが含まれている場合に、そのイメージに対して行われた変更を表示するには、ブラウザーでページを更新する必要があります。

## <a name="error-the-site-location-is-not-valid"></a>エラー: サイトの場所が無効です
 この問題は、[!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] がインストールされていない場合に発生することがあります。 また、 **Sharepoint カスタマイズウィザード**で指定された sharepoint Web サイトに対する管理者アクセス権がない場合にも発生する可能性があります。

### <a name="error-message"></a>エラー メッセージ

- 入力されている SharePoint サイトの場所が有効ではありません。

### <a name="resolution"></a>解決方法

- [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]をインストールする。

- SharePoint Web サイトに対する管理者の権限があることを確認します。 詳細については、 [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] オンラインの記事「 [SharePoint Server でのサービスアプリケーションの管理者の割り当てまたは削除](/sharepoint/administration/assign-or-remove-administrators-of-service-applications)」を参照してください。

## <a name="site-deletion-web-event-does-not-occur-in-event-receiver-project"></a>イベントレシーバープロジェクトでサイト削除 web イベントが発生しない
 イベント レシーバー プロジェクトを作成し、"サイトが削除されています" などの特定の Web イベントを選択すると、イベントは発生しません。

### <a name="error-message"></a>エラー メッセージ
 なし。

### <a name="resolution"></a>解決方法
 この問題は、サイト レベルのイベントを処理するにはフィーチャーのスコープが "サイト" である必要があるのに、イベント レシーバー プロジェクトの既定のフィーチャー スコープが "Web" になっているために発生します。 影響を受ける Web イベントは次のとおりです。

- サイトが削除されています (WebDeleting)

- サイトが削除されました (WebDeleted)

- サイトが移動されています (WebMoving)

- サイトが移動されました (WebMoved)

  この問題を修正するには、イベント レシーバーのフィーチャー スコープを次のように変更します。

##### <a name="to-change-the-feature-scope-of-the-event-receiver"></a>イベント レシーバーのフィーチャー スコープを変更するには

1. **ソリューションエクスプローラー**で、ファイルをダブルクリックするか、そのショートカットメニューを開き、[**開く**] を選択して、**機能デザイナー**でイベントレシーバーの*機能*ファイルを開きます。

2. [ **スコープ**] の横にある矢印をクリックし、表示される一覧で [ **サイト** ] を選択します。

## <a name="deployment-error-appears-after-the-name-of-an-identifier-in-a-business-data-connectivity-model-project-is-changed"></a>ビジネスデータ接続モデルプロジェクト内の識別子の名前が変更された後に配置エラーが表示される
 この問題は、ビジネス データ接続 (BDC) モデルでエンティティの識別名を変更した後、ソリューションを配置しようとすると発生します。

### <a name="error-messages"></a>エラー メッセージ

- \<*model name*> 次の外部コンテンツタイプのアクティブ化エラーがあります...

- ' ' という名前の IMetadataObject には、 \<*model name*> 重複しているフィールド ' Name ' の値が含まれています...

### <a name="resolution"></a>解決方法
 この問題を解決するには、モデルを手動で削除した後、ソリューションを再び配置します。  モデルを削除するには、次のどちらかのツールを使用します。

- SharePoint 2010 サーバーの全体管理。 詳細については、Microsoft TechNet Web サイトの「 [BDC モデル管理](/previous-versions/office/sharepoint-server-2010/ee524073(v=office.14)#delete-a-bdc-model) 」を参照してください。

- Windows PowerShell。 モデルを削除するには、コマンドプロンプトで「 **SPBusinessDataCatalogModel**」と入力します。 詳細については、Microsoft TechNet Web サイトの「 [一般的なコマンドレット (SharePoint Server 2010)](/powershell/module/sharepoint-server) 」を参照してください。

## <a name="an-error-appears-when-you-try-to-view-a-visual-web-part-in-sharepoint"></a>SharePoint で視覚的 web パーツを表示しようとするとエラーが表示される
 この問題は、ユーザーコントロールの **Path** プロパティが文字列 "controltemplates" で始まらない場合に発生し \\ ます。

### <a name="error-messages"></a>エラー メッセージ

- ファイル '/_CONTROLTEMPLATES/ *\<project name>* / *\<Web Part name>* / *\<user control name>* .ascx ' が存在しません。

- Server Error in '/' Application.

### <a name="resolution"></a>解決方法

##### <a name="to-resolve-this-issue"></a>この問題を解決するには

1. **ソリューションエクスプローラー**で、ファイル名拡張子が *.ascx*であるユーザーコントロールファイルを選択します。

2. メニューバーで、[ **View**  >  **プロパティウィンドウ**の表示] を選択します。

3. [ **プロパティ** ] ウィンドウで、[ **配置場所** ] ノードを展開します。

4. **Path**プロパティの値が文字列 "controltemplates" で始まることを確認し \\ ます。

## <a name="error-appears-when-an-imported-reusable-workflow-that-contains-a-task-form-field-is-run"></a>タスクフォームフィールドを含むインポートされた再利用可能なワークフローを実行すると、エラーが表示される
 この問題は、フィールドを含むタスク フォームが存在するワークフローをインポートした後、ワークフローのインポート元と同じシステム上で新しいワークフローを実行したときに発生します。

### <a name="error-message"></a>エラー メッセージ
 配置手順 ' Activate Features ' でエラーが発生しました: 機能 [*guid*] で定義されている Id [*guid*] のフィールドが、現在のサイトコレクションまたはサブサイトで見つかりました。

### <a name="resolution"></a>解決方法
 このエラーは、の再利用可能なワークフローのインポートプロジェクトで [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] タスクフォームのフィールド id が変更されないために、フィールド ID の競合が発生した結果です。 インポートしたワークフローを、元のワークフローと同じサーバー上に配置すると、フィールド ID の競合が発生します。

 この問題を解決するには、検索置換機能を使用して、インポートしたすべてのワークフロー ファイル内のフィールド ID 属性の値を変更する必要があります。

## <a name="error-appears-when-a-renamed-imported-list-instance-is-run"></a>名前を変更したインポート済みリストインスタンスが実行されたときにエラーが表示される
 この問題は、インポートしたリスト インスタンスの名前を変更した後、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で実行した場合に発生します。

### <a name="error-message"></a>エラー メッセージ
 ビルドエラー: 配置手順 ' Activate Features ' でエラーが発生しました: ファイルテンプレート \ 機能 \\ [*import project*<em>feature</em>*name*] \Files\Lists \\ [*old*<em>list name</em>] \Schema.xml が存在しません。

### <a name="resolution"></a>解決方法
 リスト インスタンスをインポートすると、CustomSchema という名前の属性がリスト インスタンスの Elements.xml ファイルに追加されます。 Elements.xml には、リスト インスタンス用のカスタム schema.xml のパスが含まれます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でリスト インスタンスの名前を変更すると、カスタム schema.xml の配置パスは変更されますが、CustomSchema 属性のパス値は更新されません。 その結果、リストインスタンスは、機能がアクティブ化されたときに、CustomSchema 属性で指定された古いパスの *schema.xml* ファイルを見つけることができません。

 この問題を解決するには、CustomSchema 属性で *schema.xml* ファイルの配置場所のパスを更新します。

## <a name="sharepoint-debugging-session-terminated-by-iis"></a>IIS によって終了された SharePoint デバッグセッション
 この問題は、SharePoint ソリューションにブレークポイントを設定し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、 **F5** キーを押して実行し、90秒より長いブレークポイントで保持した場合に発生します。

### <a name="error-message"></a>エラー メッセージ
 デバッグ対象の Web サーバー プロセスは、インターネット インフォメーション サービス (IIS) によって停止されました。 IIS のアプリケーション プールの ping の設定を構成することによって、この問題を回避できます。 詳細については、ヘルプを参照してください。

### <a name="resolution"></a>解決方法
 既定では、IIS アプリケーション プールは、アプリケーションから応答が返るまで 90 秒間待機した後、アプリケーションを閉じます。 このプロセスは、アプリケーションの "ping" として知られています。 この問題を解決するには、待機時間を増やすか、アプリケーションの ping を完全に無効にします。

##### <a name="to-access-the-iis-app-pool-settings"></a>IIS アプリケーション プールの設定にアクセスするには

1. IIS マネージャーを開きます。

2. [ **接続** ] ウィンドウで、[SharePoint サーバー] ノードを展開し、[ **アプリケーションプール** ] ノードを選択します。

3. [ **アプリケーションプール** ] ページで、sharepoint アプリケーションプール (通常は "sharepoint-80") を選択し、[ **操作** ] ウィンドウで [ **詳細設定** ] リンクを選択します。

4. IIS がタイムアウトするまでの待機時間を長くするには、[ **Ping 最大応答時間 (秒)** ] の値を90秒より大きい値に変更します。

5. IIS ping を無効にするには、 **Ping Enabled** を **False**に設定します。

## <a name="auto-retract-leaves-orphaned-list-instance-in-sharepoint"></a>自動取り消しにより、孤立したリストインスタンスが SharePoint に残る
 この問題は、次の手順に従った場合に発生します。

1. リスト インスタンスがあるリスト定義を [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で作成します。

2. F5 キーを **押し** てソリューションを実行します。

3. デバッグを停止するか、SharePoint サイトを閉じます。

4. SharePoint サイトを再度開き、リスト インスタンスを開きます。

### <a name="error-message"></a>エラー メッセージ
 Server Error in '/' Application.

### <a name="resolution"></a>解決方法
 このエラーは、SharePoint ソリューションのデバッグ セッションを閉じた後、自動取り消し機能によってソリューションが取り消されたために発生します。 取り消しにより、リスト定義は SharePoint から削除されますが、リスト インスタンスは削除されません。 リスト インスタンスは、基になるリスト定義を必要とします。

 この問題を解決するには、メニューバーで [**ビルド**] [デプロイ] の順に選択し、ソリューションをデプロイ  >  **Deploy**します。 (F5 キーを **押し** てソリューションをデバッグしないでください)。次に、SharePoint でリストインスタンスを削除します。

## <a name="original-sharepoint-solution-is-replaced-by-an-exported-version"></a>元の SharePoint ソリューションがエクスポートされたバージョンに置き換えられる
 エクスポートした SharePoint ソリューションを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートした後、そのソリューションをエクスポート元のサイトに配置した場合、元の SharePoint ソリューションが置換されます。 この問題は、ソリューションの配置先を元のソリューションがアクティブ化されていないサーバーにすると、発生しません。

### <a name="error-message"></a>エラー メッセージ
 なし。

### <a name="resolution"></a>解決方法
 エクスポート元のサイトでソリューションが上書きされないようにするには、ソリューション ID の GUID と [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] プロジェクトにインポートしたすべての機能の機能 ID を変更します。

## <a name="error-appears-when-debugging-starts"></a>デバッグの開始時にエラーが表示される
 Visual Studio で SharePoint ソリューションのデバッグを開始すると、特定のキーがディクショナリに存在しないので Visual Studio で Web.config ファイルを読み込むことができないというエラーが発生します。

### <a name="error-message"></a>エラー メッセージ
 Web.config 構成ファイルを読み込むことができませんでした。 ファイルをチェックして、形式が正しくない XML 要素を修正した後、再試行してください。 次のエラーが発生しています: 特定のキーがディクショナリに存在しません。

### <a name="resolution"></a>解決方法
 この問題を解決するには、Visual Studio 内の SharePoint プロジェクトの [サイト URL] プロパティの値が、Web アプリケーションの代替アクセス マッピング用の既定のゾーンに割り当てられた URL と一致することを確認します。 URL でイントラネットなどの他のゾーンを使用すると、エラーは解消されません。 プロジェクトのサイト URL と既定のゾーンの URL は一致している必要があります。 代替アクセスマッピングにアクセスするには、SharePoint 2010 サーバーの全体管理ユーティリティを開き、[ **アプリケーション管理** ] リンクを選択します。次に、[ **Web アプリケーション**] で [ **代替アクセスマッピングの構成** ] リンクを選択します。 詳細については、「 [Web アプリケーションのゾーンを作成](/previous-versions/office/sharepoint-2007-products-and-technologies/cc263087(v=office.12))する」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [SharePoint のパッケージ化と配置のトラブルシューティング](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [Visual Studio でのデバッグ](../debugger/debugger-feature-tour.md)