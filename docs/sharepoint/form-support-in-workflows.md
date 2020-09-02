---
title: ワークフローでのフォームのサポート |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b064df6729b914af7758cde86b03b886fd0e5d26
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72986259"
---
# <a name="form-support-in-workflows"></a>ワークフローでのフォームのサポート
  ワークフローでは、アソシエーション、開始、タスク、および変更の4種類のフォームを使用できます。 これらのフォーム型は、ASPX フォームまたは InfoPath フォームに基づいて作成できます。 特定のフォームに対して提供されるサポートのレベルは、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 次の表で説明されているいくつかの要因によって異なります。 ワークフローフォームの種類の詳細については、「 [ワークフローフォームの概要](/previous-versions/office/developer/sharepoint-2010/ms457061(v=office.14))」を参照してください。

## <a name="xml-refactoring"></a>XML リファクタリング
 ASPX 関連付けまたは開始フォームをワークフロープロジェクト項目に追加すると [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、によって、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ワークフローの *Elements.xml* ファイル内の XML が自動的にリファクタされ、フォーム名または配置パスが更新されたとき、またはフォームが削除されるたびに、アソシエーションまたは開始フォームを参照する属性が同期されます。 ただし、タスクや変更フォームなどの他のフォームの種類をワークフローで使用する場合、 *Elements.xml* ファイルはリファクタリングされません。

## <a name="form-support-in-new-visual-studio-workflows"></a>新しい Visual Studio ワークフローでのフォームのサポート
 次の表に、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で作成されるワークフローにおける、ASPX または InfoPath フォームでのさまざまなフォーム型のサポートを示し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

|フォームの種類|ASPX フォームを使用して Visual Studio で作成されたワークフロー|InfoPath フォームを使用して Visual Studio で作成されたワークフロー|
|---------------|---------------------------------------------------------|-----------------------------------------------------------------|
|関連付け|-ワークフロー **関連付け** フォーム項目テンプレートを使用して、ASPX 関連付けフォームをワークフローに追加できます。<br />-ワークフローの *Elements.xml* ファイルは、フォームが追加、名前変更、または削除されたとき、または配置パスが変更されたときにリファクタリングされます。<br />-詳細については、「 [チュートリアル: 関連付けフォームと開始フォームを使用したワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」を参照してください。|-に InfoPath アソシエーションフォームテンプレートがありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />-と InfoPath デザイナーの間には統合がありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。|
|確立|- **ワークフロー開始** フォーム項目テンプレートを使用して、ASPX 開始フォームをワークフローに追加できます。<br />-ワークフローの *Elements.xml* ファイルは、フォームが追加、名前変更、または削除されたとき、または配置パスが変更されたときにリファクタリングされます。<br />-詳細については、「 [チュートリアル: 関連付けフォームと開始フォームを使用したワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」を参照してください。|-に InfoPath アソシエーションフォームテンプレートがありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />-と InfoPath デザイナーの間には統合がありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。|
|タスク|-で使用できる ASPX タスクフォームテンプレートがありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 アプリケーションページを作成し、それにコードを追加する必要があります。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。<br />-詳細については、「[ワークフロータスクフォーム (SharePoint Foundation)](/previous-versions/office/developer/sharepoint-2010/ms438856(v=office.14)) 」を参照してください。|-には InfoPath タスクフォームテンプレートがありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />-と InfoPath デザイナーの間には統合がありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。|
|変更|-では、ASPX 変更フォームテンプレートは使用できません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 変更フォームを追加するには、アプリケーションページを作成してコードを追加する必要があります。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。 必要に応じて手動で編集する必要があります。<br />-詳細については、「[ワークフロー変更フォーム (SharePoint Foundation)](/previous-versions/office/developer/sharepoint-2010/ms480794(v=office.14)) 」を参照してください。|-には InfoPath 変更フォームテンプレートがありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />-と InfoPath デザイナーの間には統合がありません [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。|

## <a name="form-support-in-imported-sharepoint-reusable-workflows"></a>インポートされた SharePoint 再利用可能なワークフローでのフォームのサポート
 次の表は、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートされる SharePoint の再利用可能なワークフローにおける、ASPX または InfoPath フォームにおけるさまざまなフォーム型のサポートを示して [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] います。

|フォームの種類|SharePoint デザイナーから ASPX フォームがインポートされた再利用可能なワークフロー|SharePoint デザイナーから InfoPath フォームをインポートした再利用可能なワークフロー|
|---------------|-------------------------------------------------------------------------------| - |
|関連付け|-フォームは、ワークフローの *Elements.xml* ファイルで参照されます。<br />-ワークフローの *Elements.xml* ファイルは、フォームの名前が変更されたり削除されたりしたとき、または配置パスが変更されたときにリファクタリングされます。|-フォームはインポートされますが、ワークフローの *Elements.xml* では参照されません。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。|
|確立|-フォームは、ワークフローの *Elements.xml* ファイル内のワークフローによって参照されます。<br />-ワークフローの *Elements.xml* ファイルは、フォームの名前が変更されたり削除されたりしたとき、または配置パスが変更されたときにリファクタリングされます。|-フォームはインポートされますが、ワークフローの *Elements.xml* では参照されません。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。 **注:**  このシナリオを機能させるには、ルールとプロパティを追加して変更する必要があります。|
|タスク|-フォームは、ワークフローの *Elements.xml* ファイルで参照されます。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。|-フォームはインポートされますが、ワークフローの *Elements.xml* では参照されません。<br />-ワークフローの *Elements.xml* ファイルはリファクタリングされません。 **注:**  このシナリオを機能させるには、ルールとプロパティを追加して変更する必要があります。|
|変更|適用不可。 SharePoint Designer で ASPX 変更フォームを作成することはできません。|適用不可。 SharePoint デザイナーで InfoPath 変更フォームを作成することはできません。ただし、ワークフローをエクスポートするときに、.wsp ファイルには含まれていません。|

## <a name="see-also"></a>関連項目
- [チュートリアル: 関連付けフォームと開始フォームを使用したワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [SharePoint ワークフローソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
