---
title: C# または VB プロジェクトをリモート デバッグする |マイクロソフトドキュメント
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
ms.openlocfilehash: 5f147acae956ad380c6e85984de29d5316394c0a
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301075"
---
# <a name="remote-debugging-a-c-or-visual-basic-project-in-visual-studio"></a>C# プロジェクトまたは Visual Basic プロジェクトのリモート デバッグ
別のコンピューターに配置されている Visual Studio アプリケーションをデバッグするには、アプリを展開したコンピューターにリモート ツールをインストールして実行し、Visual Studio からリモート コンピューターに接続するようにプロジェクトを構成し、アプリを実行します。

![リモート デバッガー コンポーネント](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

ユニバーサル Windows アプリ (UWP) のリモート デバッグの詳細については、「[インストールされているアプリ パッケージのデバッグ](debug-installed-app-package.md)」を参照してください。

## <a name="requirements"></a>必要条件

リモート デバッガーは、Windows Server 2008 サービス パック 2 以降の Windows 7 以降 (電話ではない) および Windows Server のバージョンでサポートされています。 要件の完全なリストについては、[要件](../debugger/remote-debugging.md#requirements_msvsmon)を参照してください。

> [!NOTE]
> プロキシ経由で接続された 2 台のコンピュータ間のデバッグはサポートされていません。 ダイヤルアップ インターネットやインターネット経由など、遅延が長い接続や帯域幅の低い接続を介したデバッグは推奨されず、失敗したり、許容できないほど遅くなる可能性があります。

## <a name="download-and-install-the-remote-tools"></a>リモート ツールのダウンロードおよびインストール

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

> [!TIP]
> シナリオによっては、ファイル共有からリモート デバッガーを実行するのが最も効率的な場合があります。 詳細については、「[ファイル共有からリモート デバッガーを実行する](../debugger/remote-debugging.md#fileshare_msvsmon)」を参照してください。

## <a name="set-up-the-remote-debugger"></a><a name="BKMK_setup"></a>リモート デバッガーを設定する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> リモート デバッガーの認証モードまたはポート番号を変更する、追加のユーザーのアクセス許可を追加する必要がある場合は、[リモート デバッガーの構成を](../debugger/remote-debugging.md#configure_msvsmon)参照してください。

## <a name="remote-debug-the-project"></a><a name="remote_csharp"></a>プロジェクトのリモート デバッグ
デバッガーでは、Visual C# または Visual Basic のデスクトップ アプリケーションをリモート コンピューターに配置できませんが、次のようにリモートからそれらのデスクトップ アプリケーションをデバッグすることはできます。 次の手順では、次の図に示すように **、MJO-DL**という名前のコンピュータでデバッグすることを前提としています。

1. **MyWpf** という名前の WPF プロジェクトを作成します。

2. ブレークポイントをコード内の達しやすい任意の箇所に設定します。

    たとえば、ブレークポイントをボタン ハンドラーに設定できます。 これを行うには、MainWindow.xaml を開き、ツールボックスからボタン コントロールを追加し、ボタンをダブルクリックしてハンドラーを開きます。

3. ソリューション エクスプローラーでプロジェクトを右クリックし、**[プロパティ]** を選択します。

4. **[プロパティ]** ページで、**[デバッグ]** タブをクリックします。

    ![RemoteDebuggerCSharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")

5. **[作業ディレクトリ]** テキスト ボックスが空であることを確認してください。

6. [**リモート コンピュータを使用**する] をクリックし、テキスト ボックスに **「あなたのコンピュータ名:ポート」と**入力します。 (ポート番号はリモート デバッガー ウィンドウに表示されます。 ポート番号は、Visual Studio の各バージョンで 2 ずつ増加します)。

    この例では、次のコマンドを使用します。
    ::: moniker range=">=vs-2019"
    **MJO-DL:4024**オン ビジュアル スタジオ 2019
    ::: moniker-end
    ::: moniker range="vs-2017"
    **MJO-DL:4022**オン ビジュアル スタジオ 2017
    ::: moniker-end

7. **[ネイティブ コードのデバッグを有効にする]** がオフであることを確認します。

8. プロジェクトをビルドします。

9. Visual Studio コンピューター上の **Debug** フォルダー (**\<ソース パス>\MyWPF\MyWPF\bin\Debug**) と同じパスのフォルダーをリモート コンピューター上に作成します。

10. 上で作成した実行可能ファイルを、Visual Studio コンピューターから、リモート コンピューター上の新しく作成したフォルダーにコピーします。

    > [!CAUTION]
    > コードを変更したり、再構築したりしないでください (または、この手順を繰り返す必要があります)。 リモート コンピューターにコピーした実行可能ファイルは、ローカルのソースとシンボルに正確に一致している必要があります。

    プロジェクトを手動でコピーしたり、Xcopy、Robocopy、Powershell などのオプションを使用することができます。

11. リモート デバッガーがターゲット コンピューターで実行されていることを確認します (ない場合は、[**スタート]** メニューで**リモート デバッガー**を検索します)。 リモート デバッガー ウィンドウは、次のようになります。

     ![リモート デバッガーのウィンドウ](../debugger/media/remotedebuggerwindow.png "リモート デバッガーのウィンドウ")

12. Visual Studio でデバッグを開始します (**[デバッグ] > [デバッグの開始]**、または **F5** キー)。

13. プロンプトが表示されたら、リモート コンピューターに接続するためのネットワーク資格情報を入力します。

     必要な資格情報は、ネットワークのセキュリティ構成によって異なります。 たとえば、ドメイン コンピュータでは、ドメイン名とパスワードを入力できます。 ドメイン以外のマシンでは、マシン名と有効なユーザー アカウント名<strong>MJO-DL\name@something.com</strong>を入力できます。

     WPF アプリケーションのメイン ウィンドウがリモート コンピューター上で開いていることを確認できるはずです。

14. 必要に応じて、ブレークポイントにヒットするアクションを実行します。 ブレークポイントがアクティブになっていることを確認できるはずです。 ブレークポイントがアクティブでない場合、アプリケーションのシンボルが読み込まれていません。 再試行し、それがうまくいかない場合は、シンボルの読み込み方法と、[シンボル ファイルと Visual Studio のシンボル設定について で](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)トラブルシューティングする方法に関する情報を取得します。

15. Visual Studio コンピューターで、実行がブレークポイントで停止したことを確認できるはずです。

    アプリケーションで使用する必要があるコード以外のファイルがある場合は、Visual Studio プロジェクトに含める必要があります。 追加ファイルのプロジェクト フォルダを作成します (**ソリューション エクスプローラ**で[**新しいフォルダの追加 ] を**クリック> 。 次にファイルをそのフォルダーに追加します (**ソリューション エクスプローラー**で、**[追加] > [既存の項目]** の順にクリックしてからファイルを選択します)。 ファイルごとの **[プロパティ]** ページで、**[出力ディレクトリにコピー]** を **[常にコピーする]** に設定します。

## <a name="set-up-debugging-with-remote-symbols"></a>リモート シンボルを使用したデバッグのセットアップ

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>関連項目
- [Visual Studio でのデバッグ](../debugger/index.yml)
- [まずデバッガを見てください](../debugger/debugger-feature-tour.md)
- [リモート デバッグ用に Windows ファイアウォールを構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
- [リモートの IIS コンピューター上の ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)