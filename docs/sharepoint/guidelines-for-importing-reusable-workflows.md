---
title: 再利用可能なワークフローをインポートするためのガイドライン |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- SharePoint development in Visual Studio, reusable workflows
- importing items [SharePoint development in Visual Studio]
- reusable workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bb386a2d80931ece415b0b3939f2947678808261
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62557151"
---
# <a name="guidelines-for-importing-reusable-workflows"></a>再利用可能なワークフローをインポートするためのガイドライン
  SharePoint デザイナーで作成した再利用可能なワークフローをインポートするには、の再利用可能な SharePoint 2010 ワークフロープロジェクトテンプレートを使用し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 このテンプレートは、*宣言型**ワークフロー* ( [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] -のみ) をインポートし、*コードワークフロー*に変換します。これは、 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] またはコードで拡張できるワークフローです [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] 。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][チュートリアル: SharePoint Designer の再利用可能なワークフローを Visual Studio にインポート](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)します。

 ただし、再利用可能な SharePoint 2010 ワークフローテンプレートのインポートでは、ファームソリューションのみをインポートできます。 ワークフローをサンドボックスソリューションとして配置する場合は、[SharePoint 2010 ソリューションパッケージのインポート] テンプレートを使用してワークフローをインポートします。 ただし、これを行うことで、コードワークフローに変換することはできず、そのように変更することはできません。

## <a name="import-reusable-workflows-by-using-the-import-reusable-workflow-template"></a>再利用可能なワークフローのインポートテンプレートを使用して再利用可能なワークフローをインポートする
 再利用可能な SharePoint 2010 ワークフローテンプレートを使用して再利用可能なワークフローをインポートする場合は、他の sharepoint ソリューションと同様にソリューションを実行または変更でき [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ますが、一部の項目を手動で修正することが必要になる場合があります。

### <a name="import-task-forms"></a>タスクフォームのインポート
 再利用可能な SharePoint 2010 ワークフロープロジェクトテンプレートをインポートすると、すべての開始フォームと関連付けフォームがインポートされますが、コードワークフロースキーマでは1つのタスクフォームのみが許可されるため、タスクフォームは1つだけインポートされます。 元のワークフローソリューションのその他のタスクフォームは、**ソリューションエクスプローラー**の [**その他のインポート**されたファイル] フォルダーに格納されます。

## <a name="import-reusable-workflows-by-using-the-import-sharepoint-2010-solution-package-template"></a>SharePoint 2010 ソリューションパッケージのインポートテンプレートを使用して再利用可能なワークフローをインポートする
 SharePoint 2010 ソリューションパッケージのインポートテンプレートを使用して再利用可能なワークフローをインポートする場合は、次の問題を考慮する必要があります。

- ワークフローをインポートしたら、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] F5 キーを **押し** てですぐにデプロイして実行できます。 ただし、インポートされたソリューションでワークフロー内の何かを変更した場合は、ワークフローを配置して実行する前に、プロジェクト内の要素を手動で修正することが必要になる場合があります。

- ワークフローは宣言型であるため、コードを追加することはできません。 ワークフローをコードワークフローに変換するには、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] [再利用可能な SharePoint 2010 のインポート] ワークフローテンプレートを使用して、ワークフローをにインポートする必要があります。

- ワークフローデザイナー (xoml) ファイルはデザインビューで編集できますが、ワークフローデザイナーでは誤ったエラーが表示されるため、ソースビューで編集することをお勧めします。

- ワークフローでのデバッグは、宣言型コンテンツに対しては機能しません。 で設定されたブレークポイント [!INCLUDE[wfd2](../sharepoint/includes/wfd2-md.md)] はヒットしません。

## <a name="import-globally-reusable-workflow-solutions"></a>グローバルに再利用可能なワークフローソリューションをインポートする
 再利用可能な SharePoint 2010 ワークフローテンプレートを使用して、グローバルに再利用可能なワークフローをインポートすることはできません。 グローバルに再利用可能なワークフローをインポートするには、グローバルに再利用可能なワークフローに変換するか、または SharePoint 2010 ソリューションパッケージのインポートテンプレートを使用する必要があります。

 ワークフローを変換するには、SharePoint デザイナーでグローバルに再利用可能なワークフローのコピーを作成します (ワークフローのショートカットメニューを開き、[ **コピーとして保存**] をクリックします)。 次に、の再利用可能な SharePoint 2010 ワークフローテンプレートを使用して、再利用可能な新しいワークフローをインポートし [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

 グローバルに再利用可能なワークフローを変更せずにインポートするには、[SharePoint 2010 ソリューションパッケージのインポート] テンプレートを使用します。 このメソッドを使用すると、ワークフローはコードワークフローに変換されず、宣言型ワークフローのままになります。

## <a name="see-also"></a>こちらもご覧ください
- [既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [チュートリアル: SharePoint Designer の再利用可能なワークフローを Visual Studio にインポートする](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)
