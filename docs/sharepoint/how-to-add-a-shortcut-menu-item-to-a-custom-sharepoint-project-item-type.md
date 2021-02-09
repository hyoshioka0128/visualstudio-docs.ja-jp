---
title: ショートカットメニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する
titleSuffix: ''
description: ショートカットメニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する方法について説明します。 メニュー項目は、ソリューションエクスプローラーでプロジェクト項目を右クリックすると表示されます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0679233a727e716debe5d925a22cd256d250a28f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923702"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type"></a>方法: ショートカットメニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する
  カスタム SharePoint プロジェクト項目の種類を定義すると、ショートカットメニュー項目をプロジェクト項目に追加できます。 メニュー項目は、ユーザーが **ソリューションエクスプローラー** でプロジェクト項目を右クリックしたときに表示されます。

 次の手順では、独自の SharePoint プロジェクトアイテムの種類が既に定義されていることを前提としています。 詳細については、「 [方法: SharePoint プロジェクト項目の種類を定義](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)する」を参照してください。

### <a name="to-add-a-shortcut-menu-item-to-a-custom-project-item-type"></a>ショートカットメニュー項目をカスタムプロジェクト項目の種類に追加するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A>実装のメソッドで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> *projectItemTypeDefinition* パラメーターのイベントを処理します。

2. イベントのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> 、 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> イベント引数パラメーターのコレクションまたはコレクションに新しいオブジェクトを追加します。

3. <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click>新しいオブジェクトのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 、ユーザーがショートカットメニュー項目を選択したときに実行するタスクを実行します。

## <a name="example"></a>例
 次のコード例は、カスタムプロジェクト項目の種類にコンテキストメニュー項目を追加する方法を示しています。 ユーザーが **ソリューションエクスプローラー** のプロジェクト項目からショートカットメニューを開き、[ **出力ウィンドウにメッセージを書き込む** ] メニュー項目を選択すると、Visual Studio によって **出力** ウィンドウにメッセージが表示されます。

 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#4](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypemenu.cs#4)]
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#4](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypemenu.vb#4)]

 この例では、SharePoint プロジェクトサービスを使用して、 **出力** ウィンドウにメッセージを書き込みます。 詳細については、「 [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照を含むクラスライブラリプロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>プロジェクト項目を配置する
 他の開発者がプロジェクト項目を使用できるようにするには、プロジェクトテンプレートまたはプロジェクト項目テンプレートを作成します。 詳細については、「 [SharePoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)」を参照してください。

 プロジェクト項目を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリ、テンプレート、およびプロジェクト項目と共に配布するその他のファイルの拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [方法: プロパティをカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [カスタム SharePoint プロジェクト項目の種類の定義](../sharepoint/defining-custom-sharepoint-project-item-types.md)
