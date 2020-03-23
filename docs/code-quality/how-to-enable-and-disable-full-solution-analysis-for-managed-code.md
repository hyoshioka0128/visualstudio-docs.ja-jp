---
title: マネージ コードの完全なソリューション分析を有効&無効にする
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
ms.sourcegitcommit: b32fbbcbc43910b0ed7ce79aa9a22f2ed36ab57e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428189"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>方法: マネージ コードの完全なソリューション分析を有効または無効にする

*完全なソリューション分析*とは、コード分析が、エディターで開いているかどうかにかかわらず、ソリューション内のすべての C# ファイルまたは Visual Basic ファイルを調べることを意味します。 既定では、完全なソリューション分析は Visual Basic で*有効*になり、C# では*無効*になっています。

すべてのファイルで問題を確認すると便利ですが、気が散ることもあります。 ソリューションが非常に大きい場合や、ファイル数が多い場合は、Visual Studio の処理速度が低下します。 表示される問題の数を制限し、Visual Studio のパフォーマンスを向上させるには、完全なソリューション分析を無効にできます。 必要に応じて、この機能を簡単に再有効化できます。

次の図では、完全な解析解析が有効になっています。 ソリューション内のすべてのファイルで、コンパイラとコード分析の問題が表示されます。

![完全なソリューション分析が有効になっています。](../code-quality/media/fsa_enabled.png)

次の図は、完全なソリューション分析を無効にした後の同じソリューションの結果を示しています。 開いているソリューション ファイルのコンパイラ エラーとコード分析の問題のみがエラー一覧に表示されます。

![完全なソリューション分析が無効になりました。](../code-quality/media/fsa_disabled.png)

## <a name="toggle-full-solution-analysis"></a>完全な解析の切り替え

1. [**オプション]** ダイアログ ボックスを開くには、Visual Studio のメニュー バーで [**ツール** > **オプション]** を選択します。

1. [**オプション]** ダイアログ ボックスで、[**テキスト エディタ** > **C#]** または **[基本** > **詳細設定**] を選択します。

1. [**完全なソリューション分析を有効にする**] チェック ボックスをオンにして完全なソリューション分析を有効にするか、オフにして無効にします。 完了したら **[OK]を選択します**。

   ![[完全なソリューション分析を有効にする] チェック ボックスをオンにします。](../code-quality/media/options-enable-full-solution-analysis.png)

## <a name="automatically-disable-full-solution-analysis"></a>完全なソリューション分析を自動的に無効にする

Visual Studio が 200 MB 以下のシステム メモリを使用できることを検出すると、有効になっている場合は、ソリューション分析 (およびその他の機能) が自動的に無効になります。 この場合、Visual Studio が一部の機能を無効にしたことを通知する警告が表示されます。 ボタンを使用すると、必要に応じ完全なソリューション分析を再度有効にできます。

![完全なソリューション分析を中断するアラート テキスト](../code-quality/media/fsa_alert.png)
