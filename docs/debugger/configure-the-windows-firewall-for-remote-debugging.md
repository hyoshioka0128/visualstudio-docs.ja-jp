---
title: リモート デバッグ用の Windows ファイアウォールを構成する | Microsoft Docs
description: リモート デバッグ用の Windows ファイアウォールを構成する リモート デバッグ用のポートを構成する リモート デバッグ接続の問題を解決します。
ms.custom: SEO-VS-2020
ms.date: 10/31/2018
ms.topic: how-to
ms.assetid: 66e3230a-d195-4473-bbce-8ca198516014
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 959d015bd23c91ec2ba6215c7a5b42d13b37ee29
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99865827"
---
# <a name="configure-windows-firewall-for-remote-debugging"></a>リモート デバッグ用の Windows ファイアウォールを構成する

Windows ファイアウォールによって保護されているネットワークでは、リモート デバッグを許可するようにファイアウォールを構成する必要があります。 Visual Studio とリモート デバッグ ツールにより、インストール中またはスタートアップ中に適切なファイアウォール ポートを開くことが試みられますが、ポートを開いたり、またはアプリを手動で許可したりすることが必要になる場合もあります。

このトピックでは、Windows 10、8/8.1、7 コンピューター、および Windows Server 2012 R2、2012、2008 R2 コンピューターで、リモート デバッグを有効にするように Windows ファイアウォールを構成する方法について説明します。 Visual Studio コンピューターとリモート コンピューターで、同じオペレーティング システムが実行されている必要はありません。 たとえば Visual Studio コンピューターで Windows 10 を実行し、リモート コンピューターで Windows Server 2012 R2 を実行することができます。

>[!NOTE]
>Windows ファイアウォールを構成する手順は、オペレーティング システムによって多少異なります。また、Windows のバージョンが古い場合も多少異なります。 Windows 8/8.1、Windows 10、Windows Server 2012 の設定では、"*アプリ*" という単語を使用しますが、Windows 7 および Windows Server 2008 では、"*プログラム*" という単語が使用されます。

## <a name="configure-ports-for-remote-debugging"></a>リモート デバッグ用のポートを構成する

Visual Studio とリモート デバッガーは、インストール中またはスタートアップ中に適切なポートを開こうとします。 ただし、サード パーティ製のファイアウォールなど、一部のシナリオでは、ポートを手動で開く必要があります。

**ポートを開く手順:**

1. Windows の **[スタート]** メニューで、**セキュリティが強化された Windows ファイアウォール** を検索して開きます。 Windows 10 では、これは、**セキュリティが強化された Windows Defender ファイアウォール** になります。

1. 新しい受信ポートの場合は、 **[受信規則]** 、 **[新しい規則]** の順に選択します。 送信規則の場合は、代わりに **[送信規則]** を選択します。

1. **新規の受信の規則ウィザード** で、 **[ポート]** を選択し、 **[次へ]** を選択します。

1. 下記の表のポート番号に応じて、 **[TCP]** または **[UDP]** を選択します。

1. **[特定のローカル ポート]** で、下記の表のポート番号を入力し、 **[次へ]** を選択します。

1. **[接続を許可する]** を選択し、 **[次へ]** を選択します。

1. 有効にする 1 つ以上のネットワークの種類 (リモート接続のネットワークの種類など) を選択し、 **[次へ]** を選択します。

1. 規則の名前 (たとえば、**msvsmon**、**IIS**、**Web Deploy** など) を追加し、 **[完了]** を選択します。

   新しい規則が表示され、 **[受信規則]** または **[送信規則]** の一覧で選択されます。

### <a name="ports-on-the-remote-computer-that-enable-remote-debugging"></a>リモート デバッグを有効にするリモート コンピューター上のポート

リモート デバッグの場合、リモート コンピューターで次のポートが開いている必要があります。

::: moniker range="vs-2017"

|**ポート**|**着信/発信**|**プロトコル**|**説明**|
|-|-|-|-|
|4022|着信|TCP|VS 2017 の場合。 ポート番号は、Visual Studio のバージョンごとに 2 ずつ増分されます。 詳しくは、「[Visual Studio remote debugger port assignments](../debugger/remote-debugger-port-assignments.md)」(Visual Studio リモート デバッガーのポートの割り当て) をご覧ください。|
|4023|着信|TCP|VS 2017 の場合。 ポート番号は、Visual Studio のバージョンごとに 2 ずつ増分されます。 このポートは、リモート デバッガーの 64 ビット バージョンから 32 ビット プロセスをリモート デバッグするためにのみ使用されます。 詳しくは、「[Visual Studio remote debugger port assignments](../debugger/remote-debugger-port-assignments.md)」(Visual Studio リモート デバッガーのポートの割り当て) をご覧ください。|
|3702|発信|UDP|(省略可能) リモート デバッガーの検出に必須。|

::: moniker-end

::: moniker range=">= vs-2019"

|**ポート**|**着信/発信**|**プロトコル**|**説明**|
|-|-|-|-|
|4024|着信|TCP|VS 2019 の場合。 ポート番号は、Visual Studio のバージョンごとに 2 ずつ増分されます。 詳しくは、「[Visual Studio remote debugger port assignments](../debugger/remote-debugger-port-assignments.md)」(Visual Studio リモート デバッガーのポートの割り当て) をご覧ください。|
|4025|着信|TCP|VS 2019 の場合。 ポート番号は、Visual Studio のバージョンごとに 2 ずつ増分されます。 このポートは、リモート デバッガーの 64 ビット バージョンから 32 ビット プロセスをリモート デバッグするためにのみ使用されます。 詳しくは、「[Visual Studio remote debugger port assignments](../debugger/remote-debugger-port-assignments.md)」(Visual Studio リモート デバッガーのポートの割り当て) をご覧ください。|
|3702|発信|UDP|(省略可能) リモート デバッガーの検出に必須。|

