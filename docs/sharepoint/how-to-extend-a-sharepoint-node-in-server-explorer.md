---
title: '方法: サーバーエクスプローラーで SharePoint ノードを拡張するMicrosoft Docs'
description: '[SharePoint 接続ノードを使用してサーバーエクスプローラーで SharePoint ノードを拡張する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bad90701d19f97036ecba55bb2901739ad30b200
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903547"
---
# <a name="how-to-extend-a-sharepoint-node-in-server-explorer"></a>方法: サーバーエクスプローラーで SharePoint ノードを拡張する
  **サーバーエクスプローラー** の [ **SharePoint 接続**] ノードの下でノードを拡張できます。 これは、新しい子ノード、ショートカットメニュー項目、またはプロパティを既存のノードに追加する場合に便利です。 詳細については、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

### <a name="to-extend-a-sharepoint-node-in-server-explorer"></a>サーバーエクスプローラーで SharePoint ノードを拡張するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - VisualStudio (拡張子が付いています)

    - System.ComponentModel.Composition

3. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> インターフェイスを実装するクラスを作成します。

4. クラスに <xref:System.ComponentModel.Composition.ExportAttribute> 属性を追加します。 この属性を使用すると、Visual Studio で実装を検出して読み込むことができ <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> ます。 型を <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 属性コンストラクターに渡します。

5. クラスに <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 属性を追加します。 この属性は、拡張するノードの種類の文字列識別子を指定します。

     Visual Studio によって提供される組み込みのノード型を指定するには、次の列挙値のいずれかを属性コンストラクターに渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>: これらの値を使用して、 **サーバーエクスプローラー** 内のサイト接続ノード (サイトの url を表示するノード)、サイトノード、またはその他のすべての親ノードを指定します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>: リスト、フィールド、コンテンツタイプを表すノードなど、SharePoint サイト上の個々のコンポーネントを表す組み込みノードの1つを指定するには、次の値を使用します。

6. メソッドの実装では、 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> *nodeType* パラメーターのメンバーを使用して、ノードに機能を追加します。 このパラメーターは、 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> インターフェイスで定義されたイベントへのアクセスを提供するオブジェクトです <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> 。 たとえば、次のイベントを処理できます。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested>: ノードに新しい子ノードを追加するには、このイベントを処理します。 詳細については、「 [方法: サーバーエクスプローラーにカスタム SharePoint ノードを追加](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)する」を参照してください。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeMenuItemsRequested>: このイベントを処理して、カスタムショートカットメニュー項目をノードに追加します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodePropertiesRequested>: ノードにカスタムプロパティを追加するには、このイベントを処理します。 ノードが選択されると、プロパティが [ **プロパティ** ] ウィンドウに表示されます。

## <a name="example"></a>例
 次のコード例は、2つの異なる種類のノード拡張を作成する方法を示しています。

- SharePoint サイトノードにコンテキストメニュー項目を追加する拡張機能。 メニュー項目をクリックすると、クリックされたノードの名前が表示されます。

- **ContosoExampleProperty** という名前のカスタムプロパティを、 **Body** という名前のフィールドを表す各ノードに追加する拡張機能。

  [!code-csharp[SPExtensibility.ProjectSystemExtension.General#9](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextension.cs#9)]
  [!code-vb[SPExtensibility.ProjectSystemExtension.General#9](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextension.vb#9)]

  この拡張機能により、編集可能な文字列プロパティがノードに追加されます。 SharePoint サーバーから読み取り専用のデータを表示するカスタムプロパティを作成することもできます。 これを行う方法を示す例については、「 [チュートリアル: web パーツを表示するためのサーバーエクスプローラーの拡張](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- VisualStudio (拡張子が付いています)

- System.ComponentModel.Composition

- System.Windows.Forms

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 **サーバーエクスプローラー** 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: サーバーエクスプローラーにカスタム SharePoint ノードを追加する](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [カスタムデータと SharePoint ツールの拡張機能の関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
