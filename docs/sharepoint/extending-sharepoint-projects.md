---
title: SharePoint プロジェクトの拡張 |Microsoft Docs
description: SharePoint プロジェクトのプロジェクトレベルの機能をカスタマイズする場合に、プロジェクトの拡張機能を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: ae4c3c1e606fd436725ef9f54a4568b754b048af
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672640"
---
# <a name="extend-sharepoint-projects"></a>SharePoint プロジェクトの拡張
  SharePoint プロジェクトのプロジェクトレベルの機能をカスタマイズする場合は、プロジェクトの拡張機能を作成します。 たとえば、カスタムプロジェクトのプロパティを追加したり、ユーザーが Visual Studio で SharePoint ソリューションを開発したときに発生するプロジェクトレベルのイベントに応答したりできます。

## <a name="create-project-extensions"></a>プロジェクト拡張機能の作成
 プロジェクト項目を拡張するには、インターフェイスを実装する Visual Studio 拡張機能アセンブリをビルドし <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> ます。 詳細については、「 [方法: SharePoint プロジェクトの拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-extension.md)する」を参照してください。

 プロジェクト拡張機能を作成するときに、次の機能を SharePoint プロジェクトに追加することもできます。

- ショートカットメニュー項目を追加します。 メニュー項目は、**ソリューションエクスプローラー** で SharePoint プロジェクトノードのショートカットメニューを開いたときに表示されます。そのためには、ノードを右クリックするか選択し、 **Shift** + **F10** キーを押します。 詳細については、「 [方法: ショートカットメニュー項目を SharePoint プロジェクトに追加](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)する」を参照してください。

- カスタムプロパティを追加します。 **ソリューションエクスプローラー** で SharePoint プロジェクトを選択すると、プロパティが [**プロパティ**] ウィンドウに表示されます。 詳細については、「 [方法: SharePoint プロジェクトにプロパティを追加](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)する」を参照してください。

  プロジェクトの拡張機能を作成、配置、およびテストする方法を示すチュートリアルについては、「 [チュートリアル: SharePoint プロジェクトの拡張機能を作成](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)する」を参照してください。

## <a name="understand-the-relationship-between-project-extensions-and-project-instances"></a>プロジェクトの拡張機能とプロジェクトインスタンスの関係を理解する
 プロジェクト拡張機能を作成すると、で任意の種類の SharePoint プロジェクトが開かれたときに、拡張機能が読み込まれ [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、リスト定義、コンテンツの種類、イベントレシーバーなど、いくつかの SharePoint プロジェクトテンプレートが含まれています。 ただし、SharePoint プロジェクトの種類は1つだけです。 [ **新しいプロジェクト** ] ダイアログボックスに表示されるプロジェクトの種類は、1つ以上の SharePoint プロジェクトアイテムをバンドルするテンプレートにすぎません。 SharePoint プロジェクトの種類は1つだけなので、1つのプロジェクトに対して作成された拡張機能は、すべての SharePoint プロジェクトに適用されます。 たとえば、 **コンテンツタイプ** のプロジェクトにのみ適用される拡張機能を作成することはできません。

 特定のプロジェクトインスタンスにアクセスするには、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> メソッドの実装で、 *projectservice* パラメーターのイベントの1つを処理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> します。 たとえば、SharePoint プロジェクトがソリューションに追加されたことを確認するには、イベントを処理し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> ます。 詳細については、「 [方法: SharePoint プロジェクトの拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-extension.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [方法: ショートカットメニュー項目を SharePoint プロジェクトに追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [チュートリアル: SharePoint プロジェクト拡張機能の作成](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)
- [カスタム SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
