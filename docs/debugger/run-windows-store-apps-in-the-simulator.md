---
title: シミュレーターで UWP アプリを実行する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 81b69bf8-ec87-4bb6-9ad4-1fa7b7802d16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 1c208e435e63891c71fe47ebd64c5fe1307e0c82
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85348142"
---
# <a name="run-uwp-apps-in-the-simulator"></a>シミュレーターで UWP アプリを実行する

UWP アプリ用の Visual Studio シミュレーターは、UWP アプリをシミュレートするデスクトップ アプリケーションです。 通常は、ローカル コンピューター、接続されているデバイス、またはリモート コンピューター上でデバッグします。 ただし、シナリオによっては、Visual Studio シミュレーターを使用して、さまざまな物理的な画面サイズと解像度をエミュレートすることをお勧めします。 また、一般的なタッチ イベントとローテーション イベントや、ネットワーク接続プロパティをシミュレートすることもできます。

シミュレーターは、UWP アプリを設計、開発、デバッグ、テストできる環境を提供します。 ただし、Microsoft Store にアプリを発行する前に、実際のデバイスでアプリをテストする必要があります。

UWP アプリ用の Visual Studio シミュレーターは、ローカル コンピューターの分離環境では実行されません。 したがって、シミュレーターで発生したエラー (回復できないシステム エラーなど) がコンピューター全体に影響を与える場合があります。

> [!IMPORTANT]
> Visual Studio 2015 シミュレーターには、位置情報ボタンがありません。 これは、Windows 10 シミュレーターに位置情報シミュレーションが含まれていないためです。

## <a name="set-the-simulator-as-the-target"></a><a name="BKMK_Set_the_simulator_as_the_target"></a> シミュレーターをターゲットとして設定する

UWP アプリをシミュレーターで実行するには、デバッガーの **[標準]** ツール バーの **[デバッグの開始]** ボタンの横にあるドロップダウン リストの **[シミュレーター]** をクリックします。 このオプションは、アプリの **[ターゲット プラットフォームの最小バージョン]** が開発用コンピューターのオペレーティング システムと同じかそれより前である場合にのみ使用できます。

![シミュレーターでの実行](../debugger/media/vsrun_f5_simulator.png "VSRUN_F5_Simulator")

## <a name="choose-an-interaction-mode"></a><a name="BKMK_Choose_an_interaction_mode"></a> 対話モードを選択する

次の対話モードを選択できます。

- ![マウス モード ボタン](../debugger/media/simulator_mousemodebtn.png "SIMULATOR_MouseModeBtn") マウス モード: 対話モードをマウス ジェスチャに設定します。 マウス ジェスチャには、クリック、ダブルクリック、およびドラッグがあります。

- ![タッチ エミュレーション開始ボタン](../debugger/media/simulator_starttouchemulationbtn.png "SIMULATOR_StartTouchEmulationBtn") タッチ エミュレーションを開始: 対話モードを 1 本の指によるタッチ ジェスチャに設定します。 1 本指のイベントには、タップ、ドラッグ、およびスワイプがあります。

   ![シミュレーターの 1 本指のターゲット](../debugger/media/simulator_onefinger.png "SIMULATOR_OneFinger")
   
   シングル ターゲット アイコンは、シミュレーター内のイベントの位置を示します。 ポインターを配置するには、マウスを使用します。

   ![1 本指タッチのターゲット](../debugger/media/simulator_onefingerengaged.png "SIMULATOR_OneFingerEngaged")
   
   タッチ モードをアクティブにするには、マウスの左ボタンを押します。 たとえば、タップをシミュレートする場合はボタンをクリックし、ドラッグまたはスワイプする場合はボタンを長押しします。

## <a name="pinch-and-zoom"></a>ピンチとズーム

対話モードを、2 本の指によるピンチ ジェスチャとズーム ジェスチャに設定します。

![シミュレーターの 2 本指のターゲット](../debugger/media/simulator_twofinger.png)

ダブル ターゲット アイコンは、デバイス画面上の 2 本の指の位置を示します。

- デバイス画面上のオブジェクトの上にアイコンを配置するには、マウスを移動します。

- ピンチまたはズームを実行する前の 2 本の指のシミュレートされる距離を変更するは、マウス ホイールを前方または後方に回転させます。

![ターゲットのピンチ、ズーム、および回転](../debugger/media/simulator_twofingerengaged.png)

- 縮小 (ピンチ) する場合は、左ボタンを押し、ホイールを後方 (手前) に回転させます。

- 拡大 (ズーム) する場合は、左ボタンを押し、マウス ホイールを前方 (奥) に回転させます。

