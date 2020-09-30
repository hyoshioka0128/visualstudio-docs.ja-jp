---
title: ショートカットメニュー項目を SharePoint プロジェクト項目の拡張機能に追加する
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: d3c0627849df12b98ddc16f54317faf952cb41f6
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585863"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension"></a>方法: ショートカットメニュー項目を SharePoint プロジェクト項目の拡張機能に追加する
  プロジェクト項目の拡張機能を使用して、既存の SharePoint プロジェクト項目にショートカットメニュー項目を追加できます。 メニュー項目は、ユーザーが **ソリューションエクスプローラー**でプロジェクト項目を右クリックしたときに表示されます。

 次の手順では、プロジェクト項目の拡張機能が既に作成されていることを前提としています。 詳細については、「 [方法: SharePoint プロジェクト項目の拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)する」を参照してください。

### <a name="to-add-a-shortcut-menu-item-in-a-project-item-extension"></a>プロジェクト項目の拡張機能にショートカットメニュー項目を追加するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A>実装のメソッドで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> *projectItemType*パラメーターのイベントを処理します。

2. イベントのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> 、 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> イベント引数パラメーターのコレクションまたはコレクションに新しいオブジェクトを追加します。

3. <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click>新しいオブジェクトのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 、ユーザーがショートカットメニュー項目をクリックしたときに実行するタスクを実行します。

## <a name="example"></a>例
 次のコード例は、ショートカットメニュー項目をイベントレシーバープロジェクト項目に追加する方法を示しています。 ユーザーが **ソリューションエクスプローラー** でプロジェクト項目を右クリックし、[ **出力ウィンドウにメッセージを書き込む** ] メニュー項目をクリックすると、Visual Studio によって [ **出力** ] ウィンドウにメッセージが表示されます。

 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#1](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionmenu.vb#1)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#1](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionmenu.cs#1)]

 この例では、SharePoint プロジェクトサービスを使用して、 **出力** ウィンドウにメッセージを書き込みます。 詳細については、「 [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照を含むクラスライブラリプロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)
- [チュートリアル: SharePoint プロジェクト項目の種類の拡張](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
