---
title: C# または VB プロジェクトをリモート デバッグする | Microsoft Docs
description: ステップ バイ ステップの手順に従って、リモート コンピューターから Visual Studio C# または Visual Basic アプリケーションをデバッグする方法を学習します。
ms.custom:
- remotedebugging"=
- seodec18
ms.date: 08/14/2018
ms.topic: conceptual
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: a9753fbb-e7f4-47f0-9dbe-9de90c6c8457
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 76364dd6817774c38daa62463cd5bc635075ba73
ms.sourcegitcommit: 105e7b5a486262bc92939980383ceee068098a11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/30/2020
ms.locfileid: "97815699"
---
# <a name="remote-debugging-a-c-or-visual-basic-project-in-visual-studio"></a>Visual Studio での C# または Visual Basic プロジェクトのリモート デバッグ
別のコンピューターに配置されている Visual Studio アプリケーションをデバッグするには、アプリを配置したコンピューターにリモート ツールをインストールして実行し、Visual Studio からリモート コンピューターに接続するようにプロジェクトを構成してから、アプリを実行します。

![リモート デバッガーのコンポーネント](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

ユニバーサル Windows アプリ (UWP) のリモート デバッグの詳細については、[インストールされているアプリ パッケージのデバッグ](debug-installed-app-package.md)に関するページを参照してください。

## <a name="requirements"></a>必要条件

リモート デバッガーは、Windows 7 以降 (Phone を除く) および Windows Server 2008 Service Pack 2 以降でサポートされています。 詳細な要件の一覧については、「[要件](../debugger/remote-debugging.md#requirements_msvsmon)」を参照してください。

> [!NOTE]
> プロキシ経由で接続された 2 台のコンピューター間のデバッグはサポートされていません。 待機時間の長い接続や低帯域幅の接続 (ダイヤルアップ インターネットなど)、または国をまたぐインターネット経由のデバッグは推奨されません。これらは、障害が発生するか、または過度に低速になる可能性があります。

## <a name="download-and-install-the-remote-tools"></a>リモート ツールのダウンロードおよびインストール

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

> [!TIP]
> 場合によっては、ファイル共有からリモート デバッガーを実行するのが最も効率的な場合があります。 詳細については、[ファイル共有からのリモート デバッガーの実行](../debugger/remote-debugging.md#fileshare_msvsmon)に関するページを参照してください。

## <a name="set-up-the-remote-debugger"></a><a name="BKMK_setup"></a> リモート デバッガーのセットアップ

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 追加のユーザーのアクセス許可を追加し、認証モード、またはリモート デバッガーのポート番号を変更する必要がある場合は、「[リモート デバッガーを構成する](../debugger/remote-debugging.md#configure_msvsmon)」を参照してください。

## <a name="remote-debug-the-project"></a><a name="remote_csharp"></a> プロジェクトをリモート デバッグする
デバッガーでは、Visual C# または Visual Basic のデスクトップ アプリケーションをリモート コンピューターに配置できませんが、次のようにリモートからそれらのデスクトップ アプリケーションをデバッグすることはできます。 以下の手順では、次の図のように、**MJO-DL** という名前のコンピューターでこのようなデスクトップ アプリケーションをデバッグすることを想定しています。

1. **MyWpf** という名前の WPF プロジェクトを作成します。

2. ブレークポイントをコード内の達しやすい任意の箇所に設定します。

    たとえば、ブレークポイントをボタン ハンドラーに設定できます。 これを行うには、MainWindow.xaml を開き、ツールボックスから Button コントロールを追加した後、ボタンをダブルクリックしてそのハンドラーを開きます。

3. ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロパティ]** を選択します。

4. **[プロパティ]** ページで、 **[デバッグ]** タブをクリックします。

    ![Visual Studio ソリューション エクスプローラーのプロパティの [デバッグ] タブのスクリーンショット。 [リモート コンピューターを使用する] プロパティは "MJO-DL:4022" に設定されています。](../debugger/media/remotedebuggercsharp.png)

5. **[作業ディレクトリ]** テキスト ボックスが空であることを確認してください。

6. **[リモート コンピューターを使用する]** をオンにして、テキスト ボックスに「**yourmachinename:port**」と入力します。 (ポート番号がリモート デバッガー ウィンドウに表示されます。 ポート番号は、Visual Studio のバージョンごとに 2 ずつ増分されます)。

    この例では、以下を使用します。
    ::: moniker range=">=vs-2019"
    **MJO-DL:4024** (Visual Studio 2019)
    ::: moniker-end
    ::: moniker range="vs-2017"
    **MJO-DL:4022** (Visual Studio 2017)
    ::: moniker-end

7. **[ネイティブ コードのデバッグを有効にする]** がオフであることを確認します。

8. プロジェクトをビルドします。

9. Visual Studio コンピューター上の **Debug** フォルダー ( **\<source path>\MyWPF\MyWPF\bin\Debug**) と同じパスのフォルダーをリモート コンピューター上に作成します。

10. 上で作成した実行可能ファイルを、Visual Studio コンピューターから、リモート コンピューター上の新しく作成したフォルダーにコピーします。

    > [!CAUTION]
    > コードを変更したり、リビルドを行ったりしないでください (行うと、このステップを繰り返す必要があります)。 リモート コンピューターにコピーした実行可能ファイルは、ローカルのソースとシンボルに正確に一致している必要があります。

    プロジェクトは手動でコピーすることも、Xcopy、Robocopy、PowerShell、その他のオプションを使用することもできます。

11. ターゲット コンピューターでリモート デバッガーが実行されていることを確認します (実行されていない場合は、 **[スタート]** メニューで **リモート デバッガー** を検索します)。 リモート デバッガー ウィンドウは次のような外観です。

     ![[Visual Studio 2017 リモート デバッガー] ウィンドウのスクリーンショット。 デバッガーがターゲット コンピューターで実行されていることを示す 1 つのアクションが一覧表示されています。](../debugger/media/remotedebuggerwindow.png)

12. Visual Studio でデバッグを開始します ( **[デバッグ] > [デバッグの開始]** 、または **F5** キー)。

13. メッセージが表示されたら、リモート コンピューターに接続するためのネットワーク資格情報を入力します。

     必要な資格情報は、ネットワークのセキュリティ構成によって異なります。 たとえば、ドメイン コンピューターでは、ドメイン名とパスワードを入力できます。 ドメイン以外のコンピューターでは、コンピューター名と有効なユーザー アカウント名 (<strong>MJO-DL\name@something.com</strong> など) および正しいパスワードなどを入力します。

     WPF アプリケーションのメイン ウィンドウがリモート コンピューター上で開いていることを確認できるはずです。

14. 必要に応じて、ブレークポイントにヒットするためのアクションを実行します。 ブレークポイントがアクティブになっていることを確認できるはずです。 ブレークポイントがアクティブでない場合、アプリケーションのシンボルが読み込まれていません。 再試行してもうまくいかない場合、シンボルの読み込みと、それらのトラブルシューティング方法については、「[シンボル ファイルおよび Visual Studio のシンボルの設定について](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)」を参照してください。

15. Visual Studio コンピューターで、実行がブレークポイントで停止したことを確認できるはずです。

    アプリケーションで使用する必要がある、コード以外のファイルがある場合は、Visual Studio プロジェクトに含める必要があります。 追加のファイル用のプロジェクト フォルダーを作成します (**ソリューション エクスプローラー** で、 **[追加] > [新しいフォルダー]** をクリックします)。 次にファイルをそのフォルダーに追加します (**ソリューション エクスプローラー** で、 **[追加] > [既存の項目]** の順にクリックしてからファイルを選択します)。 ファイルごとの **[プロパティ]** ページで、 **[出力ディレクトリにコピー]** を **[常にコピーする]** に設定します。

## <a name="set-up-debugging-with-remote-symbols"></a>リモート シンボルを使用したデバッグのセットアップ

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>関連項目
- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
- [リモートの IIS コンピューター上の ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)