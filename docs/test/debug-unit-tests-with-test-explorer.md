---
title: テスト エクスプローラーを使用して単体テストをデバッグする
description: Visual Studio でテスト エクスプローラーを使用して単体テストをデバッグする方法について説明します。
ms.date: 07/14/2020
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7b811cc3538e3bbb108e50acf50c2fe7a977fe3d
ms.sourcegitcommit: da7f093db52df5dcd67e0a030e616b307f0dc2a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91211288"
---
# <a name="debug-and-analyze-unit-tests-with-test-explorer"></a>テスト エクスプローラーを使用した単体テストのデバッグと分析

テスト エクスプローラーを使用して、テストのデバッグ セッションを開始できます。 Visual Studio デバッガーを使用してコードをシームレスにステップ実行すると、テスト対象のプロジェクトと単体テストの間を切り替えることができます。 デバッグを開始するには:

1. Visual Studio エディターで、デバッグする 1 つ以上のテスト メソッドにブレークポイントを設定します。

    > [!NOTE]
    > テスト メソッドを任意の順序で実行できるため、デバッグするすべてのテスト メソッドにブレークポイントを設定します。

::: moniker range="vs-2017"
2. テスト エクスプローラーでテスト メソッドを選択し、右クリック メニューの **[選択したテストのデバッグ]** を選択します。
::: moniker-end
::: moniker range=">=vs-2019"
2. テスト エクスプローラーでテスト メソッドを選択し、右クリック メニューの **[デバッグ]** を選択します。

   ![テスト実行の詳細](../test/media/vs-2019/test-explorer-debug.png)
::: moniker-end

   デバッガーについて詳しくは、[Visual Studio でのデバッグ](../debugger/debugger-feature-tour.md)に関するページをご覧ください。

## <a name="diagnose-test-method-performance-issues"></a>テスト メソッドのパフォーマンスの問題を診断する

::: moniker range="vs-2017"
テスト メソッドに時間がかかる原因を診断するには、テスト エクスプローラーでメソッドを選択し、右クリック メニューの **[選択したテストのプロファイル]** を選択します。 [インストルメンテーション プロファイリング レポート](../profiling/understanding-instrumentation-data-values.md?view=vs-2017&preserve-view=true)を参照してください。
::: moniker-end

::: moniker range=">=vs-2019"
テスト メソッドに時間がかかる原因を診断するには、エクスプローラーでメソッドを選択し、右クリック メニューの **[プロファイル]** を選択します。 [インストルメンテーション プロファイリング レポート](../profiling/understanding-instrumentation-data-values.md?view=vs-2017&preserve-view=true)を参照してください。
::: moniker-end

> [!NOTE]
> この機能は .NET Core では現在サポートされていません。

## <a name="see-also"></a>関連項目

- [コードの単体テスト](../test/unit-test-your-code.md)
- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md)
- [テスト エクスプローラーに関する FAQ](test-explorer-faq.md)