::: moniker-end

選択した場合 **マネージ互換モードを使用して** **ツール** > **オプション** > **デバッグ** を開きますこれらの追加のリモート デバッガー ポート。 デバッガー マネージド互換モードでは、レガシの Visual Studio 2010 バージョンのデバッガーが有効になります。

|**ポート**|**着信/発信**|**プロトコル**|**説明**|
|-|-|-|-|
|135、139、445|発信|TCP|必須です。|
|137、138|発信|UDP|必須です。|

ドメイン ポリシーにより、ネットワーク通信を IPSec 経由で実行する必要がある場合、Visual Studio とリモート コンピューターの両方で追加のポートを開く必要があります。 リモート IIS Web サーバーでデバッグするには、リモート コンピューターでポート 80 を開きます。

|**ポート**|**着信/発信**|**プロトコル**|**説明**|
|-|-|-|-|
|500、4500|発信|UDP|ドメイン ポリシーで、ネットワーク通信を IPSec 経由で実行する必要がある場合は、必須。|
|80|発信|TCP|Web サーバーのデバッグに必要。|

Windows ファイアウォールを介して特定のアプリを許可するには、「[Windows ファイアウォールを介してリモート デバッグを構成する](#configure-remote-debugging-through-windows-firewall)」を参照してください。

## <a name="configure-remote-debugging-through-windows-firewall"></a>Windows ファイアウォールを介してリモート デバッグを構成する

リモート デバッグ ツールをリモート コンピューターにインストールするか、または共有フォルダーから実行することができます。 どちらの場合も、リモート コンピューターのファイアウォールを正しく構成する必要があります。

リモート コンピューターでは、リモート デバッグ ツールは次の場所にあります。

*\<Visual Studio installation directory\>\\Common7\\IDE\\Remote Debugger\\\<x86*, *x64*, or *Appx*\>

### <a name="allow-and-configure-the-remote-debugger-through-windows-firewall"></a>Windows ファイアウォールを介してリモート デバッガーを許可および構成する

1. Windows の **[スタート]** メニューで、**Windows ファイアウォール**、または **Windows Defender ファイアウォール** を検索して開きます。

1. **[Windows ファイアウォールによるアプリケーションの許可]** を選択します。

1. **[許可されたアプリおよび機能]** の下に **[リモート デバッガー]** または **[Visual Studio リモート デバッガー]** が表示されない場合は、 **[設定の変更]** を選択し、 **[別のアプリの許可]** を選択します。

1. 依然として、リモート デバッガー アプリが **[アプリを追加する]** ダイアログの一覧に表示されない場合、 **[参照]** を選択し、アプリに適したアーキテクチャに応じて、*\<Visual Studio installation directory\>\\Common7\\IDE\\リモート デバッガー\\\<x86*, *x64*, or *Appx*\> に移動します。 *[msvsmon.exe]* を選択し、 **[追加]** を選択します。

1. **[アプリ]** の一覧で、追加したばかりの **[リモート デバッガー]** を選択します。 **[ネットワークの種類]** を選択し、1 つ以上のネットワークの種類 (リモート接続のネットワークの種類など) を選択します。

1. **[追加]** 、 **[OK]** の順に選択します。

## <a name="troubleshoot-the-remote-debugging-connection"></a><a name="troubleshooting"></a>リモート デバッグ接続のトラブルシューティング

リモート デバッガーを使用してアプリに接続できない場合、リモート デバッグのファイアウォールのポート、プロトコル、ネットワークの種類、アプリの設定のすべてが正しいことを確認します。

- Windows の **[スタート]** メニューで、**Windows ファイアウォール** を検索して開き、 **[Windows ファイアウォールによるアプリケーションの許可]** を選択します。 **[許可されたアプリおよび機能]** の一覧に **[リモート デバッガー]** または **[Visual Studio リモート デバッガー]** が表示され、チェック ボックスがオンで、正しいネットワークの種類が選択されていることを確認します。 そうでない場合は、[正しいアプリおよび設定を追加](#configure-remote-debugging-through-windows-firewall)します。

- Windows の **[スタート]** メニューで、**セキュリティが強化された Windows ファイアウォール** を検索して開きます。 **[受信規則]** (および任意で **[送信規則]** ) の下に **[リモート デバッガー]** または **[Visual Studio リモート デバッガー]** が表示され、緑色のチェックマーク アイコンが付いていることと、すべての設定が正しいことを確認します。

  - 規則の設定を表示または変更するには、一覧で **[リモート デバッガー]** アプリを右クリックし、 **[プロパティ]** を選択します。 規則を有効または無効にしたり、ポート番号、プロトコル、またはネットワークの種類を変更したりするには、 **[プロパティ]** タブを使用します。
  - リモート デバッガー アプリが規則の一覧に表示されない場合は、[正しいポートを追加して構成](#configure-ports-for-remote-debugging)します。

## <a name="see-also"></a>関連項目

- [リモート デバッグ](../debugger/remote-debugging.md)
- [Visual Studio リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
