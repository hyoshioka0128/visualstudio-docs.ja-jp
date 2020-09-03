---
title: '方法: ワークフローアクティビティライブラリを作成する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflows, activity library projects
- workflow activity libraries
- projects, workflow activity libraries
ms.assetid: fb5aa940-2ae8-4b52-b52c-51c20861a7b4
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d5bc4566c1ea520ac1050227ac8e4c0aee22e617
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72604962"
---
# <a name="how-to-create-a-workflow-activity-library-legacy"></a>方法: ワークフロー アクティビティ ライブラリを作成する (レガシ)
[!INCLUDE[wfd1](../includes/wfd1-md.md)] が備えている従来の [!INCLUDE[vs2010](../includes/vs2010-md.md)]を使用してワークフロー アクティビティ ライブラリ プロジェクトを作成するには、次の手順を実行します。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

### <a name="to-create-a-workflow-activity-library-project"></a>ワークフロー アクティビティ ライブラリ プロジェクトを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. レガシデザイナーにアクセスするには、[**新しいプロジェクト**] ウィンドウの上部にあるドロップダウンリストの [ **.NET Framework 3.0** ] オプションまたは [ **.NET Framework 3.5** ] オプションを選択します。

    > [!NOTE]
    > の既定のオプション [!INCLUDE[vs2010](../includes/vs2010-md.md)] は **.NET Framework 4**です。 このオプションは、[!INCLUDE[wf](../includes/wf-md.md)] を対象とする [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] アプリケーションを作成する場合に使用され、従来のデザイナーは使用しません。

4. [ **プロジェクトの種類** ] ペインで、[Visual C#] または [Visual Basic ([ **その他の言語**] の下) を選択し、[ **ワークフロー**] を選択します。

5. [ **テンプレート** ] ペインで、[ **ワークフローアクティビティライブラリ**] を選択します。

6. [ **名前** ] ボックスに、プロジェクトのわかりやすい名前を入力します。

7. [ **場所** ] ボックスに、プロジェクトを保存するディレクトリを入力するか、[ **参照** ] をクリックして移動します。

     プロジェクト用にソリューションディレクトリを作成する場合は、[ **ソリューションのディレクトリを作成** する] チェックボックスをオンにして、[ **ソリューション名** ] ボックスに名前を入力します。

8. **[OK]** をクリックします。

## <a name="see-also"></a>参照
 従来[のアクティビティデザイナーを使用して従来の](../workflow-designer/using-the-legacy-activity-designer.md)[ワークフロープロジェクトを作成する](../workflow-designer/creating-legacy-workflow-projects.md)従来のワークフロー[アクティビティ](../workflow-designer/legacy-workflow-activities.md)[ワークフローアクティビティ](https://msdn.microsoft.com/19876dfc-dfa5-4d52-b1f5-1d087474cc52) [Windows Workflow Foundation アクティビティ](https://msdn.microsoft.com/192c4c1e-afb6-4f58-ab11-2b5bbbc2d2c0)