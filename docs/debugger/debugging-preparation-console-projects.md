---
title: コンソールプロジェクトのデバッグの準備 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], console applications
- debugging console applications
- console applications, debugging
ms.assetid: 9641f1d9-2d5a-48b1-8731-6525e8f67892
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e612228bf5440936c336d286962820a02d6bd071
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916280"
---
# <a name="debugging-preparation-console-projects-c-c-visual-basic-f"></a>デバッグの準備: コンソールプロジェクトC#( C++、、Visual Basic F#、)

コンソールプロジェクトのデバッグの準備は、Windows プロジェクトのデバッグの準備と似ています。コマンドライン引数の設定や、デバッグのためにアプリを一時停止する方法など、いくつかの考慮事項があります。 詳細については、次を参照してください。 [Windows フォーム アプリケーション](../debugger/debugging-preparation-windows-forms-applications.md)、および[デバッグの準備。 Windows フォーム アプリケーション (.NET)](/previous-versions/visualstudio/visual-studio-2010/sez9z95a(v=vs.100))。 コンソール アプリケーションはどれも類似しているため、このトピックでは次のプロジェクトの種類について説明します。

- C#、Visual Basic、 F#コンソールアプリケーション

- C++ コンソール アプリケーション (.NET)

- C++ コンソール アプリケーション (Win32)

  コンソール アプリケーションは、 **[コンソール]** ウィンドウを使用して、入力を受け付けたり出力メッセージを表示したりします。 **コンソール**ウィンドウに書き込むには、アプリケーションで Debug オブジェクトではなく**console**オブジェクトを使用する必要があります。 ただし、**Visual Studio の出力**ウィンドウに書き込むには、通常どおりに Debug オブジェクトを使用します。 アプリケーションの書き込み先を理解し、間違った場所でメッセージを探すことのないようにしてください。 詳細については、「[Console クラス](/dotnet/api/system.console)」、「[Debug クラス](/dotnet/api/system.diagnostics.debug)」、「[[出力] ウィンドウ](../ide/reference/output-window.md)」を参照してください。

## <a name="set-command-line-arguments"></a>コマンドライン引数の設定

コンソール アプリケーションのコマンド ライン引数を指定する必要がある場合があります。 詳細については、次を参照してください[C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)、 [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)、または[c# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)。

すべてのプロジェクト プロパティと同様に、これらの引数はデバッグ セッション間および Visual Studio セッション間で保持されます。 このため、対象のコンソール アプリケーションを以前にデバッグしたことがある場合は、前回のセッションで **[\<プロジェクト名> プロパティ ページ]** ダイアログ ボックスに入力した引数が存在する場合があります。

## <a name="start-the-application"></a>アプリケーションの起動

 いくつかのコンソール アプリケーションが起動すると、それらのアプリケーションは最後まで実行されてから終了します。 この動作のため、実行を中断してデバッグする時間が十分ない場合があります。 アプリケーションをデバッグできるようにするには、次のいずれかの手順に従ってアプリケーションを起動します。

- コードにブレークポイントを設定し、アプリケーションを開始します。

- **F10** (**デバッグ** > **ステップオーバー**) または**F11** (**デバッグ** > **ステップイン**) を使用してアプリケーションを起動し、 **[実行]** などの他のオプションを使用してコード内を移動します。

- コードエディターで、行を右クリックし、[カーソル行の前**まで実行**] をクリックします。

  コンソール アプリケーションをデバッグする場合、Visual Studio からではなく、コマンド プロンプトからアプリケーションを起動することもできます。 その場合は、コマンド プロンプトからアプリケーションを起動し、Visual Studio デバッガーをアプリケーションにアタッチします。 詳細については、「[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)」を参照してください。

  Visual Studio からコンソール アプリケーションを起動すると、 **[コンソール]** ウィンドウが Visual Studio ウィンドウの背後に表示される場合があります。 Visual Studio からコンソール アプリケーションを起動しようとしても、何も起こらない場合は、Visual Studio ウィンドウを移動してみてください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [プロジェクトのデバッグC++の準備](../debugger/debugging-preparation-visual-cpp-project-types.md)
- [C#、F#、および Visual Basic のプロジェクト](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)