---
title: マネージド コードのデバッグ | Microsoft Docs
ms.date: 09/23/2019
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging managed code
- debugging ASP.NET Web applications, managed code
- managed code, debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 76b841d94aee93a1bc88f6d01161239828dee166
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73188416"
---
# <a name="debug-managed-code-c-visual-basic-f-ccli"></a>マネージド コードのデバッグ (C#、Visual Basic、F#、C++/CLI)

ここでは、マネージド アプリケーションに共通するデバッグの問題と手法について説明します。マネージド アプリケーションは、Visual Basic、C#、C++/CLI など、共通言語ランタイムをターゲットにした言語で記述されたアプリケーションです。 ここでは、高度な手法について説明します。 [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)

## <a name="in-this-section"></a>このセクションの内容

[出力ウィンドウの診断メッセージ](../debugger/diagnostic-messages-in-the-output-window.md)\
<xref:System.Diagnostics.Debug> クラスと <xref:System.Diagnostics.Trace> クラスについて説明します。このクラスを使用して、 **[出力]** ウィンドウに出力されるランタイム メッセージを記述できます。 Debug クラスと Trace クラスに含まれている出力メソッドを使用すると、実行の中断を伴わない情報出力、および指定した条件が満たされなかった場合に実行の中断を伴う情報出力ができます。

[マネージド コードのアサーション](../debugger/assertions-in-managed-code.md)\
マネージド コードのアサーションについて説明し、`Assert` メソッドの引数として指定された条件をテストします。 ここでは、サンプル コード、<xref:System.Diagnostics.Debug> クラスと <xref:System.Diagnostics.Trace> クラスのメソッドの使用に関する情報、デバッグ バージョンとリリース バージョンのコードの注意事項、副作用、アサートの引数、アサートの動作のカスタマイズ、および構成ファイルについても説明します。

[Visual Basic の Stop ステートメント](../debugger/stop-statements-in-visual-basic.md)\
ブレークポイントの設定の代わりに使用できる `Stop` ステートメントについて説明します。 サンプル コードを示し、`Stop` ステートメントと `End` ステートメントの比較、および `Stop` ステートメントと `Assert` ステートメントの比較を行います。

[チュートリアル: Windows フォームのデバッグ](../debugger/walkthrough-debugging-a-windows-form.md)\
Windows フォームを作成し、そのフォームをデバッグする方法を順をおって説明します。 マネージド Windows アプリケーションの標準コンポーネントである Windows フォームは、最も一般的なマネージド アプリケーションの 1 つです。 このチュートリアルでは Visual C# と Visual Basic を使用しますが、C++ を使って Windows フォームを作成する場合と方法は似ています。

[OnStart メソッドのデバッグ](../debugger/how-to-debug-the-onstart-method.md)\
マネージド Windows サービスの `OnStart` メソッドのデバッグに使用できるコード例を紹介します。 Windows サービスの `OnStart` メソッドをデバッグするには、サービスをシミュレートする数行のコードを追加する必要があります。

[混合モードのデバッグ](../debugger/debugging-mixed-mode-applications.md)\
混合モード アプリケーションのデバッグについて説明します。 これは、ネイティブ コードとマネージド コードを組み合わせたアプリケーションです。

[エラー: システム上でカーネル デバッガーが有効になっているため、デバッグできません](../debugger/error-debugging-isn-t-possible-because-a-kernel-debugger-is-enabled-on-the-system.md)\
デバッグ モードで起動された [!INCLUDE[win7](../debugger/includes/win7_md.md)]、[!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)]、[!INCLUDE[winxp](../code-quality/includes/winxp_md.md)]、[!INCLUDE[Win2kFamily](../code-quality/includes/win2kfamily_md.md)]、または Windows NT システムでマネージド コードのデバッグを試みたときに発生するエラー メッセージについて説明します。

[JIT の最適化とデバッグ](../debugger/jit-optimization-and-debugging.md)\
デバッグでの JIT 最適化の効果について説明します。

[LINQ および DLINQ のデバッグ](../debugger/debugging-linq.md)\
LINQ クエリのデバッグ手法について説明します。

[チュートリアル: 並行アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md)\
**[並列タスク]** ツール ウィンドウと **[並列スタック]** ツール ウィンドウを使用して並行アプリケーションをデバッグする方法について説明します。

## <a name="related-sections"></a>関連項目

[IntelliTrace](../debugger/intellitrace.md)\
IntelliTrace でアプリの実行履歴を記録することにより、すばやく簡単にバグを検索します。 記録されたイベントと呼び出しを前後にステップ実行して重要な時点でのアプリの状態を調べます。 多くのブレークポイントを設定することも、アプリを頻繁に再起動することもなく、コードをデバッグします。 Visual Studio Enterprise が必要です。

[アプリケーションのトレースとインストルメント](/dotnet/framework/debug-trace-profile/tracing-and-instrumenting-applications)\
アプリケーションの実行を監視するトレース、およびコードの重要な位置にトレース ステートメントを挿入するインストルメントについて説明します。 ここでは、ステートメントのインストルメンテーションとトレース、トレース スイッチ、トレース リスナー、アプリケーション コードのトレース、アプリケーション コードへのトレース ステートメントの追加、<xref:System.Diagnostics.Debug> と <xref:System.Diagnostics.Trace> を使った条件付きコンパイルの説明へのリンクを提供します。

[/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute)\
C++ で作成されたコードに <xref:System.Diagnostics.DebuggableAttribute> を追加するリンカー オプションについて説明します。 この属性は、C++ によるアタッチなどのデバッグ機能を使用するときに必要です。

[Windows サービス アプリケーションのデバッグ](/dotnet/framework/windows-services/how-to-debug-windows-service-applications)\
Windows サービス アプリケーションのデバッグに関する注意事項を示します。セットアップ、プロセスとのアタッチ、サービスの `OnStart` メソッドと Main メソッドのコードのデバッグ、ブレークポイントの設定、サービス コントロール マネージャーを使用したサービスの開始、停止、一時中断、継続などが含まれます。

[デバッグとプロファイリング](/dotnet/framework/debug-trace-profile/index)\
.NET アプリケーションのデバッグと構成要件について説明します。

[スクリプトと Web アプリケーションのデバッグ](how-to-enable-debugging-for-aspnet-applications.md)\
スクリプトおよび Web アプリケーションのデバッグ時に発生する一般的な問題、およびデバッグの手法について説明します。

## <a name="see-also"></a>関連項目

- [チュートリアル: カスタム Windows フォーム コントロールのデザイン時のデバッグ](/dotnet/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)