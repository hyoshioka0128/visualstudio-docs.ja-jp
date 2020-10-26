---
title: '方法: ステートマシンワークフローライブラリを作成する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- projects, state machine workflow library
- state machine workflow libraries
- workflows, state machine workflow library
ms.assetid: 5bd68c6e-6a98-47d9-826d-9bb7a4fd72f8
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d3cff5d6aaa28915524b7699affdf41d3bebef4a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72663378"
---
# <a name="how-to-create-a-state-machine-workflow-library-legacy"></a>方法: ステート マシン ワークフロー ライブラリを作成する (レガシ)
[!INCLUDE[wfd1](../includes/wfd1-md.md)] が備えている従来の [!INCLUDE[vs2010](../includes/vs2010-md.md)]を使用してステート マシン ワークフロー ライブラリ プロジェクトを作成するには、次の手順を実行します。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

### <a name="to-create-a-state-machine-workflow-library-project"></a>ステート マシン ワークフロー ライブラリ プロジェクトを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. レガシデザイナーにアクセスするには、[**新しいプロジェクト**] ウィンドウの上部にあるドロップダウンリストの [ **.NET Framework 3.0** ] オプションまたは [ **.NET Framework 3.5** ] オプションを選択します。

    > [!NOTE]
    > の既定のオプション [!INCLUDE[vs2010](../includes/vs2010-md.md)] は **.NET Framework 4**です。 このオプションは、[!INCLUDE[wf](../includes/wf-md.md)] を対象とする [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] アプリケーションを作成する場合に使用され、従来のデザイナーは使用しません。

4. [ **プロジェクトの種類** ] ペインで、[Visual C#] または [Visual Basic ([ **その他の言語**] の下) を選択し、[ **ワークフロー**] を選択します。

5. [ **テンプレート** ] ペインで、[ **ステートマシンのワークフローライブラリ**] を選択します。

6. [ **名前** ] ボックスに、プロジェクトのわかりやすい名前を入力します。

7. [ **場所** ] ボックスに、プロジェクトを保存するディレクトリを入力するか、[ **参照** ] をクリックして移動します。

     プロジェクト用にソリューションディレクトリを作成する場合は、[ **ソリューションのディレクトリを作成** する] チェックボックスをオンにして、[ **ソリューション名** ] ボックスに名前を入力します。

8. **[OK]** をクリックします。

## <a name="see-also"></a>参照
 [従来のワークフロープロジェクトの作成](../workflow-designer/creating-legacy-workflow-projects.md)[ステートマシンワークフロー](https://msdn.microsoft.com/library/344caacd-bf3b-4716-bd5a-eca74fc5a61d)