---
title: '方法: ワークフロープロジェクトを作成する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflow projects, creating
- projects, workflow
ms.assetid: 32299555-662c-469d-a90d-89f4700dc78c
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3cf68c1a28f662bfa4e271d3c402ef1c8946b6f1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668674"
---
# <a name="how-to-create-workflow-projects-legacy"></a>方法: ワークフロー プロジェクトを作成する (レガシ)
[!INCLUDE[wf](../includes/wf-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] プロジェクトを作成するには、次の手順を実行します。 この手順では、[!INCLUDE[wfd1](../includes/wfd1-md.md)] が備えている従来の [!INCLUDE[vs2010](../includes/vs2010-md.md)]を使用します。

### <a name="to-create-a-workflow-project"></a>ワークフロー プロジェクトを作成するには

1. [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. レガシデザイナーにアクセスするには、[**新しいプロジェクト**] ウィンドウの上部にあるドロップダウンリストの [ **.NET Framework 3.0** ] オプションまたは [ **.NET Framework 3.5** ] オプションを選択します。

    > [!NOTE]
    > の既定のオプション [!INCLUDE[vs2010](../includes/vs2010-md.md)] は **.NET Framework 4**です。 このオプションは、[!INCLUDE[wf](../includes/wf-md.md)] を対象とする [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] アプリケーションを作成する場合に使用され、従来のデザイナーは使用しません。

4. [ **プロジェクトの種類** ] ペインで、[Visual C# プロジェクト] または [Visual Basic プロジェクト] を選択し、[ **ワークフロー**] を選択します。

5. [ **テンプレート** ] ペインで、インストールされているプロジェクトテンプレートの1つを選択します。

    - シーケンシャル ワークフロー コンソール アプリケーション

    - シーケンシャル ワークフロー ライブラリ

    - ワークフロー アクティビティ ライブラリ

    - ステート マシンのワークフロー コンソール アプリケーション

    - ステート マシンのワークフロー ライブラリ

    - 空のワークフロー プロジェクト

6. [ **名前** ] ボックスに、プロジェクトのわかりやすい名前を入力します。

7. [ **場所** ] ボックスに、プロジェクトを保存するディレクトリを入力するか、[ **参照** ] をクリックしてディレクトリに移動します。

     プロジェクト用にソリューションディレクトリを作成する場合は、[ **ソリューションのディレクトリを作成** する] チェックボックスをオンにして、[ **ソリューション名** ] ボックスに名前を入力します。

8. **[OK]** をクリックします。

## <a name="see-also"></a>参照
 [従来のワークフロー プロジェクトの作成](../workflow-designer/creating-legacy-workflow-projects.md)