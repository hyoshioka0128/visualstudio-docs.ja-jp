---
title: 'デバッグの準備: コンソールプロジェクト |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], console applications
- debugging console applications
- console applications, debugging
ms.assetid: 9641f1d9-2d5a-48b1-8731-6525e8f67892
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5ac87f6c5ef5fcf9fc7ca5532fe7436dedb8ba97
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691214"
---
# <a name="debugging-preparation-console-projects"></a>デバッグの準備 : コンソール プロジェクト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コンソール プロジェクトのデバッグの準備は Windows プロジェクトのデバッグの準備に似ていますが、次の点を考慮する必要があります。 詳細については、「[Windows フォーム アプリケーション](../debugger/debugging-preparation-windows-forms-applications.md)」および「[デバッグの準備: Windows フォーム アプリケーション (.NET)](https://msdn.microsoft.com/a8bc54de-41a3-464d-9a12-db9bdcbc1ad5)」を参照してください。 コンソール アプリケーションはどれも類似しているため、このトピックでは次のプロジェクトの種類について説明します。  
  
- C# コンソール アプリケーション  
  
- Visual Basic コンソール アプリケーション  
  
- C++ コンソール アプリケーション (.NET)  
  
- C++ コンソール アプリケーション (Win32)  
  
  コンソール アプリケーションのコマンド ライン引数を指定する必要がある場合があります。 詳細については、次を参照してください[C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)、 [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)、または[c# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)。  
  
  すべてのプロジェクト プロパティと同様に、これらの引数はデバッグ セッション間および Visual Studio セッション間で保持されます。 したがって、コンソールアプリケーションが前にデバッグしたものである場合は、[ ** \<Project> プロパティページ**] ダイアログボックスで入力した前のセッションの引数がある可能性があることに注意してください。  
  
  コンソール アプリケーションは、 **[コンソール]** ウィンドウを使用して、入力を受け付けたり出力メッセージを表示したりします。 **[コンソール]** ウィンドウに書き込むには、アプリケーションで Debug オブジェクトではなく **Console** オブジェクトを使用する必要があります。 ただし、**Visual Studio の出力**ウィンドウに書き込むには、通常どおりに Debug オブジェクトを使用します。 アプリケーションの書き込み先を理解し、間違った場所でメッセージを探すことのないようにしてください。 詳細については、「[Console クラス](https://msdn.microsoft.com/library/system.console.aspx)」、「[Debug クラス](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx)」、「[[出力] ウィンドウ](../ide/reference/output-window.md)」を参照してください。  
  
## <a name="starting-the-application"></a>アプリケーションの起動  
 いくつかのコンソール アプリケーションが起動すると、それらのアプリケーションは最後まで実行されてから終了します。 この動作のため、実行を中断してデバッグする時間が十分ない場合があります。 アプリケーションをデバッグできるようにするには、次のいずれかの手順に従ってアプリケーションを起動します。  
  
- アプリケーションを起動し、ブレークポイントに達するまで実行する。  
  
- アプリケーションを起動し、ソース コードの最初の行ですぐに中断する。  
  
- ソースコードウィンドウで、行を右クリックし、[カーソル行の前 **まで実行**] をクリックします。  
  
   アプリケーションが起動され、選択した行まで実行されます。または、その行に達する前にブレークポイントがヒットした場合は、ブレークポイントまで実行されます。  
  
  コンソール アプリケーションをデバッグする場合、Visual Studio からではなく、コマンド プロンプトからアプリケーションを起動することもできます。 その場合は、コマンド プロンプトからアプリケーションを起動し、Visual Studio デバッガーをアプリケーションにアタッチします。 詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。  
  
  Visual Studio からコンソール アプリケーションを起動すると、 **[コンソール]** ウィンドウが Visual Studio ウィンドウの背後に表示される場合があります。 Visual Studio からコンソール アプリケーションを起動しようとしても、何も起こらない場合は、Visual Studio ウィンドウを移動してみてください。  
  
## <a name="see-also"></a>参照  
 [ネイティブコードのデバッグ](../debugger/debugging-native-code.md)   
 [マネージコードのデバッグ](../debugger/debugging-managed-code.md)   
 [Visual C++ のプロジェクトの種類](../debugger/debugging-preparation-visual-cpp-project-types.md)   
 [C#、F #、および Visual Basic プロジェクトの種類](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)
