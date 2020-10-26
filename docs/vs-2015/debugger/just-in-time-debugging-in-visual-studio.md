---
title: Just-In-Time デバッグ
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
- CSharp
- VB
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
ms.assetid: 14972d5f-69bc-479b-9529-03b8787b118f
caps.latest.revision: 51
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ad2814dffa75809a318dc7cebe7831b5ecec7d29
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690606"
---
# <a name="just-in-time-debugging-in-visual-studio"></a>Just-In-Time Debugging in Visual Studio (Visual Studio での Just-In-Time デバッグ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Just-in-time デバッグは、Visual Studio の外部で実行されているアプリケーションで例外またはクラッシュが発生した場合に、Visual Studio を自動的に起動します。 これにより、Visual Studio が実行されていないときにアプリケーションをテストし、問題が発生したときに Visual Studio でのデバッグを開始できます。

Just-In-Time デバッグは、Windows デスクトップ アプリで使用できます。 Windows ユニバーサルアプリでは機能しません。ビジュアライザーなどのネイティブアプリケーションでホストされているマネージコードでは機能しません。

## <a name="did-the-just-in-time-debugger-dialog-box-appear-when-trying-to-run-an-app"></a><a name="BKMK_Scenario"></a> アプリを実行しようとすると、[Just-in-time デバッガー] ダイアログボックスが表示されますか?

[Visual Studio Just-in-time デバッガー] ダイアログボックスが表示されたときに実行する操作は、実行しようとしている操作によって異なります。

#### <a name="if-you-want-to-get-rid-of-the-dialog-box-and-just-run-the-app-normally"></a>ダイアログボックスを削除して、アプリを通常どおり実行する場合