## <a name="object-rotation"></a>オブジェクトの回転

**[タッチ エミュレーションの回転]** ボタンは、対話モードを、2 本の指による回転ジェスチャに設定します。

- デバイス画面上のオブジェクトの上にアイコンを配置するには、マウスを移動します。 オブジェクトの回転を実行する前の 2 本の指のシミュレートされる方向を変更するは、マウス ホイールを前方または後方に回転させます。

- オブジェクトを反時計回りに回転させる場合は、左ボタンを押し、ホイールを後方 (手前) に回転させます。 マウス ホイールを回転させると、回転の相対サイズを示すために、2 つのターゲット アイコンのいずれかが他方のアイコンを中心として回転します。

- オブジェクトを時計回りに回転させる場合は、左ボタンを押し、マウス ホイールを前方 (奥) に回転させます。

## <a name="enable-or-disable-always-on-top-mode"></a><a name="BKMK_Enable_or_disable_Always_on_top_mode"></a> [常に手前に表示] モードを有効または無効にする
 シミュレーター ウィンドウが常に他のウィンドウの上に表示されるように設定できます。 **[最前面に表示するウィンドウの切り替え]** ボタンは、シミュレーター ウィンドウの **[常に手前に表示]** モードを有効または無効にします。

## <a name="change-the-device-orientation"></a><a name="BKMK_Change_the_device_orientation"></a> デバイスの方向を変更する
 シミュレーターを任意の方向に 90 度回転させることで、デバイスの方向を縦長と横長の間で切り替えることができます。

> [!NOTE]
> シミュレーターでは、プロジェクトのプロパティ [DisplayProperties.AutoRotationPreferences](/uwp/api/windows.graphics.display.displayproperties.autorotationpreferences) は考慮されません。 たとえば、プロジェクトで方向が `Landscape`に設定されている場合でも、シミュレーターの方向を回転させて縦向きにすると、シミュレーターに表示されるイメージも回転され、サイズが変更されます。 実際のデバイスでこれらの設定をテストしてください。

> [!NOTE]
> シミュレーターを回転させたときに、シミュレーターの 1 つの辺がシミュレーターを表示している画面よりも大きくなる場合、シミュレーターのサイズは画面に収まるように自動的に変更されます。 シミュレーターは、再度回転させた場合でも、元のサイズに戻ることはありません。

## <a name="change-the-simulated-screen-size-and-resolution"></a><a name="BKMK_Change_the_simulated_screen_size_and_resolution"></a> シミュレートされる画面のサイズと解像度を変更する
 シミュレートされる画面のサイズと解像度を変更するには、パレットの **[解像度の変更]** ボタンをクリックし、一覧から新しいサイズと解像度を選択します。

 画面サイズと解像度は *画面の幅 (インチ)、ピクセル幅 X ピクセル高さ*で一覧表示されます。 画面のサイズと解像度の両方がシミュレートされます。 シミュレーター上の位置座標は、選択したデバイスのサイズと解像度に変換されます。

> [!NOTE]
> ビットマップ イメージのスケーリングされたバージョンをアプリに保存できます。Windows は、現在のスケールで正しいイメージを読み込みます。 詳細については、[設計と UI の概要](/windows/uwp/layout/design-and-ui-intro)に関するページを参照してください。 ただし、Windows によって解像度に合ったイメージが選択されるようにシミュレーターの解像度を変更した場合、新しいイメージを表示するにはデバッグ セッションを停止して再度開始する必要があります。

## <a name="capture-a-screenshot-of-your-app-for-submission-to-microsoft-store"></a><a name="BKMK_Capture_a_screenshot_of_your_app_for_submission_to_the_Microsoft_Store"></a> Microsoft Store に送信するアプリのスクリーンショットをキャプチャする
 Microsoft Store にアプリを送信するときは、アプリのスクリーンショットを含める必要があります。

> [!NOTE]
> スクリーンショットは、シミュレーターの現在の解像度で保存されます。 解像度を変更するには、 **[解像度の変更]** ボタンをクリックします。

- シミュレーターからアプリのスクリーンショットを作成するには、 **[クリップボードにスクリーンショットをキャプチャします]** ボタンをクリックします。

- スクリーンショットの配置場所を設定するには、 **[スクリーンショットの設定]** ボタンをクリックし、ショートカット メニューから場所を選択します。

   ![スクリーンショットの設定のコンテキスト メニュー](../debugger/media/simulator_screenshotsettingscntxmnu.png)

