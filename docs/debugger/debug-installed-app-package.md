---
title: インストールされた UWP アプリ パッケージをデバッグする | Microsoft Docs
ms.custom: ''
ms.date: 11/07/2018
ms.topic: how-to
f1_keywords:
- vs.debug.installedapppackagelauncher
- vs.debug.remote.connection
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- app package, debug
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: eabc694665bede7d193a360a01c42366568e33c5
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350733"
---
# <a name="debug-an-installed-uwp-app-package-in-visual-studio"></a>Visual Studio でインストールされた UWP アプリ パッケージをデバッグする

Visual Studio は Windows 10 コンピューターと Xbox、HoloLens、IoT デバイスにインストールされたユニバーサル Windows プラットフォーム (UWP) アプリ パッケージをデバッグすることができます。

>[!NOTE]
>インストールされた UWP アプリの Visual Studio でのデバッグはスマートフォンではサポートされていません。

UWP アプリのデバッグの詳細については、[インストールされているアプリ パッケージのデバッグ](https://devblogs.microsoft.com/devops/updates-for-debugging-installed-app-packages-in-visual-studio-2015-update-2/)と[ユニバーサル Windows アプリ (UWP) のビルド](https://devblogs.microsoft.com/visualstudio/universal-windows-apps-targeting-windows-10-anniversary-sdk/)に関するブログ記事を参照してください。

## <a name="debug-an-installed-uwp-app-on-a-local-machine"></a>ローカル コンピューターにインストールされている UWP アプリをデバッグする

1. Visual Studio で、 **[デバッグ]**  >  **[その他のデバッグ ターゲット]**  >  **[インストールされているアプリ パッケージのデバッグ]** の順に選択します。

1. **[インストールされているアプリ パッケージのデバッグ]** ダイアログの **[接続の種類]** で、 **[ローカル コンピューター]** を選択します。

1. **[インストールされているアプリ パッケージ]** で、デバッグするアプリを選択するか、検索ボックスにその名前を入力します。 インストール済みで実行されていないアプリ パッケージは、 **[実行されていません]** の下に表示され、実行中のアプリは **[実行中]** の下にあります。

   ![DebugInstalledAppPackage](../debugger/media/debug-installed-app-pkg.png "DebugInstalledAppPackage")

1. 必要に応じて、 **[このコードの種類をデバッグ]** でコードの種類を変更し、その他のオプションを選択します。
   - アプリの起動時にデバッグを開始するには、 **[Do not launch, but debug my code when it starts]\(起動しない。ただし起動時にはコードをデバッグする\)** を選択します。 アプリの起動時にデバッグを開始する方法は、カスタム パラメーターを使用したプロトコルのアクティベーションなど、[さまざまな起動方法](/windows/uwp/xbox-apps/automate-launching-uwp-apps)から制御パスをデバッグする場合に効果的です。

1. **[開始]** を選択するか、アプリが実行されている場合は **[アタッチ]** を選択します。

> [!NOTE]
> Visual Studio で **[デバッグ]** ** > [プロセスにアタッチ]** を選択して、実行中の UWP またはその他のアプリ プロセスにアタッチすることもできます。 実行中のプロセスにアタッチするために元の Visual Studio プロジェクトは必要ありませんが、アプリのシンボルを読み込むことは、元のコードがないプロセスをデバッグする際に、非常に役立ちます。 [デバッガーでのシンボル ファイルとソース ファイルの指定](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)に関する記事を参照してください。

## <a name="debug-an-installed-uwp-app-on-a-remote-computer-or-device"></a><a name="remote"></a> リモート コンピューターまたはリモート デバイスでインストールされている UWP アプリをデバッグする

Windows 10 デバイスまたは Creators Update 後のリモートの Windows 10 コンピューターにインストールされている UWP アプリが Visual Studio で初めてデバッグすると、ターゲット デバイスにリモート デバッグ ツールがインストールされます。

1. Visual Studio コンピューターとリモート デバイスまたはコンピューターの両方で、[開発者モードを有効にします](/windows/uwp/get-started/enable-your-device-for-development)。

1. Creators Update 前の Windows 10 を実行しているリモート コンピューターに接続している場合は、リモート コンピューターで[リモート デバッガーを手動でインストールし、起動します](../debugger/remote-debugging.md)。

1. Visual Studio コンピューターで、 **[デバッグ]**  >  **[その他のデバッグ ターゲット]**  >  **[インストールされているアプリ パッケージのデバッグ]** の順に選択します。

1. **[インストールされているアプリ パッケージのデバッグ]** ダイアログの **[接続の種類]** で、 **[リモート コンピューター]** または **[デバイス]** を選択します。

   **[デバイス]** を選択した場合は、コンピューターが Windows 10 デバイスに物理的に接続されている必要があります。

   リモート コンピューターで、 **[アドレス]** の横にコンピューター アドレスが表示されない場合は、 **[変更]** を選択します。

   1. **[リモート接続]** ダイアログ ボックスの **[アドレス]** の横に、接続先のコンピューターの名前または IP アドレスを入力します。

      ![ChooseRemoteComputer](../debugger/media/debug-remote-app-pkg.png "ChooseRemoteComputer")

      デバッガーがコンピューター名を使用してリモート コンピューターに接続できない場合は、代わりに IP アドレスを使用します。 Xbox、HoloLens、または IoT デバイスの IP アドレスを使用します。
   1. **[認証モード]** の横にある認証オプションを選択します。

      ほとんどのアプリでは、既定値の **[ユニバーサル (暗号化されていないプロトコル)]** をそのまま使用します。
   1. **[選択]** を選択します。

1. **[インストールされているアプリ パッケージ]** で、デバッグするアプリを選択するか、検索ボックスにその名前を入力します。 インストール済みで実行されていないアプリ パッケージは、 **[実行されていません]** の下に表示され、実行中のアプリは **[実行中]** の下にあります。

1. 必要に応じて、 **[このコードの種類をデバッグ]** でコードの種類を変更し、その他のオプションを選択します。
   - アプリの起動時にデバッグを開始するには、 **[Do not launch, but debug my code when it starts]\(起動しない。ただし起動時にはコードをデバッグする\)** を選択します。 アプリの起動時にデバッグを開始する方法は、カスタム パラメーターを使用したプロトコルのアクティベーションなど、[さまざまな起動方法](/windows/uwp/xbox-apps/automate-launching-uwp-apps)から制御パスをデバッグする場合に効果的です。

1. **[開始]** を選択するか、アプリが実行されている場合は **[アタッチ]** を選択します。

接続されている Xbox、HoloLens、または IoT デバイスにインストールされているアプリ パッケージのデバッグを初めて開始すると、Visual Studio によってターゲット デバイスの正しいバージョンのリモート デバッガーがインストールされます。 リモート デバッガーのインストールには時間がかかることがあります。その間、 **[リモート デバッガーを開始しています]** のメッセージが表示されます。

>[!NOTE]
>現時点では、Xbox または HoloLens デバイスはデバッガーがアタッチされた状態でアプリを再起動します (既に実行されていた場合)。

UWP アプリのリモート展開の詳細については、[UWP アプリの展開とデバッグ](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)に関する記事と、「[リモート コンピューター上の UWP アプリのデバッグ](run-windows-store-apps-on-a-remote-machine.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [リモート デバッグ](../debugger/remote-debugging.md)
- [Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)