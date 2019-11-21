---
title: リモートデバッガーのポート割り当て |Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.topic: reference
ms.assetid: 238bb4ec-bb00-4c2b-986e-18ac278f3959
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2d99a1aff2c241e81e8914a247d2f6d8981ee273
ms.sourcegitcommit: 9c7d8693108ecd2042a70c04cebe3c44af657baf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74239457"
---
# <a name="remote-debugger-port-assignments"></a>リモート デバッガーのポートの割り当て
Visual Studio リモート デバッガーは、アプリケーションまたはバック グラウンド サービスとして実行できます。 アプリケーションとして実行される際には、次のように既定で割り当てられているポートを使用します。
::: moniker range=">=vs-2019"
- Visual Studio 2019: 4024
::: moniker-end
- Visual Studio 2017: 4022

- Visual Studio 2015: 4020

- Visual Studio 2013: 4018

- Visual Studio 2012: 4016

つまり、リモート デバッガーに割り当てられるポート番号はリリースごとに 2 つずつ増えます。 別の任意のポート番号を設定することができます。 ポート番号の設定方法は、後のセクションで説明します。

## <a name="the-remote-debugger-port-on-32-bit-operating-systems"></a>32 ビット オペレーティング システムのリモート デバッガーのポート

::: moniker range=">=vs-2019"
 TCP 4024 (Visual Studio 2019 の場合) がメイン ポートであり、すべてのシナリオにこれが必要です。 これは、コマンド ラインまたはリモート デバッガー ウィンドウのいずれかから構成できます。
::: moniker-end
::: moniker range="vs-2017"
 TCP 4022 (Visual Studio 2017 の場合) がメイン ポートであり、すべてのシナリオにこれが必要です。 これは、コマンド ラインまたはリモート デバッガー ウィンドウのいずれかから構成できます。
::: moniker-end

 リモート デバッガー ウィンドウでは、 **[ツール] > [オプション]** の順にクリックし、TCP/IP ポート番号を設定します。

 コマンド ラインでは、 **/port** スイッチを使用して「**msvsmon /port \<ポート番号>** 」と入力して、リモート デバッガーを開始します。

 リモート デバッグのヘルプに、リモート デバッガーのすべてのコマンド ライン スイッチが記載されています (リモート デバッガー ウィンドウで **F1** キーを押すか、または **[ヘルプ] > [使い方]** の順にクリックします)。

## <a name="the-remote-debugger-port-on-64-bit-operating-systems"></a>64 ビット オペレーティング システムのリモート デバッガーのポート
::: moniker range=">=vs-2019"
 リモートデバッガーの64ビットバージョンが起動すると、既定でメインポート (4024) が使用されます。  32ビットプロセスをデバッグする場合、リモートデバッガーの64ビットバージョンは、リモートデバッガーの32ビットバージョンをポート4025で開始します (メインポート番号は1ずつ増加します)。 32 ビットのリモート デバッガーを実行する場合は、4024 が使用され、4025 は使用されません。
::: moniker-end
::: moniker range="vs-2017"
 リモートデバッガーの64ビットバージョンが起動すると、既定でメインポート (4022) が使用されます。  32ビットプロセスをデバッグする場合、リモートデバッガーの64ビットバージョンは、リモートデバッガーの32ビットバージョンをポート4023で開始します (メインポート番号は1ずつ増加します)。 32 ビットのリモート デバッガーを実行する場合は、4022 が使用され、4023 は使用されません。
:::moniker-end

 このポートは、次のように入力して、コマンド ラインから構成できます: **Msvsmon /wow64port \<ポート番号>** 。

## <a name="the-discovery-port"></a>検出ポート
 実行中のリモート デバッガーのインスタンスをネットワークで検出するには (たとえば、 **[プロセスにアタッチ]** ダイアログの **[検索]** ダイアログ)、UDP 3702 が使用されます。 これが使用されるのは、リモート デバッガーを実行しているコンピューターを検出する場合だけです。つまり、ターゲット コンピューターのコンピューター名または IP アドレスが他の方法でわかれば省略できます。 これは検出用の標準ポートなので、ポート番号を構成することはできません。

 検出を有効にしない場合は、コマンド ラインから検出を無効にして msvsmon を開始できます。次のように入力します。  **Msvsmon /nodiscovery**

## <a name="remote-debugger-ports-on-azure"></a>Azure でのリモート デバッガーのポート
 Azure のリモート デバッガーでは次のポートが使用されます。 クラウド サービス上のポートは、個々の VM 上のポートにマップされます。 すべてのポートは TCP です。

|接続|クラウド サービス上のポート|VM 上のポート|
|-|-|-|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector|30400|30398|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Forwarder|31400|31398|
|Windowsazure.servicebus を Forwarderx86 します。|31401|31399|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.FileUpload|32400|32398|

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)
