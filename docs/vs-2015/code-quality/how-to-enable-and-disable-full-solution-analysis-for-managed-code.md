---
title: '方法: マネージコードの完全なソリューション分析を有効または無効にする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
ms.assetid: 04315147-5792-47f0-8b5f-9ac8413c6a57
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 72b27bf9dcc1f0ee8a222ac701f2ffae4fc68614
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72646291"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>方法: マネージド コードの完全ソリューション解析を有効/無効にする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注意]
> このトピックは、Visual Studio 2015 Update 3 RC 以降にのみ適用されます。

 *完全なソリューション分析* は、visual Studio の機能です。この機能を使用すると、ソリューション内の開いている Visual c# または Visual Basic ファイルにのみコード分析の問題があるか、またはソリューション内の開いている Visual c# または Visual Basic ファイルの両方でコード分析の問題が発生したかを選択できます。

 すべてのファイル内のすべての問題が役に立ちますが、ソリューションが非常に大きい場合や、ファイルが多数ある場合は、Visual Studio の速度が低下する可能性があります。  表示される問題の数を制限し、Visual Studio のパフォーマンスを向上させるには、完全なソリューション分析を無効にすることができます。 必要に応じて、この機能を簡単に有効にすることができます。

#### <a name="to-toggle-full-solution-analysis"></a>完全なソリューション分析を切り替えるには

1. Visual Studio のメインメニューで、[ **ツール** ] &#124; [ **オプション** ] の順に選択し、[ **オプション** ] ダイアログボックスを表示します。

2. [ **オプション** ] ダイアログボックスで、[ **テキストエディター** &#124; **C#** ] または [ **基本** &#124; **[詳細設定**] を選択します。

3. 完全なソリューション分析を有効にする場合は [ **完全なソリューション分析を有効** にする] チェックボックスをオンにし、無効にする場合はオフにします。 完了したら、 **[OK** ] をクリックします。

     ![[完全なソリューション分析を有効にする] チェックボックスをオンにします。](../code-quality/media/fsa-toolsoptions.png "FSA_ToolsOptions")

## <a name="results-of-enabling-and-disabling-full-solution-analysis"></a>完全なソリューション分析を有効または無効にした結果
 次のスクリーンショットでは、完全なソリューション分析が有効になっている場合に結果を確認できます。 ファイルが開いているかどうかに関係なく、ソリューション内の *すべて* のファイルのすべてのエラーとコード分析の問題が表示されます。

 ![完全なソリューション分析が有効になりました。](../code-quality/media/fsa-enabled.png "FSA_Enabled")

 次のスクリーンショットは、完全なソリューション分析を無効にした後の同じソリューションの結果を示しています。 エラー一覧には、開いているソリューションファイルのエラーとコード分析の問題のみが表示されます。

 ![完全なソリューション分析が無効になっています。](../code-quality/media/fsa-disabled.png "FSA_Disabled")

## <a name="automatically-disabling-full-solution-analysis"></a>完全なソリューション分析を自動的に無効にする
 使用可能なシステムメモリが200MB 以下であることが Visual Studio によって検出されると、完全なソリューション分析 (およびその他の機能) が有効になっている場合は自動的に無効になります。 この問題が発生した場合は、通知が表示されます。 ボタンを使用すると、完全なソリューション分析を再び有効にすることができます。

 ![アラートテキストの完全なソリューション分析の中断](../code-quality/media/fsa-alert.png "FSA_Alert")

## <a name="additional-details"></a>追加情報
 既定では、完全なソリューション分析は Visual Basic に対して有効になり、Visual C# では無効になります。

 Visual Studio Update 3 RC には、完全なソリューション分析が有効になっている場合でも、メモリ使用量を大幅に削減し、CPU 時間を短縮する、強化されたコードアナライザー診断 v2 エンジンが含まれています。
