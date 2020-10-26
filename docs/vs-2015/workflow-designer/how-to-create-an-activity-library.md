---
title: '方法: アクティビティライブラリを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 1eeebe74-7303-4345-8a83-fe37a26bc84b
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9dec73d392dc6af74e5daef99bd6d306f7d58409
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662757"
---
# <a name="how-to-create-an-activity-library"></a>アクティビティ ライブラリを作成する方法
カスタム アクティビティは、ワークフローで特定のビジネス プロセスをモデル化するために使用されます。 [!INCLUDE[vs2010](../includes/vs2010-md.md)] のアクティビティ ライブラリ テンプレートでは、[!INCLUDE[wfd1](../includes/wfd1-md.md)]を使用して、こうしたカスタム アクティビティを視覚的に作成できます。

### <a name="to-create-a-workflow-activity-library"></a>ワークフロー アクティビティ ライブラリを作成するには

1. [!INCLUDE[vs2010](../includes/vs2010-md.md)]を起動します。

2. [ **ファイル** ] メニューの [ **新規作成**] をポイントし、[ **プロジェクト**] をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. [**プロジェクトの種類**] ペインで、使用している言語に応じて、 **Visual C#** プロジェクトまたは**Visual Basic**グループから [**ワークフロー** ] を選択します。

4. [ **テンプレート** ] ウィンドウで、[ **アクティビティライブラリ**] を選択します。

5. [ **名前** ] ボックスに、プロジェクトのわかりやすい名前を入力します。

6. [ **場所** ] ボックスに、プロジェクトを保存するディレクトリを入力するか、[ **参照** ] をクリックして移動します。

7. [ **ソリューション** ] ボックスにソリューションの内容を示す名前を入力し、[ **OK]** をクリックします。

    > [!NOTE]
    > ワークフローコンソールアプリケーションを既存のソリューションに追加する場合は、でそのソリューションを開き [!INCLUDE[vs2010](../includes/vs2010-md.md)] 、**ソリューションエクスプローラー**でソリューションを右クリックして、[**追加**]、[**新しいプロジェクト...** ] の順に選択します。 を選択すると、[ **新しいプロジェクト** ] ダイアログボックスが開きます。 上記の手順を実行します。

8. プロジェクト テンプレートによって、XAML でアクティビティ定義が作成されます。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] で、カスタム アクティビティ用のキャンバスが開かれて表示されます。

9. アクティビティを [ **ツールボックス** ] からデザイン画面にドラッグして、カスタムアクティビティに追加します。

    > [!CAUTION]
    > カスタム アクティビティの本体に含めることができる子アクティビティは 1 つのみです。ただし、その子アクティビティは、<xref:System.Activities.Statements.Sequence> アクティビティや <xref:System.Activities.Statements.Flowchart> アクティビティなどの複合アクティビティにすることができます。

## <a name="see-also"></a>参照
 方法:[ワークフロープロジェクトを作成](../workflow-designer/creating-a-workflow-project.md)する[アクティビティを作成する](https://msdn.microsoft.com/library/c09b1e99-21b5-4d96-9c04-ec31db3f4436)