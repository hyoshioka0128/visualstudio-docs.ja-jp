---
title: '方法: ワークフロープロジェクトに新しい項目を追加する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 004f079576b792fb76d596ee8ebac3f6f96f316e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656626"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>方法 : ワークフロー プロジェクトへ新しい項目を追加する
ワークフロー プロジェクトを作成した後に、ワークフロー アクティビティ、デザイナーなどの一般的な [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 項目をプロジェクトに追加できます。

 次の表は、ワークフロー プロジェクトに追加できる [!INCLUDE[wf](../includes/wf-md.md)] 項目の一覧です。

|名前|説明|
|----------|-----------------|
|アクティビティ|他のアクティビティで構成されるアクティビティ。 この項目を選択すると、新しいプロジェクトの [ **アクティビティライブラリ** ] テンプレートを選択したときに取得したものと同じ XAML ファイルがプロジェクトに追加されます。 [!INCLUDE[crabout](../includes/crabout-md.md)] この手順については、「 [How to: Create a Activity Library](../workflow-designer/how-to-create-an-activity-library.md)」を参照してください。|
|アクティビティ デザイナー|アクティビティのデザイン時の操作をカスタマイズするデザイナー。 この項目を選択すると、新しいプロジェクトに対して [ **アクティビティデザイナーライブラリ** ] テンプレートを選択したときに取得したものと同じファイルがプロジェクトに追加されます。 [!INCLUDE[crabout](../includes/crabout-md.md)] この手順については、「 [方法: アクティビティデザイナーライブラリを作成](../workflow-designer/how-to-create-an-activity-designer-library.md)する」を参照してください。|
|Code アクティビティ|コードに記述される実行ロジックを含むアクティビティ。 <xref:System.Activities.CodeActivity.Execute%2A> メソッドのオーバーライドを含むソース コード ファイルは既に自動的に生成されています。|
|WCF ワークフロー サービス|ワークフロー アクティビティを使用して作成された [!INCLUDE[indigo2](../includes/indigo2-md.md)] サービス。 この項目を選択すると、新しいプロジェクトの **WCF ワークフローサービスアプリケーション** テンプレートを選択したときに取得したものと同じファイルがプロジェクトに追加されます。 [!INCLUDE[crabout](../includes/crabout-md.md)] この手順については、「 [方法: WCF ワークフローサービスアプリケーションを作成](../workflow-designer/how-to-create-a-wcf-workflow-service-application.md)する」を参照してください。|

### <a name="to-add-a-new-item-to-a-workflow-project"></a>ワークフロー プロジェクトに新しい項目を追加するには

1. [ **プロジェクト** ] メニューの [ **新しい項目の追加**] をクリックします。

     [ **新しい項目の追加** ] ダイアログボックスが表示されます。

2. [ **インストールされたテンプレート** ] ペインで、[ **ワークフロー** グループ] を選択します。

3. 4 つの項目のいずれかを選択します。 選択可能な項目の一覧が、上記の表に示されています。

4. ダイアログボックスの下部にある [ **名前** ] ボックスに、項目の適切な名前を入力します。

5. [ **追加** ] をクリックして、現在のワークフロープロジェクトに項目を追加します。

## <a name="see-also"></a>参照
 [ワークフロー プロジェクトの作成](../workflow-designer/creating-a-workflow-project.md)