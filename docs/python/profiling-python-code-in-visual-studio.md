---
title: Python コードのパフォーマンスの測定
description: CPython ベースのインタープリターを使っているときに、Visual Studio プロファイラーを使って Python コードのパフォーマンスを調べます。
ms.date: 11/12/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 64cd7db0131843ab48410b6676551c8563b8ffbd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531782"
---
# <a name="profile-python-code"></a>Python コードのプロファイリング

CPython ベースのインタープリターを使っている場合、Python アプリケーションをプロファイリングできます (この機能を使うことができる Visual Studio のバージョンについては、[機能一覧のプロファイリング](overview-of-python-tools-for-visual-studio.md#matrix-profiling)を参照してください)。

## <a name="profiling-for-cpython-based-interpreters"></a>CPython ベースのインタープリターのプロファイリング

**[分析]**  >  **[Launch Python Profiling]\(Python プロファイリングの開始\)** メニュー コマンドでプロファイリングを開始すると、構成ダイアログが開きます。

![プロファイリング構成ダイアログ](media/profiling-start.png)

**[OK]** を選ぶと、プロファイラーが実行されてパフォーマンス レポートが表示され、アプリケーションで時間がどのように消費されたかを調べることができます。

![プロファイリング パフォーマンス レポート](media/profiling-results.png)

> [!Note]
> 現時点では、Visual Studio は、このレベルのフル アプリケーション プロファイリングのみをサポートしています。今後の機能に関するフィードバックをお寄せください。 このページの下部にある **[製品のフィードバック]** ボタンをお使いください。

## <a name="profiling-for-ironpython"></a>IronPython のプロファイリング

IronPython は CPython ベースのインタープリターではないため、上記のプロファイリング機能は使用できません。

代わりに、ターゲット アプリケーションとして *ipy.exe* を直接起動し、適切な引数を使ってスタートアップ スクリプトを起動することにより、Visual Studio .NET のプロファイラーを使います。 すべての Python コードを確実にデバッグし、プロファイリングできるようにするには、コマンド ラインに `-X:Debug` を含めます。 この引数により、IronPython ランタイムとコードの両方で費やされた時間を含むパフォーマンス レポートが生成されます。 コードは、完全修飾名を使って識別されます。

または、IronPython には独自の組み込みプロファイリングがありますが、現在は適切なビジュアライザーがありません。 利用できるものについては、「[An IronPython Profiler](https://blogs.msdn.microsoft.com/curth/2009/03/30/an-ironpython-profiler/)」(IronPython プロファイラー) (MSDN ブログ) をご覧ください。
