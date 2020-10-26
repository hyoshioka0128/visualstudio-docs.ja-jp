---
title: マネージド コードのデバッグ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging managed code
- debugging ASP.NET Web applications, managed code
- managed code, debugging
ms.assetid: fa3aff01-c271-4aa7-b5b1-def560471c84
caps.latest.revision: 37
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 39076459f684aafce4e800ecad6341d120aac480
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691440"
---
# <a name="debugging-managed-code"></a>マネージド コードのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここでは、マネージド アプリケーションに共通するデバッグの問題と手法について説明します。マネージド アプリケーションは、Visual Basic、C#、C++ など、共通言語ランタイムをターゲットにした言語で記述されたアプリケーションです。 ここでは、高度な手法について説明します。 詳細については、「 [デバッガーの使用](../debugger/debugger-basics.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [出力ウィンドウの診断メッセージ](../debugger/diagnostic-messages-in-the-output-window.md)  
 <xref:System.Diagnostics.Debug> クラスと <xref:System.Diagnostics.Trace> クラスについて説明します。このクラスを使用して、 **[出力]** ウィンドウに出力されるランタイム メッセージを記述できます。 Debug クラスと Trace クラスに含まれている出力メソッドを使用すると、実行の中断を伴わない情報出力、および指定した条件が満たされなかった場合に実行の中断を伴う情報出力ができます。  
  
 [マネージド コードのアサーション](../debugger/assertions-in-managed-code.md)  
 マネージド コードのアサーションについて説明し、`Assert` メソッドの引数として指定された条件をテストします。 ここでは、サンプル コード、<xref:System.Diagnostics.Debug> クラスと <xref:System.Diagnostics.Trace> クラスのメソッドの使用に関する情報、デバッグ バージョンとリリース バージョンのコードの注意事項、副作用、アサートの引数、アサートの動作のカスタマイズ、および構成ファイルについても説明します。  
  
 [Visual Basic の Stop ステートメント](../debugger/stop-statements-in-visual-basic.md)  
 ブレークポイントの設定の代わりに使用できる `Stop` ステートメントについて説明します。 サンプル コードを示し、`Stop` ステートメントと `End` ステートメントの比較、および `Stop` ステートメントと `Assert` ステートメントの比較を行います。  
  
 [チュートリアル: Windows フォームのデバッグ](../debugger/walkthrough-debugging-a-windows-form.md)  
 Windows フォームを作成し、そのフォームをデバッグする方法を順をおって説明します。 マネージド Windows アプリケーションの標準コンポーネントである Windows フォームは、最も一般的なマネージド アプリケーションの 1 つです。 このチュートリアルでは Visual C# と Visual Basic を使用しますが、C++ を使って Windows フォームを作成する場合と方法は似ています。  
  
 [OnStart メソッドのデバッグ](../debugger/how-to-debug-the-onstart-method.md)  
 マネージド Windows サービスの `OnStart` メソッドのデバッグに使用できるコード例を紹介します。 Windows サービスの `OnStart` メソッドをデバッグするには、サービスをシミュレートする数行のコードを追加する必要があります。  
  
 [混合モードのデバッグ](../debugger/debugging-mixed-mode-applications.md)  
 混合モード アプリケーションのデバッグについて説明します。 これは、ネイティブ コードとマネージド コードを組み合わせたアプリケーションです。  
  
 [エラー: システム上でカーネル デバッガーが有効になっているため、デバッグできません](../debugger/error-debugging-isn-t-possible-because-a-kernel-debugger-is-enabled-on-the-system.md)  
 デバッグ モードで起動された [!INCLUDE[win7](../includes/win7-md.md)]、[!INCLUDE[wiprlhext](../includes/wiprlhext-md.md)]、[!INCLUDE[winxp](../includes/winxp-md.md)]、[!INCLUDE[Win2kFamily](../includes/win2kfamily-md.md)]、または Windows NT システムでマネージド コードのデバッグを試みたときに発生するエラー メッセージについて説明します。  
  
 [JIT の最適化とデバッグ](../debugger/jit-optimization-and-debugging.md)  
 デバッグでの JIT 最適化の効果について説明します。  
  
 [LINQ および DLINQ のデバッグ](../debugger/debugging-linq.md)  
 LINQ クエリのデバッグ手法について説明します。  
  
 [チュートリアル: 並列アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md)  
 **[並列タスク]** ツール ウィンドウと **[並列スタック]** ツール ウィンドウを使用して並行アプリケーションをデバッグする方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [IntelliTrace](../debugger/intellitrace.md)  
 IntelliTrace でアプリの実行履歴を記録することにより、すばやく簡単にバグを検索します。 記録されたイベントと呼び出しを前後にステップ実行して重要な時点でのアプリの状態を調べます。 多くのブレークポイントを設定することも、アプリを頻繁に再起動することもなく、コードをデバッグします。 Visual Studio Ultimate が必要です。  
  
 [アプリケーションのトレースとインストルメント](https://msdn.microsoft.com/library/773b6fc4-9013-4322-b728-5dec7a72e743)  
 アプリケーションの実行を監視するトレース、およびコードの重要な位置にトレース ステートメントを挿入するインストルメントについて説明します。 ここでは、ステートメントのインストルメンテーションとトレース、トレース スイッチ、トレース リスナー、アプリケーション コードのトレース、アプリケーション コードへのトレース ステートメントの追加、<xref:System.Diagnostics.Debug> と <xref:System.Diagnostics.Trace> を使った条件付きコンパイルの説明へのリンクを提供します。  
  
 [/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)  
 C++ で作成されたコードに <xref:System.Diagnostics.DebuggableAttribute> を追加するリンカー オプションについて説明します。 この属性は、C++ によるアタッチなどのデバッグ機能を使用するときに必要です。  
  
 [Windows サービス アプリケーションのデバッグ](https://msdn.microsoft.com/library/63ab0800-0f05-4f1e-88e6-94c73fd920a2)  
 Windows サービス アプリケーションのデバッグに関する注意事項を示します。セットアップ、プロセスとのアタッチ、サービスの `OnStart` メソッドと Main メソッドのコードのデバッグ、ブレークポイントの設定、サービス コントロール マネージャーを使用したサービスの開始、停止、一時中断、継続などが含まれます。  
  
 [デバッグとプロファイリング](https://msdn.microsoft.com/library/4a04863e-2475-46f4-bc3f-3c11510c2a4b)  
 .NET Framework アプリケーションのデバッグと構成要件について説明します。  
  
 [スクリプトと Web アプリケーションのデバッグ](../debugger/debugging-web-applications-and-script.md)  
 スクリプトおよび Web アプリケーションのデバッグ時に発生する一般的な問題、およびデバッグの手法について説明します。  
 このリリースの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で追加された新しいデバッグ機能について説明します。  
  
 [ホーム ページのデバッグ](../debugger/debugging-in-visual-studio.md)  
 デバッグに関連するドキュメントのより広範囲なリンクを提供します。 これらのリンクでは、デバッガーの新機能、設定と準備、ブレークポイント、例外処理、エディット コンティニュ、マネージド コードのデバッグ、Visual C++ プロジェクトのデバッグ、COM および ActiveX のデバッグ、DLL のデバッグ、SQL のデバッグ、ユーザー インターフェイス リファレンスなどの情報が示されます。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: デザイン時のカスタム Windows フォームコントロールのデバッグ](https://msdn.microsoft.com/library/1fd83ccd-3798-42fc-85a3-6cba99467387)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)
