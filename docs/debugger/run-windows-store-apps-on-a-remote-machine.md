---
title: リモート マシンの UWP アプリをデバッグする | Microsoft Docs
description: Visual Studio を使用し、離れた場所にある別のコンピューターまたはデバイス上のユニバーサル Windows プラットフォーム (UWP) アプリを実行、デバッグ、プロファイリング、テストする方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 10/05/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 0f6814d6-cd0d-49f3-b501-dea8c094b8ef
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- uwp
ms.openlocfilehash: f75c1c2420a356a38148f67daab05eadf5a073e6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881322"
---
# <a name="debug-uwp-apps-on-remote-machines-from-visual-studio"></a>リモート マシンの UWP アプリを Visual Studio からデバッグする

Visual Studio を使用して、別のコンピューターまたはデバイス上のユニバーサル Windows プラットフォーム (UWP) アプリを実行、デバッグ、プロファイリング、テストすることができます。 リモート マシンで UWP アプリを実行するのは、Visual Studio コンピューターで、タッチ、地理的位置、物理的な方向などの UWP 固有の機能がサポートされていない場合に特に便利です。

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a> 必要条件

リモート デバイスの UWP アプリを Visual Studio からデバッグするには:

- Visual Studio プロジェクトは、リモート デバッグ用に構成されている必要があります。
- リモート マシンと Visual Studio コンピューターは、ネットワークを介して接続されているか、USB またはイーサネット ケーブルを使って直接接続されている必要があります。 インターネットを介したデバッグはサポートされません。
- Visual Studio コンピューターとリモート マシンの両方で、[開発者モードを有効にする](/windows/uwp/get-started/enable-your-device-for-development)必要があります。
- リモート コンピューターで、Remote Tools for Visual Studio を実行している必要があります。
  - Windows 10 のバージョンによっては、リモート ツールが自動的に起動され、実行されます。 それ以外の場合は、[Remote Tools for Visual Studio をインストールして実行します](#BKMK_download)。
  - Windows Mobile 10 デバイスでは、リモート ツールは必要なく、サポートされていません。

## <a name="configure-a-visual-studio-project-for-remote-debugging"></a><a name="BKMK_ConnectVS"></a> リモート デバッグ用に Visual Studio プロジェクトを構成する
<a name="BKMK_DirectConnect"></a> プロジェクトの **プロパティ** を使用して、接続先のリモート デバイスを指定します。 設定は、プログラミング言語によって異なります。

> [!CAUTION]
> Windows 10 リモート接続の場合、既定では、プロパティ ページの **[認証の種類]** に **[ユニバーサル (暗号化されていないプロトコル)]** が設定されます。 リモート デバッガーに接続するには、場合によって **[認証]** を設定する必要があります。 **[ユニバーサル (暗号化されていないプロトコル)]** および **[認証なし]** プロトコルにはネットワーク セキュリティがないため、開発用コンピューターとリモート マシンの間で受け渡されるデータは脆弱です。 これらの認証の種類は、悪意のあるトラフィックや敵対的なトラフィックのリスクがないことが確実な信頼されるネットワークに対してのみ選択してください。
>
>**[認証の種類]** に **[Windows 認証]** を選択した場合は、デバッグ時にリモート マシンにサインインする必要があります。 リモート デバッガーも、Visual Studio コンピューターと同じユーザー アカウントを使用して **Windows 認証** モードで実行されている必要があります。

### <a name="configure-a-c-or-visual-basic-project-for-remote-debugging"></a><a name="BKMK_Choosing_the_remote_device_for_C__and_Visual_Basic_projects"></a> リモート デバッグ用に C# または Visual Basic プロジェクトを構成する

1. Visual Studio の **ソリューション エクスプローラー** で C# または Visual Basic プロジェクトを選択し、 **[プロパティ]** アイコンを選択して、**Alt**+**Enter** を押すか、右クリックして **[プロパティ]** を選択します。

1. **[デバッグ]** タブを選択します。

1. **[ターゲット デバイス]** で、リモート コンピューターの場合は **[リモート コンピューター]** 、直接接続されている Windows Mobile 10 デバイスの場合は **[デバイス]** を選択します。

1. リモート マシンの場合は、[[リモート接続] ダイアログ ボックス](#remote-connections)で **[リモート コンピューター]** フィールドにネットワーク名または IP アドレスを入力するか、 **[検索]** を選択してデバイスを検索します。

    ![リモート デバッグ用のマネージド プロジェクト プロパティ](../debugger/media/vsrun_managed_projprop_remote.png "マネージド デバッグ プロジェクトのプロパティ")

### <a name="configure-a-c-project-for-remote-debugging"></a><a name="BKMK_Choosing_the_remote_device_for_JavaScript_and_C___projects"></a> リモートデバッグ用に C++ プロジェクトを構成する

1. Visual Studio の **ソリューション エクスプローラー** で C++ プロジェクトを選択し、 **[プロパティ]** アイコンを選択して、**Alt**+**Enter** を押すか、右クリックして **[プロパティ]** を選択します。

1. **[デバッグ]** タブを選択します。

3. **[起動するデバッガー]** で、リモート コンピューターの場合は **[リモート コンピューター]** 、直接接続されている Windows Mobile 10 デバイスの場合は **[デバイス]** を選択します。

1. リモート マシンの場合は、[[リモート接続] ダイアログ ボックス](#remote-connections)で **[コンピューター名]** フィールドにネットワーク名または IP アドレスを入力または選択するか、ドロップダウンして **[検索]** を選択してデバイスを検索します。

    ![リモート デバッグ用の C++ プロジェクト プロパティ](../debugger/media/vsrun_cpp_projprop_remote.png "C++ のデバッグ プロジェクト プロパティ")

### <a name="use-the-remote-connections-dialog-box"></a><a name="remote-connections"></a> [リモート接続] ダイアログ ボックスを使用する

**[リモート接続]** ダイアログ ボックスでは、特定のリモート コンピューター名または IP アドレスを検索したり、最新の情報に更新する丸い矢印のアイコンを選択して接続を自動検出したりすることができます。 このダイアログ ボックスでは、リモート デバッガーを現在実行しているローカル サブネット上のデバイスのみが検索されます。 **[リモート接続]** ダイアログ ボックスですべてのデバイスを検出できるわけではありません。

 ![[リモート接続] ダイアログ ボックス](../debugger/media/vsrun_selectremotedebuggerdlg.png "[リモート接続] ダイアログ")

>[!TIP]
>名前を指定してリモート デバイスに接続できない場合は、IP アドレスを使用してみてください。 IP アドレスを確認するには、リモート デバイスのコマンド ウィンドウに「**ipconfig**」と入力します。 IP アドレスは **IPv4 アドレス** として表示されます。

## <a name="download-and-install-the-remote-tools-for-visual-studio"></a><a name="BKMK_download"></a> Remote Tools for Visual Studio をダウンロードしてインストールする

Visual Studio でリモート コンピューター上のアプリをデバッグするには、リモート コンピューターで Remote Tools for Visual Studio が実行されている必要があります。

- Windows Mobile 10 デバイスでは、リモート ツールは必要なく、サポートもされていません。
- Creators Update (バージョン 1703) 以降を実行している Windows 10 PC、Windows 10 の Xbox、IoT、HoloLens デバイスでアプリを展開するとリモート ツールが自動的にインストールされます。
- Creators Update より前の Windows 10 PC では、デバッグを開始する前に、リモート コンピューターでリモート ツールを手動でダウンロードしてインストールし、実行する必要があります。

**リモート ツールをダウンロードしてインストールするには:**

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="configure-the-remote-tools"></a><a name="BKMK_setup"></a> リモート ツールを構成する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

## <a name="debug-uwp-apps-remotely"></a><a name="BKMK_RunRemoteDebug"></a> UWP アプリをリモートでデバッグする

リモート デバッグはローカル デバッグと同じように動作します。

1. Windows 10 の Creators Update より前のバージョンでは、リモート デバッグ モニター (*msvsmon.ex*) がリモート デバイスで実行されていることを確認してください。

1. Visual Studio コンピューターで、ツールバーの緑色の矢印の横に適切なデバッグ ターゲット ( **[リモート コンピューター]** または **[デバイス]** ) が表示されていることを確認します。

1. デバッグを開始するには、 **[デバッグ]**  >  **[デバッグの開始]** を選択する、**F5** を押す、またはツールバーの緑色の矢印を選択します。

   プロジェクトが再コンパイルされ、リモート デバイスに展開され起動されます。 デバッガーにより、ブレークポイントで実行が中断され、コードをステップ イン、ステップ オーバー、ステップ アウトできます。

1. 必要に応じて、 **[デバッグ]**  >  **[デバッグの停止]** を選択するか、**Shift**+**F5** を押してデバッグを停止し、リモート アプリを閉じます。

## <a name="see-also"></a>関連項目
- [高度なリモート配置オプション](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)
- [Visual Studio での UWP アプリのテスト](../test/unit-test-your-code.md)
- [Visual Studio で UWP アプリを展開する](debugging-windows-store-and-windows-universal-apps.md)