1. (上級ユーザー)Visual Studio がインストールされている (または、以前にインストールして削除した) 場合は、 [just-in-time デバッグを無効](#BKMK_Enabling) にし、アプリをもう一度実行してみてください。

2. Internet Explorer で web アプリを実行している場合は、スクリプトのデバッグを無効にします。

    [インターネットオプション] ダイアログボックスで、スクリプトのデバッグを無効にします。 これには、**コントロールパネル**  /  の [**ネットワークと**インターネット] のオプションからアクセスでき  /  **Internet Options**ます (正確な手順は、Windows および internet Explorer のバージョンによって異なります)。

    ![JITInternetOptions](../debugger/media/jitinternetoptions.png "JITInternetOptions")

3. エラーが検出された web ページを再度開きます。 これで問題が解決しない場合は、web アプリの所有者に連絡して問題を解決してください。

4. 別の種類の Windows アプリを実行している場合は、アプリの所有者に連絡してエラーを修正し、修正されたバージョンのアプリを再インストールする必要があります。

#### <a name="if-you-want-to-fix-or-debug-the-error-advanced-users"></a>エラーを修正またはデバッグする場合 (上級ユーザー)

- エラーに関する詳細情報を表示し、デバッグを試行するには、 [Visual Studio がインストールされ](https://visualstudio.microsoft.com/vs/older-downloads/) ている必要があります。 詳細については、「 [JIT の使用](#BKMK_Using_JIT) 」を参照してください。 エラーを解決してアプリを修正できない場合は、アプリの所有者に連絡してエラーを解決してください。

## <a name="enable-or-disable-just-in-time-debugging"></a><a name="BKMK_Enabling"></a> Just-in-time デバッグを有効または無効にする
 Just-in-time デバッグを有効または無効にするには、Visual Studio の [ツール] の [ **オプション** ] ダイアログボックスを使用します。

#### <a name="to-enable-or-disable-just-in-time-debugging"></a>Just-In-Time デバッグの有効/無効を切り替えるには

1. Visual Studio を開きます。 **[ツール]** メニューの **[オプション]** をクリックします。

2. [ **オプション** ] ダイアログボックスで、[ **デバッグ** ] フォルダーを選択します。

3. [ **デバッグ** ] フォルダーで、[ **just-in-time** ] ページを選択します。

4. [ **これらの種類のコードの just-in-time デバッグを有効にする** ] ボックスで、関連するプログラムの種類 ([ **マネージ**]、[ **ネイティブ**]、または [ **スクリプト**]) をオンまたはオフにします。

    Just-In-Time デバッグを有効にした後で無効に切り替えるには、管理者特権で実行する必要があります。 Just-In-Time デバッグを有効にするとレジストリ キーが設定され、そのキーを変更するには管理者特権が必要になります。

5. **[OK]** をクリックします。

   Visual Studio がコンピューターからアンインストールされた後でも、Just-In-Time デバッグが有効になっている場合があります。 Visual Studio がインストールされていない場合は、Visual Studio の [ **オプション** ] ダイアログボックスから just-in-time デバッグを無効にすることはできません。 その場合は、Windows レジストリを編集して Just-In-Time デバッグを無効にできます。

#### <a name="to-disable-just-in-time-debugging-by-editing-the-registry"></a>レジストリを編集して Just-In-Time デバッグを無効にするには

1. [ **スタート** ] メニューで、を検索して実行します。 `regedit.exe`

2. **レジストリエディター**ウィンドウで、次のレジストリエントリを見つけて削除します。

    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger

    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\DbgManagedDebugger

3. コンピューターで64ビットのオペレーティングシステムが実行されている場合は、次のレジストリエントリも削除します。

    - HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger

    - HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\DbgManagedDebugger

4. 誤って他のレジストリ キーを削除または変更しないように注意してください。

5. **[レジストリ エディター]** ウィンドウを閉じます。

> [!NOTE]
> サーバー側アプリの Just-in-time デバッグを無効にしようとしても、これらの手順で問題が解決しない場合は、IIS アプリケーション設定でサーバー側のデバッグを無効にして、再試行してください。

#### <a name="to-enable-just-in-time-debugging-of-a-windows-form"></a>Windows フォームの Just-In-Time デバッグを有効化するには

1. 既定では、Windows フォーム アプリケーションには、プログラムが正常な状態に戻れば続行できるように、トップ レベルの例外ハンドラーが用意されています。 たとえば、Windows フォームアプリケーションがハンドルされない例外をスローした場合、次のようなダイアログが表示されます。

     ![WindowsFormsUnhandledException](../debugger/media/windowsformsunhandledexception.png "WindowsFormsUnhandledException")

     Windows フォームアプリケーションの Just-in-time デバッグを有効にするには、次の追加手順を実行する必要があります。

2. `jitDebugging` `true` `system.windows.form` machine.config または.exe.config ファイルのセクションで、値をに設定し *\<application name>* ます。

    ```
    <configuration>
        <system.windows.forms jitDebugging="true" />
    </configuration>
    ```

3. さらに、C++ Windows フォーム アプリケーションでは、.config ファイルまたはコード内で `DebuggableAttribute` も設定する必要があります。 [/Zi](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8) を使用し、[/Og](https://msdn.microsoft.com/library/d10630cc-b9cf-4e97-bde3-8d7ee79e9435) は使用しないでコンパイルすると、コンパイラによってこの属性が設定されます。 ただし、最適化されていないリリース ビルドをデバッグする場合は、この属性を自分で設定する必要があります。 そのためには、アプリケーションの AssemblyInfo.cpp ファイルに次の行を追加します。

    ```
    [assembly:System::Diagnostics::DebuggableAttribute(true, true)];
    ```

     詳細については、「<xref:System.Diagnostics.DebuggableAttribute>」を参照してください。

## <a name="a-namebkmk_using_jituse-just-in-time-debugging"></a><a name="BKMK_Using_JIT">Just-in-time デバッグを使用する
 このセクションでは、実行可能ファイルが例外をスローした場合の処理について説明します。

 これらのステップを実行するには、Visual Studio をインストールする必要があります。 Visual Studio をお持ちでない場合は、無料の [Visual studio 2015 Community Edition](https://visualstudio.microsoft.com/vs/older-downloads/)をダウンロードできます。

 Visual Studio をインストールすると、Just-In-Time デバッグは既定で有効になります。

 このセクションでは、Visual Studio でをスローする C# コンソールアプリを作成 <xref:System.NullReferenceException> します。

 Visual Studio で、 **ThrowsNullException**という名前の C# コンソールアプリ ([ファイル]、[新規]、[プロジェクト]、[Visual C#]、[**コンソールアプリケーション**]) を作成します。 Visual Studio でのプロジェクトの作成の詳細については、「 [チュートリアル: 簡単なアプリケーションの作成](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md)」を参照してください。

 プロジェクトが Visual Studio で開いたら、Program.cs ファイルを開きます。 Main() メソッドを次のコードで置き換えます。これは、行をコンソールに出力して、NullReferenceException をスローします。

```csharp
static void Main(string[] args)
{
    Console.WriteLine("we will now throw a NullReferenceException");
    throw new NullReferenceException("this is the exception thrown by the console app");
}
```

> [!IMPORTANT]
> この手順を [リリース構成](../debugger/how-to-set-debug-and-release-configurations.md)で使用するには、 [マイコードのみ](../debugger/just-my-code.md)をオフにする必要があります。 Visual Studio で、[ **ツール**]、[オプション] の順にクリックします。 [ **オプション** ] ダイアログボックスで、[ **デバッグ**] を選択します。 [ **Enable マイコードのみ**] からチェックを削除します。

 ソリューションをビルドします (Visual Studio で、[ **ソリューションのビルド/リビルド**] を選択します)。 デバッグ構成またはリリース構成のいずれかを選択できます。 ビルド構成の詳細については、「 [ビルド構成](../ide/understanding-build-configurations.md)について」を参照してください。

 ビルドプロセスでは、ThrowsNullException.exe 実行可能ファイルが作成されます。 C# プロジェクトを作成したフォルダーの下に、 **. ..\ThrowsNullException\ThrowsNullException\bin\Debug** または **. ..\ThrowsNullException\ThrowsNullException\bin\Release**というファイルがあります。

 ThrowsNullException.exe をダブルクリックします。 次のようなコマンドウィンドウが表示できます。

 ![ThrowsNullExceptionConsole](../debugger/media/throwsnullexceptionconsole.png "ThrowsNullExceptionConsole")

 数秒後に、エラーウィンドウが表示されます。

 ![ThrowsNullExceptionError](../debugger/media/throwsnullexceptionerror.png "ThrowsNullExceptionError")

 [ **キャンセル**] をクリックしないでください。 数秒後に、[ **デバッグ** ] と [ **プログラムの終了**] の2つのボタンが表示されます。 [ **デバッグ**] をクリックします。

> [!CAUTION]
> アプリケーションに信頼できないコードが含まれている場合は、セキュリティ警告のダイアログボックスが表示されます。 このダイアログ ボックスでは、デバッグを開始するかどうかを選択できます。 デバッグを開始する前に、コードを信頼できるかどうかを判断します。 このコードは、自分で作成したコードですか。 このコードの作成者は信頼できますか。 アプリケーションをリモート コンピューター上で実行している場合、プロセスの名前を識別できますか。 アプリケーションをローカルに実行している場合でも、それが必ずしもコードを信頼できることにはなりません。 コンピューターで悪意のあるコードが実行される可能性を考慮してください。 デバッグしようとしているコードが信頼できると判断した場合は、[ **デバッグ**] をクリックします。 それ以外の場合は、[ **デバッグしない**] をクリックします。

 [ **Visual Studio Just-in-time デバッガー** ] ウィンドウが表示されます。

 ![JustInTimeDialog](../debugger/media/justintimedialog.png "JustInTimeDialog")

 [ **可能なデバッガー**] で、 **Microsoft Visual Studio 2015 行の新しいインスタンス** が選択されていることを確認します。 まだ選択されていない場合は、ここで選択します。

 ウィンドウの下部にある [選択し **たデバッガーを使用してデバッグしますか?**] で、[ **はい**] をクリックします。

 ThrowsNullException プロジェクトが Visual Studio の新しいインスタンスで開き、例外をスローする行で実行が停止します。

 ![NullReferenceSecondInstance](../debugger/media/nullreferencesecondinstance.png "NullReferenceSecondInstance")

 この時点でデバッグを開始できます。 これが実際のアプリケーションである場合は、コードが例外をスローしている理由を確認する必要があります。

## <a name="just-in-time-debugging-errors"></a>Just-In-Time デバッグのエラー
 プログラムがクラッシュしたときにダイアログが表示されない場合は、コンピューターの設定が Windows エラー報告ことが原因である可能性があります。 詳細については、「」を参照してください [。WER の設定](https://msdn.microsoft.com/library/windows/desktop/bb513638\(v=vs.85\).aspx)。

 Just-In-Time デバッグに関連して次のエラー メッセージが表示されることがあります。

- **クラッシュ プロセスにアタッチできません。指定されたプログラムは、Windows または MS-DOS プログラムではありません。**

     このエラーは、別のユーザーとして実行されているプロセスにアタッチしようとしたときに発生します。

     この問題を回避するには、Visual Studio を起動し、[**デバッグ**] メニューの [**プロセスにアタッチ**] ダイアログボックスを開いて、[**選択可能なプロセス**] ボックスの一覧でデバッグするプロセスを見つけます。 プロセスの名前がわからない場合は、 **Visual Studio の Just-in-time デバッガー** ダイアログで、プロセス ID を確認します。 [選択 **可能なプロセス** ] ボックスの一覧でプロセスを選択し、[ **アタッチ**] をクリックします。 [ **Visual Studio Just-in-time デバッガー** ] ダイアログボックスで、[ **いいえ** ] をクリックしてダイアログボックスを閉じます。

- **ログオンしているユーザーがいないため、デバッガーを開始できませんでした。**

     このエラーは、コンソールにログオンしているユーザーがいないコンピューターで Just-In-Time デバッグが Visual Studio を起動しようとしたときに発生します。 ログオンしているユーザーがいないため、[Just-In-Time デバッグ] ダイアログ ボックスを表示するためのユーザー セッションがありません。

     この問題を解決するには、コンピューターにログオンします。

- **クラスは登録されていません。**

     このエラーは、おそらくインストールの問題が原因で登録されていない COM クラスをデバッガーが作成しようとしたことを示します。

     この問題を解決するには、セットアップ ディスクを使って Visual Studio を再インストールするか、既存のインストールを修復します。

## <a name="see-also"></a>参照
 [デバッガーセキュリティ](../debugger/debugger-security.md)[デバッガーの基本](../debugger/debugger-basics.md)[ジャストインタイム、デバッグ、オプションダイアログボックス](../debugger/just-in-time-debugging-options-dialog-box.md)の[セキュリティ警告: 信頼されていないユーザーが所有するプロセスへのアタッチは危険な場合があります。次の情報が疑わしいと思われる場合や、不明な場合は、このプロセスにアタッチしないでください](/visualstudio/debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user?view=vs-2015)。
