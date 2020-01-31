---
title: 例外の検査-Visual Studio |Microsoft Docs
ms.date: 1/18/2020
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- exception helper, debugger, exception
- debugging [Visual Studio], exception helper, Examine an exception
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2dae1609486ec4f3462be89b0526467dd7414647
ms.sourcegitcommit: 8cbced0fb46959a3a2494852df1e41db1177a26c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76829757"
---
# <a name="inspect-an-exception-using-the-exception-helper"></a>例外ヘルパーを使用して例外を検査する 

例外の処理は、テクノロジや専門知識のレベルに関係なく、一般的な問題です。 例外がコード内で問題の原因となっている理由を理解しておくと、フラストレーションを感じることがあります。 Visual Studio で例外をデバッグしているときは、問題のデバッグに役立つ関連する例外情報を提供することで、そのフラストレーションを軽減する必要があります。

![例外ヘルパー](media/debugger-exception-helper-default.png)

## <a name="pause-on-the-exception"></a>例外を一時停止します。
デバッガーが例外で中断した場合、そのコード行の右側に例外エラーアイコンが表示されます。 モーダルでない例外ヘルパーは、例外アイコンの近くに表示されます。

![コード行の横にある例外ヘルパー](media/debugger-exception-helper-locerror.png)

## <a name="inspect-exception-info"></a>例外情報の検査
例外ヘルパーで例外の種類と例外メッセージをすぐに読み取り、例外がスローされたかどうかを確認できます。 例外オブジェクトのプロパティを確認および表示するには、 **[詳細の表示]** リンクをクリックします。

## <a name="analyze-null-references"></a>Null 参照の分析
Visual Studio 2017 以降では、.Net と C/C++ code の両方で、`NullReferenceException` または `AccessViolation`にヒットすると、例外ヘルパーに null の分析情報が表示されます。 分析は、例外メッセージの下にテキストとして表示されます。 次の図では、情報は "**s** is null." と表示されています。

![例外ヘルパー null 分析](media/debugger-exception-helper-default.png)


> [!NOTE]
> マネージコードの Null 参照分析では、.NET バージョン4.6.2 が必要です。 現在、Null 分析はユニバーサル Windows プラットフォーム (UWP) およびその他の .NET Core アプリケーションではサポートされていません。 ジャストインタイム (JIT) コードの最適化がないコードをデバッグする場合にのみ使用できます。

## <a name="configure-exception-settings"></a>例外設定の構成 
現在の型の例外がスローされた場合、例外ヘルパーの **[例外設定]** セクションからデバッガーを中断するように構成できます。 スローされた例外でデバッガーが一時停止している場合は、チェックボックスを使用して、将来スローされたときにその例外の種類の中断を無効にすることができます。 この特定のモジュールでスローされたときにこの特定の例外を中断しない場合は、 **[例外設定]** ウィンドウで、 **[次の値からスローされた場合を除く]** の下にあるモジュール名でチェックボックスをオンにします。 

## <a name="inspect-inner-exceptions"></a>内部例外の検査 
例外に内部例外 ([InnerException](https://docs.microsoft.com/dotnet/api/system.exception.innerexception)) がある場合は、例外ヘルパーでそれらを表示できます。 複数の例外が存在する場合は、呼び出し履歴の上に表示されている左矢印と右矢印を使用して、それらの間を移動できます。

![内部例外のある例外ヘルパー](media/debugger-exception-helper-innerexception.png)

## <a name="inspect-rethrown-exceptions"></a>再スローした例外の検査
例外が `thrown` されている場合、例外ヘルパーは例外が初めてスローされたときから呼び出し履歴を表示します。 例外が複数回スローされた場合は、元の例外のコールスタックだけが表示されます。

![例外ヘルパーと再スローされる例外](media/debugger-exception-helper-innerexception.png)

## <a name="share-a-debug-session-with-live-share"></a>デバッグセッションを Live Share と共有する
例外ヘルパーから、 **[start Live Share session...]** リンクを使用して[Live Share](https://docs.microsoft.com/visualstudio/liveshare/)セッションを開始できます。Live Share セッションに参加すると、他のすべてのデバッグ情報と共に例外ヘルパーが表示されます。
