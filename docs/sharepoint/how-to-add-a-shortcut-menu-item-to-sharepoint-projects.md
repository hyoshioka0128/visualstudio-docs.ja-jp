---
title: '方法: ショートカットメニュー項目を SharePoint プロジェクトに追加する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4e43d8d7717302eb8ab250935188bc2db3bdd66a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86014843"
---
# <a name="how-to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>方法: ショートカットメニュー項目を SharePoint プロジェクトに追加する
  ショートカットメニュー項目は、任意の SharePoint プロジェクトに追加できます。 メニュー項目は、ユーザーが **ソリューションエクスプローラー**内のプロジェクトノードを右クリックしたときに表示されます。

 次の手順では、プロジェクトの拡張機能が既に作成されていることを前提としています。 詳細については、「 [方法: SharePoint プロジェクトの拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-extension.md)する」を参照してください。

### <a name="to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>ショートカットメニュー項目を SharePoint プロジェクトに追加するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A>実装のメソッドで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> *projectservice*パラメーターのイベントを処理します。

2. イベントのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> 、 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.ActionMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.AddMenuItems%2A> イベント引数パラメーターのコレクションまたはコレクションに新しいオブジェクトを追加します。

3. <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click>新しいオブジェクトのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 、ユーザーがショートカットメニュー項目をクリックしたときに実行するタスクを実行します。

## <a name="example"></a>例
 次のコード例は、 **ソリューションエクスプローラー**の SharePoint プロジェクトノードにショートカットメニュー項目を追加する方法を示しています。 ユーザーがプロジェクトノードを右クリックし、[ **メッセージを出力ウィンドウに書き込む** ] メニュー項目をクリックすると、Visual Studio によって [ **出力** ] ウィンドウにメッセージが表示されます。 この例では、SharePoint プロジェクトサービスを使用してメッセージを表示します。 詳細については、「 [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

 [!code-csharp[SPExtensibility.ProjectExtension.Menu#1](../sharepoint/codesnippet/CSharp/projectmenu/extension/projectitemextensionmenu.cs#1)]
 [!code-vb[SPExtensibility.ProjectExtension.Menu#1](../sharepoint/codesnippet/VisualBasic/projectmenu/extension/projectitemextensionmenu.vb#1)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照を含むクラスライブラリプロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトの拡張](../sharepoint/extending-sharepoint-projects.md)
- [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