## <a name="simulate-network-connection-properties"></a><a name="BKMK_Simulate_network_connection_properties"></a> ネットワーク接続のプロパティをシミュレートする

アプリケーションのユーザーがネットワーク接続コストやデータ プランの状態の変化を認識し、アプリケーションがその情報を使用して、ローミングや指定されたデータ転送の制限の超過による追加コストの発生を避けることにより、アプリケーションのユーザーが従量制課金接続のコストを管理できるようにします。 [Windows.Networking.Connectivity](/uwp/api/windows.networking.connectivity) API を使用すると、 [NetworkStatusChanged](/uwp/api/windows.networking.connectivity.networkinformation) および署名を行うイベント [TriggerType](/uwp/api/windows.applicationmodel.background.systemtrigger) に応答できます。 例については、「[クイック スタート:従量制課金接続のコスト制約を管理する方法 (HTML)](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)」を参照してください。

ご利用のネットワーク コストを認識するコードをデバッグまたはテストするには、シミュレーターを使って、[GetInternetConnectionProfile](/uwp/api/windows.networking.connectivity.connectionprofile) によって返される [ConnectionProfile](/uwp/api/windows.networking.connectivity.networkinformation)オブジェクトを通じて公開されるネットワークのプロパティを模倣します。

ネットワークのプロパティをシミュレートするには、次のようにします。

1. シミュレーターのツール バーの **[ネットワーク プロパティの変更]** ボタンをクリックします。

2. **[ネットワーク プロパティの設定]** ダイアログ ボックスの **[シミュレートされたネットワーク プロパティの使用]** をクリックします。

    チェック ボックスをオフにしてシミュレーションを削除し、現在接続されているインターフェイスのネットワーク プロパティに戻ります。

3. シミュレートされたネットワークの **[プロファイル名]** を入力します。 [ConnectionProfile](/uwp/api/windows.networking.connectivity.connectionprofile) オブジェクトの [ProfileName](/uwp/api/windows.networking.connectivity.connectionprofile) プロパティでシミュレーションを識別するために使用できる一意の名前を使用することをお勧めします。

4. [[ネットワーク コストの種類]](/uwp/api/windows.networking.connectivity.networkcosttype) の一覧からプロファイルの **NetworkCostType** 値を選択します。

5. **[データの限度の状態フラグ]** の一覧から、[ApproachingDataLimit](/uwp/api/windows.networking.connectivity.connectioncost) プロパティまたは [OverDataLimit](/uwp/api/windows.networking.connectivity.connectioncost) プロパティを true に設定できます。または、 **[データの限度を下回っています]** を選択すると、両方の値を false に設定できます。

6. **[ローミングの状態]** の一覧から、 [Roaming](/uwp/api/windows.networking.connectivity.connectioncost) プロパティを設定します。

7. **[プロパティの設定]** をクリックして、前景の [NetworkStatusChanged](/uwp/api/windows.networking.connectivity.networkinformation) イベントおよび [NetworkStateChange](/uwp/api/windows.applicationmodel.background.systemtrigger) 型の背景の **SystemTrigger**をトリガーして、ネットワーク プロパティをシミュレートします。

ネットワーク接続の管理の詳細については、以下を参照してください。

[クイック スタート:従量制課金接続のコスト制約を管理する方法 (HTML)](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)

[ネットワーク情報のサンプル](https://code.msdn.microsoft.com/windowsapps/Network-Information-Sample-63aaa201)

::: moniker range="vs-2017"
[エネルギー使用の分析](../profiling/analyze-energy-use-in-store-apps.md)
::: moniker-end

[Windows.Networking.Connectivity](/uwp/api/windows.networking.connectivity)

[バックグラウンド タスクでシステム イベントに応答する方法](/previous-versions/windows/apps/hh977058(v=win.10))

[UWP アプリで中断イベント、再開イベント、およびバックグラウンド イベントをトリガーする方法](how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)

## <a name="navigate-the-simulator-with-the-keyboard"></a><a name="BKMK_Navigate_the_simulator_with_the_keyboard"></a> キーボードを使用してシミュレーター内を移動する

**Ctrl + Alt + 上矢印キー**を押してシミュレーター ウィンドウからシミュレーター ツールバーにフォーカスを切り替えて、シミュレーター ツールバーをナビゲートできます。 ツール バーのボタンの間を移動するには、 **上向きの矢印** と **下向きの矢印** を使用します。

シミュレーターを終了するには、 **Ctrl + Alt + F4** キーを押します。

## <a name="see-also"></a>関連項目

- [Visual Studio からアプリを実行](debugging-windows-store-and-windows-universal-apps.md)
