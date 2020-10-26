---
title: SharePoint プロジェクト項目の拡張 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f60c95418379399196c461e055645ae7c85a473e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62967397"
---
# <a name="extend-sharepoint-project-items"></a>SharePoint プロジェクト項目の拡張
  Visual Studio に既にインストールされている SharePoint プロジェクト項目の種類に機能を追加する場合は、プロジェクト項目の拡張機能を作成します。 たとえば、Visual Studio で組み込み **イベントレシーバー** または **リスト定義** プロジェクト項目の拡張機能を作成したり、カスタムプロジェクト項目の種類の拡張機能を作成したりすることができます。 また、すべての種類の SharePoint プロジェクト項目の拡張機能を作成することもできます。

## <a name="tasks-for-extending-sharepoint-project-items"></a>SharePoint プロジェクト項目を拡張するためのタスク
 プロジェクト項目を拡張するには、インターフェイスを実装する Visual Studio 拡張機能アセンブリをビルドし <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> ます。 詳細については、「 [方法: SharePoint プロジェクト項目の拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)する」を参照してください。

 プロジェクト項目を拡張すると、次の機能をプロジェクト項目に追加することもできます。

- ショートカットメニュー項目をプロジェクト項目に追加します。 メニュー項目は、 **ソリューションエクスプローラー**でプロジェクト項目のショートカットメニューを開くと表示されます。 ショートカットメニューを開くには、プロジェクト項目を右クリックするか、プロジェクト項目を選択してから**Shift** + **F10**キーを押します。 詳細については、「 [方法: ショートカットメニュー項目を SharePoint プロジェクト項目の拡張機能に追加](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)する」を参照してください。

- カスタムプロパティをプロジェクト項目に追加します。 **ソリューションエクスプローラー**でプロジェクト項目を選択すると、プロパティが [**プロパティ**] ウィンドウに表示されます。 詳細については、「 [方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)する」を参照してください。

  プロジェクト項目の拡張機能を作成、配置、およびテストする方法を示すチュートリアルについては、「 [チュートリアル: SharePoint プロジェクト項目の種類の拡張](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)」を参照してください。

## <a name="understand-the-relationship-between-project-item-extensions-and-project-item-instances"></a>プロジェクト項目の拡張機能とプロジェクト項目インスタンスの関係を理解する
 プロジェクト項目の拡張機能を作成すると、関連付けられている型のプロジェクト項目が SharePoint プロジェクトに追加されたときに、Visual Studio によって拡張機能が読み込まれます。 たとえば、 **イベントレシーバー** プロジェクト項目の拡張機能を作成すると、ユーザーが **イベントレシーバー** プロジェクト項目をプロジェクトに追加したときに、Visual Studio によって拡張機能が読み込まれます。 Visual Studio では、関連付けられているプロジェクト項目の種類のすべてのインスタンスに対して、拡張機能の同じインスタンスが使用されます。 前の例では、ユーザーが2つ目の **イベントレシーバー** プロジェクト項目をプロジェクトに追加した場合、2つ目のプロジェクト項目をカスタマイズするために、拡張機能の同じインスタンスが使用されます。

 拡張するプロジェクト項目の種類の特定のインスタンスにアクセスするには、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> メソッドの実装で *projectItemType* パラメーターのイベントの1つを処理し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> ます。 たとえば、拡張する型のプロジェクト項目がプロジェクトに追加されるタイミングを確認するには、イベントを処理し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> ます。 詳細については、「 [方法: SharePoint プロジェクト項目の拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)する」を参照してください。

## <a name="identifiers-for-sharepoint-project-items"></a>SharePoint プロジェクトアイテムの識別子
 各 SharePoint プロジェクトアイテムには、対応する文字列識別子があります。 次のタスクを実行する場合は、プロジェクト項目の識別子を把握しておく必要があります。

- プロジェクト項目の拡張機能を作成します。 この場合、拡張するプロジェクト項目の識別子をのコンストラクターに渡す必要があり <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> ます。 すべてのプロジェクト項目の種類の拡張機能を作成するには、 **\\** * 文字列値を渡します。

- プロジェクト項目をプログラムによってプロジェクトに追加します。 この場合は、プロジェクト項目の識別子をメソッドに渡す必要があり <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemCollection.Add%2A> ます。

  次の表に、Visual Studio に含まれている SharePoint プロジェクト項目の識別子を示します。

|プロジェクト項目名|文字列識別子|
|-----------------------|-----------------------|
|ビジネス Data Catalog モデル|VisualStudio. BusinessDataConnectivity|
|コンテンツの種類|VisualStudio. ContentType|
|イベント レシーバー|VisualStudio. SharePoint. EventHandler|
|空の要素|VisualStudio 要素です。|
|リスト定義<br /><br /> コンテンツの種類からのリスト定義|VisualStudio (ListDefinition)|
|リストインスタンス|VisualStudio. ListInstance|
|モジュール|VisualStudio のモジュール|
|シーケンシャル ワークフロー<br /><br /> ステート マシン ワークフロー|VisualStudio (ワークフロー)|
|サイト定義|VisualStudio を定義します。|
|可視 Web パーツ|VisualStudio (Microsoft. SharePoint)|
|Web パーツ|VisualStudio (SharePoint)|
|ワークフローの関連付けフォーム|VisualStudio (WorkflowAssociation)|

## <a name="see-also"></a>こちらもご覧ください
- [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [方法: ショートカットメニュー項目を SharePoint プロジェクト項目の拡張機能に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [チュートリアル: SharePoint プロジェクト項目の種類の拡張](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
- [SharePoint プロジェクトシステムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)
