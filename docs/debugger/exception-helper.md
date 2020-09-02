---
title: 例外を調べる - Visual Studio | Microsoft Docs
ms.date: 1/18/2020
ms.topic: how-to
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
ms.openlocfilehash: 75d044ed5ddaf4b7eb7a66bc09c8b3de3502a50f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85350499"
---
# <a name="inspect-an-exception-using-the-exception-helper"></a>例外ヘルパーを使用して例外を調べる 

例外の処理は、テクノロジや専門知識のレベルに関係なく、一般的な問題です。 例外がコードでの問題の原因になっている理由を究明していると、フラストレーションを感じることがあります。 Visual Studio で例外をデバッグしているときは、問題のすばやいデバッグに役立つ関連する例外情報が提供されるので、そのフラストレーションが軽減されます。

![例外ヘルパー](media/debugger-exception-helper-default.png)

## <a name="pause-on-the-exception"></a>例外で一時停止する
デバッガーが例外で中断した場合、そのコード行の右側に例外エラー アイコンが表示されます。 例外アイコンの近くに、非モーダルの例外ヘルパーが表示されます。

![コード行の隣の例外ヘルパー](media/debugger-exception-helper-locerror.png)

## <a name="inspect-exception-info"></a>例外の情報を調べる
例外ヘルパーで簡単に、例外の種類と例外メッセージ、および例外がスローされたか、またはハンドルされなかったかどうかを、読むことができます。 **[詳細の表示]** リンクをクリックすることで、例外オブジェクトのプロパティを調べたり表示したりできます。

## <a name="analyze-null-references"></a>null 参照を分析する
Visual Studio 2017 以降 (.Net と C/C++ コードの両方)、`NullReferenceException` または `AccessViolation` にヒットすると、例外ヘルパーに null の分析情報が表示されます。 分析は、例外メッセージの下にテキストとして表示されます。 次の図の情報では、"**s** が null であった" ことが示されています。

![例外ヘルパーの null 分析](media/debugger-exception-helper-default.png)


> [!NOTE]
> マネージド コードでの null 参照の分析には、.NET バージョン 4.6.2 が必要です。 現在、null 分析はユニバーサル Windows プラットフォーム (UWP) アプリケーションおよび他の .NET Core アプリケーションではサポートされていません。 Just-In-Time (JIT) コード最適化が行われていないコードをデバッグする場合にのみ使用できます。

## <a name="configure-exception-settings"></a>例外設定を構成する 
例外ヘルパーの **[例外設定]** セクションでは、現在の種類の例外がスローされたときに中断するようにデバッガーを構成できます。 スローされた例外でデバッガーが一時停止した場合、チェック ボックスを使用して、その例外の種類が将来スローされたときの中断を無効にすることができます。 この特定のモジュールでこの特定の例外がスローされたときに中断しないようにする場合は、 **[例外設定]** ウィンドウの **[次からスローされた場合を除く:]** でモジュール名のチェック ボックスをオンにします。 

## <a name="inspect-inner-exceptions"></a>内部例外を調べる 
例外に内部例外 ([InnerException](https://docs.microsoft.com/dotnet/api/system.exception.innerexception)) が含まれる場合は、例外ヘルパーでそれらを表示できます。 複数の例外が存在する場合は、呼び出し履歴の上に表示される左右の矢印を使用して、それらの間を移動できます。

![例外ヘルパーと内部例外](media/debugger-exception-helper-innerexception.png)

## <a name="inspect-rethrown-exceptions"></a>再スローされた例外を調べる
例外が `thrown` されている場合、例外ヘルパーには例外が初めてスローされたときからの呼び出し履歴が表示されます。 例外が複数回スローされた場合は、元の例外の呼び出し履歴だけが表示されます。

![例外ヘルパーと再スローされた例外](media/debugger-exception-helper-innerexception.png)

## <a name="share-a-debug-session-with-live-share"></a>デバッグ セッションを Live Share と共有する
**[Live Share セッションを開始]** リンクを使用して、例外ヘルパーから [Live Share](https://docs.microsoft.com/visualstudio/liveshare/) セッションを開始できます。Live Share セッションに参加しているすべてのユーザーは、他のすべてのデバッグ情報と共に例外ヘルパーを見ることができます。
