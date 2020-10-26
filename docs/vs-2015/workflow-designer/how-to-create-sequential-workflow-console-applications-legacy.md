---
title: '方法: シーケンシャルワークフローコンソールアプリケーションを作成する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflows, console applications
- sequential workflows, console applications
- console applications, sequential workflow
ms.assetid: 9f7be7fa-551f-42c6-a9bb-f5ae8ab83625
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c9e3f97021e742db7b22a400dee0682669b07e4c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662727"
---
# <a name="how-to-create-sequential-workflow-console-applications-legacy"></a>方法: シーケンシャル ワークフロー コンソール アプリケーションを作成する (レガシ)
[!INCLUDE[wfd1](../includes/wfd1-md.md)] が備えている従来の [!INCLUDE[vs2010](../includes/vs2010-md.md)]を使用してシーケンシャル ワークフロー コンソール アプリケーション プロジェクトを作成するには、次の手順を実行します。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

### <a name="to-create-a-sequential-workflow-console-application"></a>シーケンシャル ワークフロー コンソール アプリケーションを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. レガシデザイナーにアクセスするには、[**新しいプロジェクト**] ウィンドウの上部にあるドロップダウンリストの [ **.NET Framework 3.0** ] オプションまたは [ **.NET Framework 3.5** ] オプションを選択します。

    > [!NOTE]
    > の既定のオプション [!INCLUDE[vs2010](../includes/vs2010-md.md)] は **.NET Framework 4**です。 このオプションは、[!INCLUDE[wf](../includes/wf-md.md)] を対象とする [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] アプリケーションを作成する場合に使用され、従来のデザイナーは使用しません。

4. [ **プロジェクトの種類** ] ペインで、[Visual C# プロジェクト] または [Visual Basic プロジェクト ([ **その他の言語**]) を選択し、[ **ワークフロー**] を選択します。

5. [ **テンプレート** ] ペインで、[ **シーケンシャルワークフローコンソールアプリケーション**] を選択します。

6. [ **名前** ] ボックスに、プロジェクトのわかりやすい名前を入力します。

7. [ **場所** ] ボックスに、プロジェクトを保存するディレクトリを入力するか、[ **参照** ] をクリックして移動します。

     Windows フォーム デザイナが開き、作成済みプロジェクトの Form1 が表示されます。

8. **[OK]** をクリックします。

     ワークフロー デザイナが開き、作成済みシーケンシャル ワークフローのワークフロー デザイン サーフェイスが表示されます。

9. アクティビティを [ **ツールボックス** **]** からデザイン画面にドラッグします。

## <a name="see-also"></a>参照
 [従来のワークフロープロジェクトの作成](../workflow-designer/creating-legacy-workflow-projects.md)[ワークフローの開発](https://msdn.microsoft.com/557bcb1f-a7ab-49f6-8df7-2706b7001301)