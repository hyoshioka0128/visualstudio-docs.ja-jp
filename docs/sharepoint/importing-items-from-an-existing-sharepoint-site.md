---
title: 既存の SharePoint サイトからのアイテムのインポート |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VS.SharePointTools.WSPImport.SelectionDependency
- VS.SharepointTools.WSPImport.SpecifyProjectSource
- VS.SharePointTools.WSPImport.SelectionItemsToImport
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- SharePoint development in Visual Studio, importing .wsp files
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9c2703bfdd4f47281a1fc19060cb69f8b312e7d2
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017030"
---
# <a name="import-items-from-an-existing-sharepoint-site"></a>既存の SharePoint サイトからのアイテムのインポート
  SharePoint ソリューション パッケージのインポート プロジェクト テンプレートによって、新しい [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint ソリューションの既存の SharePoint サイトからコンテンツ タイプやフィールドなどの要素を再利用できます。 インポートしたソリューションのほとんどは変更せずに実行できますが、それらをインポートした後にいずれかの項目を変更する場合は特に、考慮すべき特定の制限事項および問題があります。

> [!NOTE]
> 再利用可能なワークフローをインポートするには、再利用可能なワークフローのインポート プロジェクト テンプレートを使用します。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][再利用可能なワークフローをインポートするためのガイドライン](../sharepoint/guidelines-for-importing-reusable-workflows.md)。

## <a name="supported-sharepoint-solutions"></a>サポートされる SharePoint ソリューション
 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] は、 [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] および [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]で作成したソリューションのインポートを完全にサポートします。

 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] では、以下のアプリケーションで作成したソリューションのインポートはサポートされません。

- [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)]

- [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)]

- [!INCLUDE[vs_orcas_long](../sharepoint/includes/vs-orcas-long-md.md)]

- Microsoft SharePoint Designer 2007

- [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)]

  これらのアプリケーションによって作成されたソリューションを正常にインポートできる場合もありますが、その機能はテストされておらず、サポートされていません。

## <a name="item-import-restrictions"></a>項目のインポートの制限
 ほとんどの SharePoint アイテムは既存の *.wsp*ファイルからインポートできますが、次のアイテムはサポートされていないため、正しく機能するための変更が必要になる場合があります。

- BDC エンティティ

- コード ワークフロー関連の要素

- コード ワークフロー

- 視覚的 Web パーツ (.ascx)

- Web サービス (*.asmx*)

- コンテンツ タイプのバインディング

- イベント レシーバー

- リスト定義 (テンプレート)

- サイト定義

  またはからソリューションをエクスポートすると [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] 、これらのアイテムは *.wsp*ファイルから自動的に除外されます。 ただし、サポートされていないツールから生成された *.wsp*ファイルには、これらの項目が含まれている場合があります。 (このトピック前半の「サポートされる SharePoint ソリューション」をご覧ください。)

## <a name="what-happens-when-you-import-a-solution"></a>ソリューションをインポートするとどうなりますか
 SharePoint ソリューションパッケージのインポートテンプレートを使用してソリューションをインポートすると、によって、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] *.wsp*ファイルのすべての内容がコピーされ、インポートされた要素とそのファイルの間の関連付けと参照が可能な限り、調整および保持されます。

 インポートされるすべてのアイテムは、 **ソリューション エクスプローラー**の対応するフォルダーにコピーされます。 たとえば、 **[コンテンツ タイプ]** フォルダーの下にコンテンツ タイプが表示され、 **[リスト インスタンス]** の下にリスト インスタンスが一覧表示されます。 インポートされたアイテムに関連付けられているファイルは、そのアイテムのフォルダーにコピーされます。 たとえば、インポートしたリスト インスタンスには、そのモジュール、フォーム、ASPX ページが含まれます。

### <a name="dependent-items"></a>依存アイテム
 [SharePoint ソリューション パッケージのインポート] ウィザードでアイテムを選んだものの、その依存アイテムを選んでいない場合は、インポートする前に依存アイテムも選ぶ必要があることがメッセージ ボックスで通知されます。

### <a name="what-are-features"></a>機能とは
 SharePoint Designer のユーザーは、 *ソリューション エクスプローラー*のインポートされたソリューションに、 **フィーチャー** と呼ばれる予期せぬファイルが表示されているのに気付くことがあります。フィーチャーは SharePoint Designer ソリューションに存在していましたが、表示されていませんでした。 現在では [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]にフィーチャーが表示されるようになりました。

 フィーチャーは、SharePoint アイテムのコンテナーになります。 各フィーチャーは、その中に含まれているコンテンツ タイプやリスト定義などの各アイテムへの参照を保持します。 ソリューションをインポートすると、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] はインポートされた要素のすべてのフィーチャーを設定して、ファイルのフィーチャーと要素との関係を維持しようと試みます。 参照を解決できないファイルがあれば、 **[その他のインポートされたファイル]** フォルダーに配置されます。

 機能の詳細については、「 [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)と[機能の](/previous-versions/office/developer/sharepoint-2010/ms460318(v=office.14))使用」を参照してください。

