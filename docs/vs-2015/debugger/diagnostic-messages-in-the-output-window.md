---
title: 出力ウィンドウ | の診断メッセージMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.output
dev_langs:
- FSharp
- VB
- CSharp
- C++
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
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 60f8da2430e1c84af3c26be31c6de561291c8c6e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695293"
---
# <a name="diagnostic-messages-in-the-output-window"></a>出力ウィンドウの診断メッセージ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:System.Diagnostics> クラス ライブラリに含まれている Debug クラスまたは Trace クラスを使用して、[出力] ウィンドウに出力されるランタイム メッセージを記述できます。 プログラムのデバッグ バージョンだけで出力する場合は Debug クラスを使用します。 プログラムのデバッグ バージョンとリリース バージョンの両方で出力する場合は Trace クラスを使用します。  
  
## <a name="output-methods"></a>出力メソッド  
 <xref:System.Diagnostics.Trace> クラスと <xref:System.Diagnostics.Debug> クラスが提供する出力方法は次のとおりです。  
  
- 各種の `Write` メソッド。実行を中断せずに情報を出力します。 これらのメソッドは、Visual Basic の以前のバージョンで使用されていた `Debug.Print` メソッドに代わるものです。  
  
- <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName><xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>メソッドとメソッド。指定された条件が失敗した場合に、実行を中断し、情報を出力します。 既定では、`Assert` メソッドはダイアログ ボックスに情報を出力します。 詳細については、「[マネージド コードのアサーション](../debugger/assertions-in-managed-code.md)」を参照してください。  
  
- <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName> メソッドと <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName> メソッド。常に実行を中断して情報を出力します。 既定では、`Fail` メソッドはダイアログ ボックスに情報を出力します。  
  
  アプリケーションからのプログラムの作成に加えて、[ **出力** ] ウィンドウには次の情報が表示されます。  
  
- デバッガーが読み込んだり、アンロードしたりしたモジュール  
  
- スローされた例外  
  
- 終了したプロセス  
  
- 終了したスレッド  
  
## <a name="see-also"></a>参照  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [[出力ウィンドウ]](../ide/reference/output-window.md)   
 [アプリケーションのトレースとインストルメント](https://msdn.microsoft.com/library/773b6fc4-9013-4322-b728-5dec7a72e743)   
 [インストルメンテーションとトレースの概要](https://msdn.microsoft.com/e924e57c-33cf-4b0e-9e7f-a45d13e38f2c)   
 [C#、F #、および Visual Basic プロジェクトの種類](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
