---
title: カスタム SharePoint プロジェクト項目の種類の定義 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e5f32abba4c4cbdeab59ed66e38019d913e704e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62580785"
---
# <a name="define-custom-sharepoint-project-item-types"></a>カスタム SharePoint プロジェクト項目の種類を定義する
  新しい種類の SharePoint プロジェクト項目を作成する場合は、新しい SharePoint プロジェクト項目の種類を定義します。 たとえば、Visual Studio には、フィールドやカスタムアクションを SharePoint サイトに追加するための SharePoint プロジェクトアイテムは含まれていません。 フィールド、カスタムアクション、またはその他の種類の SharePoint コンポーネントを作成するために、独自の種類の SharePoint プロジェクト項目を定義できます。

## <a name="tasks-for-defining-sharepoint-project-item-types"></a>SharePoint プロジェクト項目の種類を定義するためのタスク
 カスタムプロジェクト項目の種類を定義するには、インターフェイスを実装する Visual Studio 拡張機能アセンブリをビルドし <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> ます。 詳細については、「 [方法: SharePoint プロジェクト項目の種類を定義](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)する」を参照してください。

 カスタムプロジェクト項目の種類を定義する場合は、次の機能をプロジェクト項目に追加することもできます。

- ショートカットメニュー項目をプロジェクト項目に追加します。 メニュー項目は、**ソリューションエクスプローラー**のプロジェクト項目のショートカットメニューを開くと表示されます。プロジェクト項目を右クリックするか、プロジェクト項目を選択してから**Shift** + **F10**キーを押します。 詳細については、「 [方法: ショートカットメニュー項目をカスタム SharePoint プロジェクト項目の種類に追加](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)する」を参照してください。

- カスタムプロパティをプロジェクト項目に追加します。 **ソリューションエクスプローラー**でプロジェクト項目を選択すると、プロパティが [**プロパティ**] ウィンドウに表示されます。 詳細については、「 [方法: カスタム SharePoint プロジェクト項目の種類にプロパティを追加](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)する」を参照してください。

  他の開発者が Visual Studio でプロジェクト項目を使用できるようにするには、sharepointprojectitem.spdata ファイルを作成し、プロジェクト項目に関連付けられている項目テンプレートまたはプロジェクトテンプレートを作成します。 詳細については、「 [SharePoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)」を参照してください。

## <a name="understand-the-relationship-between-project-item-types-and-project-item-instances"></a>プロジェクト項目の種類とプロジェクト項目インスタンスの関係を理解する
 SharePoint プロジェクト項目の種類を定義すると、関連付けられている型のプロジェクト項目が SharePoint プロジェクトに追加されたときに、Visual Studio によって拡張機能が読み込まれます。 たとえば、新しい **カスタムアクション** プロジェクト項目の種類を定義すると、ユーザーが **カスタム動作** プロジェクト項目をプロジェクトに追加したときに、Visual Studio によって拡張機能が読み込まれます。 Visual Studio では、関連付けられているプロジェクト項目の種類のすべてのインスタンスに対して、拡張機能の同じインスタンスが使用されます。 前の例では、ユーザーが2つ目の **カスタムアクション** プロジェクト項目をプロジェクトに追加した場合、2つ目のプロジェクト項目をカスタマイズするために、拡張機能の同じインスタンスが使用されます。

 プロジェクト項目の種類の特定のインスタンスにアクセスするには、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> メソッドの実装で *projectItemTypeDefinition* パラメーターのイベントの1つを処理し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> ます。 たとえば、カスタム型のプロジェクト項目がプロジェクトに追加されたことを確認するには、イベントを処理し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> ます。 詳細については、「 [方法: SharePoint プロジェクト項目の種類を定義](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)する」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [方法: プロパティをカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [方法: ショートカットメニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [チュートリアル: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (第2部)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