### <a name="handle-special-cases"></a>特殊なケースの処理
 Visual Studio はアイテムとその依存ファイルの調整ができない場合があります。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] が解決できないファイルは **[その他のインポートされたファイル]** フォルダーに表示されます。 また、その **DeploymentType** プロパティは **NoDeployment** に設定されるので、それらのファイルがソリューションと一緒に配置されることはありません。

 たとえば、リスト定義をインポートした場合、その名前を持つリスト定義が、**ソリューションエクスプローラー**の [**リスト定義**] フォルダーの下に*Elements.xml*ファイルと*Schema.xml*ファイルと共に表示されます。 しかし、関連付けられた ASPX と HTML フォームは、 **[その他のインポートされたファイル]** フォルダーの下にある **[ExpenseForms]** と呼ばれるフォルダーに配置される可能性があります。 インポートを完了するには、 **ソリューション エクスプローラー** で ExpenseForms リスト定義の下にあるそれらのファイルを移動し、各ファイルの **DeploymentType** プロパティを **NoDeployment** から **ElementFile**に変更します。

 イベントレシーバーをインポートする場合、 *Elements.xml*ファイルは正しい場所にコピーされますが、ソリューションと共に配置されるように、ソリューションパッケージにアセンブリを手動で含める必要があります。 [!INCLUDE[crabout](../sharepoint/includes/crabout-md.md)]その方法については、「[方法: 追加のアセンブリを追加および削除](../sharepoint/how-to-add-and-remove-additional-assemblies.md)する」を参照してください。

 ワークフローをインポートすると、InfoPath フォームが **[その他のインポートされたファイル]** フォルダーにコピーされます。 *.Wsp*ファイルに Web テンプレートが含まれている場合は、**ソリューションエクスプローラー**の [スタートアップ] ページとして設定されます。

## <a name="import-fields-and-property-bags"></a>フィールドとプロパティバッグのインポート
 複数のフィールドを持つソリューションをインポートすると、すべての個別のフィールド定義が、**ソリューションエクスプローラー** **フィールド**と呼ばれるノードの下の1つの*Elements.xml*ファイルにマージされます。 同様に、すべてのプロパティバッグエントリは、 **propertybags**と呼ばれるノードの下にある*Elements.xml*ファイルにマージされます。

 SharePoint 内のフィールドは、テキスト、ブール値、参照などの指定したデータ型の列です。 詳しくは、「 [構成要素: 列とフィールド型](/previous-versions/office/developer/sharepoint-2010/ee535893(v=office.14))」をご覧ください。 プロパティ バッグを使用することによって、SharePoint 内のオブジェクト (ファームから SharePoint サイト上のリストまですべて) にプロパティを追加できます。 プロパティ バッグは、プロパティの名前と値のハッシュ テーブルとして実装されます。 詳しくは、「 [SharePoint 構成の管理](/previous-versions/msp-n-p/ff647766(v=pandp.10)) 」または「 [SharePoint プロパティ バッグ設定](https://archive.codeplex.com/?p=pbs)」をご覧ください。

## <a name="delete-items-in-the-project"></a>プロジェクト内の項目を削除する
 SharePoint ソリューションのほとんどのアイテムには、1 つ以上の依存アイテムがあります。 たとえば、リスト インスタンスはコンテンツ タイプに依存します。また、コンテンツ タイプは、フィールドに依存します。 SharePoint ソリューションをインポートした後でソリューション内のアイテムを削除し、その依存アイテムを削除しない場合、ソリューションの配置を試みるまで [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] は参照の問題を通知しません。 たとえば、インポートされたソリューションに、コンテンツ タイプに依存するリスト インスタンスがある場合、そのコンテンツ タイプを削除すると、配置でエラーが発生する可能性があります。 依存アイテムが SharePoint サーバー上に存在しない場合に、エラーが発生します。 同様に、削除された項目に関連するプロパティバッグもある場合は、そのプロパティバッグエントリを**propertybags** *Elements.xml*ファイルから削除します。 そのため、インポートされたソリューションから何らかのアイテムを削除すると配置エラーが発生する場合は、削除が必要な配置アイテムがないか確認します。

## <a name="restore-missing-feature-attributes"></a>見つからないフィーチャー属性の復元
 ソリューションをインポートするときに、オプションのいくつかのフィーチャー属性は、インポートされたフィーチャー マニフェストから除外されます。 これらの属性を新しいフィーチャーファイルで復元する場合は、元のフィーチャーファイルと新しいフィーチャーマニフェストを比較して、不足している属性を特定し、「 [How to: Customize a SharePoint feature](../sharepoint/how-to-customize-a-sharepoint-feature.md)」トピックの手順に従います。

## <a name="deployment-conflict-detection-is-not-performed-on-built-in-list-instances"></a>組み込みのリストインスタンスで配置競合検出が実行されない
 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、組み込みのリスト インスタンス (つまり、SharePoint に付属している既定のリスト インスタンス) に関する配置競合の検出は実行されません。 SharePoint 上の組み込みのリスト インスタンスを上書きしないために、競合の検出は実行されません。 組み込みのリスト インスタンスは配置されたり、更新されたりしますが、削除されたり、上書きされたりすることはありません。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][SharePoint のパッケージ化と配置のトラブルシューティングを](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)行います。

