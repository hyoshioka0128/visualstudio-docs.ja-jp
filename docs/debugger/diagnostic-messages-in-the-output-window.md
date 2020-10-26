---
title: 出力ウィンドウにメッセージを送信する | Microsoft Docs
ms.date: 11/08/2018
ms.topic: how-to
helpviewer_keywords:
- diagnostic messages [C#]
- System.Diagnostics.Debug class, Output window
- messages, diagnostic
- Debug.Print replacements
- diagnosis
- Output window, diagnostic messages
- System.Diagnostics.Trace class, Output window
- Trace class, diagnostic messages
- diagnostics
- debugger, Output window
- debugging [Visual Studio], diagnostic messages in Output window
- Debug class
ms.assetid: 386e9524-be17-4573-83fb-4f7c5cae0be0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 85d3c146775ac06b3118186738ee74932a4c452a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85350473"
---
# <a name="send-messages-to-the-output-window"></a>出力ウィンドウにメッセージを送信する

<xref:System.Diagnostics> クラス ライブラリに含まれている <xref:System.Diagnostics.Debug> クラスまたは <xref:System.Diagnostics.Trace> クラスを使用して、**出力**ウィンドウにランタイム メッセージを出力することができます。 プログラムの*デバッグ* バージョンだけで出力する場合は <xref:System.Diagnostics.Debug> クラスを使用します。 プログラムの*デバッグ* バージョンと*リリース* バージョンの両方で出力する場合は <xref:System.Diagnostics.Trace> クラスを使用します。

## <a name="output-methods"></a>出力メソッド
 <xref:System.Diagnostics.Trace> クラスと <xref:System.Diagnostics.Debug> クラスが提供する出力方法は次のとおりです。

- 各種の `Write` メソッド。実行を中断せずに情報を出力します。 これらのメソッドは、Visual Basic の以前のバージョンで使用されていた `Debug.Print` メソッドに代わるものです。

- <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> メソッドと <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> メソッド。指定された条件を満たさない場合は、実行を中断して情報を出力します。 既定では、`Assert` メソッドはダイアログ ボックスに情報を出力します。 詳細については、「[マネージド コードのアサーション](../debugger/assertions-in-managed-code.md)」を参照してください。

- <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName> メソッドと <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName> メソッド。常に実行を中断し、情報を出力します。 既定では、`Fail` メソッドはダイアログ ボックスに情報を出力します。

**出力**ウィンドウには、次の情報も表示されます。

- デバッガーが読み込んだり、アンロードしたりしたモジュール

- スローされた例外

- 終了したプロセス

- 終了したスレッド

## <a name="see-also"></a>関連項目
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [[出力] ウィンドウ](../ide/reference/output-window.md)
- [アプリケーションのトレースとインストルメント化](/dotnet/framework/debug-trace-profile/tracing-and-instrumenting-applications)
- [C#、F#、Visual Basic プロジェクト タイプ](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
