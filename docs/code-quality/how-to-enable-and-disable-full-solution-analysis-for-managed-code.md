---
title: マネージコードの完全なソリューション分析を有効 & 無効にする
ms.date: 03/23/2018
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d699dd74315cfc36820c1cdb4120543e0290b1a1
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587512"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>方法: マネージコードの完全なソリューション分析を有効または無効にする

*完全なソリューション分析*では、コード分析にC#よって、エディターで開いているかどうかに関係なく、ソリューション内のすべてのファイルまたは Visual Basic ファイルが検証されます。 既定では、完全なソリューション分析は Visual Basic に対し*て有効*になり、でC#は*無効*になります。

すべてのファイルのすべての問題を確認すると役に立つ場合がありますが、邪魔になることもあります。 ソリューションのサイズが非常に大きい場合や、ファイルが多数ある場合は、Visual Studio の速度が低下します。 表示される問題の数を制限し、Visual Studio のパフォーマンスを向上させるには、完全なソリューション分析を無効にすることができます。 必要に応じて、この機能を簡単に有効にすることができます。

次の図では、完全なソリューション分析が有効になっています。 ソリューション内のすべてのファイルのコンパイラおよびコード分析の問題は、開いていない場合でも表示されます。

![完全なソリューション分析が有効になりました。](../code-quality/media/fsa_enabled.png)

次の図は、完全なソリューション分析を無効にした後の同じソリューションの結果を示しています。 開いているソリューションファイルのコンパイラエラーとコード分析の問題のみがエラー一覧に表示されます。

![完全なソリューション分析が無効になっています。](../code-quality/media/fsa_disabled.png)

## <a name="toggle-full-solution-analysis"></a>完全なソリューション分析の切り替え

1. **[オプション]** ダイアログボックスを開くには、Visual Studio のメニューバーで **[ツール]** [ > **オプション**] の順に選択します。

1. **[オプション]** ダイアログボックスで、 **[テキストエディター** **C#**  > ] または [**基本** > **詳細設定**] を選択します。

1. 完全なソリューション分析を有効にする場合は [**完全なソリューション分析を有効**にする] チェックボックスをオンにし、無効にする場合はオフにします。 完了したら、 **[OK]** を選択します。

   ![[完全なソリューション分析を有効にする] チェックボックスをオンにします。](../code-quality/media/options-enable-full-solution-analysis.png)

## <a name="automatically-disable-full-solution-analysis"></a>完全なソリューション分析を自動的に無効にする

Visual Studio で 200 MB 以下のシステムメモリが使用可能であることが検出されると、完全なソリューション分析 (およびその他の機能) が有効になっている場合は自動的に無効になります。 これが発生すると、Visual Studio が一部の機能を無効にしたことを通知するアラートが表示されます。 ボタンを使用すると、必要に応じて完全なソリューション分析を再び有効にすることができます。

![完全ソリューション解析を中断する警告テキスト](../code-quality/media/fsa_alert.png)