## <a name="import-sharepoint-server-2010-workflows"></a>SharePoint Server 2010 ワークフローのインポート
 [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]で作成したワークフローをインポートする場合、そのワークフローを配置した後は正常に実行されません。 特定のアセンブリが不足するため、また  [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] のワークフローに [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のワークフロー ソリューションで現在サポートされていない InfoPath フォームが含まれるために、ワークフローは正しく実行されません。 ただし、インポートされた [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] のワークフローは、 [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] アセンブリへの参照を追加したり、InfoPath フォームを再接続したりすることによって一部のアイテムを修正した後、正常に機能させることができます。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][SharePoint Server 2010 ワークフローをインポート](/sharepoint/dev/)しています。

## <a name="item-name-character-limit"></a>項目名の文字制限
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、プロジェクトおよびプロジェクト アイテムの名前 (パスを含む) に合計 260 文字の制限があります。 ソリューションをインポートするときに、アイテム名がこの制限を超えると、次のエラーが発生します。

 **指定されたパス、ファイル名、またはその両方が長すぎます。完全修飾ファイル名は260文字未満、ディレクトリ名は248文字未満にする必要があります。**

 このエラーが発生すると、アイテムは作成されません。 この問題は、インポートしたモジュールで最も頻繁に発生します。 この問題を回避するには、次の操作を行います。

- **[新しいプロジェクトの追加]** ダイアログ ボックスにプロジェクト名を入力するときは、短い名前を使用します。

- パスを短くために、可能な限りルート フォルダーに近い場所にプロジェクトを作成します。

## <a name="the-sharepointproductversion-attribute"></a>SharePointProductVersion 属性
 [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] または [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)]など SharePoint の以前のバージョンで作成されたソリューションをインポートする場合、パッケージ マニフェストの SharePointProductVersion 属性の値を 12.0 に変更するか、インポートされたすべての Web ページに Script Manager コントロールを挿入して SharePointProductVersion の設定を 14.0 のままにします。 それ以外の場合、インポートされた Web フォームは、SharePoint では表示されません。

### <a name="background"></a>バックグラウンド
 [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] と [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] のソリューションには SharePointProductVersion という属性が含まれています。 SharePoint はパッケージ マニフェストのこの属性を使用して、そのソリューションが設計されている SharePoint のバージョンを判別します。 正しい値は 12.0 と 14.0 の 2 つです。 値 12.0 は、アイテムが [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] または [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)]向けに設計されていることを示します。値 14.0 は、アイテムが [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] または [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]向けに設計されていることを示します。

 ASPX ページのレンダリング時のセキュリティを強化するため、 [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] と [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] では、すべての ASPX ページまたはマスター ページに Script Manager コントロールを含める必要があります。 Script Manager について詳しくは、「 [ScriptManager コントロールの概要](/previous-versions/bb398863(v=vs.140))」をご覧ください。 [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] と [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)]には Script Manager コントロールがないため、 [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] または [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] にアップグレードされる [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] または [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]のページには Script Manager コントロールを追加する必要があります。 標準のマスター ページを使用する ASPX ページでは、標準のマスター ページに既に Script Manager コントロールが 1 つ追加されているため、Script Manager コントロールは必要ありません。 ただし、マスター ページを使用しない、またはカスタム マスター ページを使用する ASPX ページでは、 [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] または [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]で作業するために Script Manager コントロールを追加する必要があります。

 新しいすべてのプロジェクトの SharePointProductVersion 属性は 14.0 に設定されるため、Script Manager コントロールがないと、 [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] または [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] のプロジェクトを [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)]にインポートするときに問題が発生する可能性があります。 Web フォームが存在するアップグレードされたプロジェクトを Script Manager なしで配置する場合、フォームは SharePoint に表示されません。

## <a name="see-also"></a>関連項目
- [チュートリアル: 既存の SharePoint サイトからの項目のインポート](../sharepoint/walkthrough-import-items-from-an-existing-sharepoint-site.md)
- [再利用可能なワークフローをインポートするためのガイドライン](../sharepoint/guidelines-for-importing-reusable-workflows.md)
- [チュートリアル: SharePoint Designer の再利用可能なワークフローを Visual Studio にインポートする](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)
- [方法: 既存の BDC モデルファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
