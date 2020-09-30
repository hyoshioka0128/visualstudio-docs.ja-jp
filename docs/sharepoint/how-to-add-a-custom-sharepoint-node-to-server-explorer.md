---
title: '方法: サーバーエクスプローラーにカスタム SharePoint ノードを追加する |Microsoft Docs'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5a74c9c879df57a5ff6444626870ee9f021fb4e9
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584886"
---
# <a name="how-to-add-a-custom-sharepoint-node-to-server-explorer"></a>方法: サーバーエクスプローラーにカスタム SharePoint ノードを追加する
  カスタムノードは、**サーバーエクスプローラー**の [ **SharePoint 接続**] ノードの下に追加できます。 これは、既定では **サーバーエクスプローラー** に表示されない追加の SharePoint コンポーネントを表示する場合に便利です。 詳細については、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

 カスタムノードを追加するには、まず、新しいノードを定義するクラスを作成します。 次に、既存のノードの子としてノードを追加する拡張機能を作成します。

### <a name="to-define-the-new-node"></a>新しいノードを定義するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - VisualStudio (拡張子が付いています)

    - System.ComponentModel.Composition

    - System.Drawing

3. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> インターフェイスを実装するクラスを作成します。

4. クラスに次の属性を追加します。

    - <xref:System.ComponentModel.Composition.ExportAttribute>. この属性を使用すると、Visual Studio で実装を検出して読み込むことができ <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> ます。 型を <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 属性コンストラクターに渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute>. ノード定義では、この属性は新しいノードの文字列識別子を指定します。 *会社名*の形式を使用することをお勧めします。*ノード名*を使用して、すべてのノードが一意の識別子を持つようにします。

5. メソッドの実装では <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider.InitializeType%2A> 、 *typedefinition* パラメーターのメンバーを使用して、新しいノードの動作を構成します。 このパラメーターは、 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition> インターフェイスで定義されたイベントへのアクセスを提供するオブジェクトです <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> 。

     次のコード例は、新しいノードを定義する方法を示しています。 この例では、プロジェクトに CustomChildNodeIcon というアイコンが埋め込みリソースとして含まれていることを前提としています。

     [!code-vb[SPExtensibility.ProjectSystemExtension.General#6](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#6)]
     [!code-csharp[SPExtensibility.ProjectSystemExtension.General#6](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#6)]

### <a name="to-add-the-new-node-as-a-child-of-an-existing-node"></a>新しいノードを既存のノードの子として追加するには

1. ノード定義と同じプロジェクトで、インターフェイスを実装するクラスを作成し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> ます。

2. クラスに <xref:System.ComponentModel.Composition.ExportAttribute> 属性を追加します。 この属性を使用すると、Visual Studio で実装を検出して読み込むことができ <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> ます。 型を <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 属性コンストラクターに渡します。

3. クラスに <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 属性を追加します。 ノード拡張では、この属性によって、拡張するノードの種類の文字列識別子が指定されます。

     Visual Studio によって提供される組み込みのノード型を指定するには、次の列挙値のいずれかを属性コンストラクターに渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>: これらの値を使用して、 **サーバーエクスプローラー**内のサイト接続ノード (サイトの url を表示するノード)、サイトノード、またはその他のすべての親ノードを指定します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>: リスト、フィールド、コンテンツタイプを表すノードなど、SharePoint サイト上の個々のコンポーネントを表す組み込みノードの1つを指定するには、次の値を使用します。

4. メソッドの実装で <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> 、 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> パラメーターのイベントを処理し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> ます。

5. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested>イベントハンドラーで、 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeEventArgs.Node%2A> イベント引数パラメーターによって公開されるオブジェクトの子ノードコレクションに新しいノードを追加します。

     次のコード例は、 **サーバーエクスプローラー**で SharePoint サイトノードの子として新しいノードを追加する方法を示しています。

     [!code-vb[SPExtensibility.ProjectSystemExtension.General#7](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#7)]
     [!code-csharp[SPExtensibility.ProjectSystemExtension.General#7](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#7)]

## <a name="complete-example"></a>コード例全体
 次のコード例では、単純なノードを定義し、それを **サーバーエクスプローラー**の SharePoint サイトノードの子として追加するための完全なコードを示します。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#5](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#5)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#5](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#5)]

## <a name="compiling-the-code"></a>コードのコンパイル
 この例では、プロジェクトに CustomChildNodeIcon というアイコンが埋め込みリソースとして含まれていることを前提としています。 この例では、次のアセンブリへの参照も必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

- System.Drawing

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 **サーバーエクスプローラー**拡張機能を配置するには、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [方法: サーバーエクスプローラーで SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
