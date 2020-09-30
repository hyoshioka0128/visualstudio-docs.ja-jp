---
title: リモート デバッガーのダウンロード
description: リモート デバッガーのダウンロード リンク
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 86bc2a1b73b492dc5f8d9977f05c3b2ba0dde6dc
ms.sourcegitcommit: 13cf7569f62c746708a6ced1187d8173eda7397c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91376700"
---
Visual Studio マシンではなく、デバッグするリモート デバイスまたはサーバーで、次の表のリンクから適切なバージョンのリモート ツールをダウンロードしてインストールします。

- お使いのバージョンの Visual Studio 用の最新のリモート ツールをダウンロードします。 最新バージョンのリモート ツールは、以前のバージョンの Visual Studio と互換性がありますが、以前のバージョンのリモート ツールは、以降のバージョンの Visual Studio と互換性がありません (たとえば、Visual Studio 2017 を使用している場合、Visual Studio 2017 用のリモート ツールの最新の更新プログラムをダウンロードします。 このシナリオでは、Visual Studio 2019 用のリモート ツールをダウンロードしないでください)。
- インストール先のマシンと同じアーキテクチャを持つリモート ツールをダウンロードします。 たとえば、64 ビットのオペレーティング システムを実行しているリモート コンピューターで 32 ビット アプリをデバッグする場合は、64 ビットのリモート ツールをインストールします。

::: moniker range=">=vs-2019"

|バージョン|Link|メモ|
|-|-|-|
|Visual Studio 2019|[リモート ツール](https://visualstudio.microsoft.com/downloads#remote-tools-for-visual-studio-2019)|すべてのバージョンの Visual Studio 2019 と互換性があります。 デバイスのオペレーティング システム (x86、x64、または ARM64) に一致するバージョンをダウンロードします。 Windows Server の場合、リモート ツールのダウンロードについては、[ファイルのダウンロードのブロック解除](../../debugger/remote-debugging-unblock-file-download.md)に関するページを参照してください。|
|Visual Studio 2017|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|すべてのバージョンの Visual Studio 2017 と互換性があります。 デバイスのオペレーティング システム (x86、x64、または ARM64) に一致するバージョンをダウンロードします。 Windows Server の場合、リモート ツールのダウンロードについては、[ファイルのダウンロードのブロック解除](../../debugger/remote-debugging-unblock-file-download.md)に関するページを参照してください。|
|Visual Studio 2015|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Visual Studio 2015 用のリモート ツールは My.VisualStudio.com で入手できます。 メッセージが表示されたら、無料の [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) プログラムに参加するか、または Visual Studio サブスクリプション ID でサインインします。 Windows Server の場合、リモート ツールのダウンロードについては、[ファイルのダウンロードのブロック解除](../../debugger/remote-debugging-unblock-file-download.md)に関するページを参照してください。|
|Visual Studio 2013|[リモート ツール](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|Visual Studio 2013 ドキュメントのダウンロード ページ|
|Visual Studio 2012|[リモート ツール](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|Visual Studio 2012 ドキュメントのダウンロード ページ|

::: moniker-end

::: moniker range="vs-2017"

|バージョン|Link|メモ|
|-|-|-|
|Visual Studio 2017|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|すべてのバージョンの Visual Studio 2017 と互換性があります。 デバイスのオペレーティング システム (x86、x64、または ARM64) に一致するバージョンをダウンロードします。 Windows Server の場合、リモート ツールのダウンロードについては、[ファイルのダウンロードのブロック解除](../../debugger/remote-debugging-unblock-file-download.md)に関するページを参照してください。 最新バージョンのリモート ツールについては、[Visual Studio 2019 ドキュメント](../../debugger/remote-debugging.md?view=vs-2019&preserve-view=true)を開きます。|
|Visual Studio 2015|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Visual Studio 2015 用のリモート ツールは My.VisualStudio.com で入手できます。 メッセージが表示されたら、無料の [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) プログラムに参加するか、または Visual Studio サブスクリプション ID でサインインします。 Windows Server の場合、リモート ツールのダウンロードについては、[ファイルのダウンロードのブロック解除](../../debugger/remote-debugging-unblock-file-download.md)に関するページを参照してください。|
|Visual Studio 2013|[リモート ツール](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|Visual Studio 2013 ドキュメントのダウンロード ページ|
|Visual Studio 2012|[リモート ツール](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|Visual Studio 2012 ドキュメントのダウンロード ページ|

::: moniker-end

リモート デバッガーを実行するには、リモート ツールをインストールするのではなく、*msvsmon.exe* をリモート コンピューターにコピーします。 ただし、リモート デバッガー構成ウィザード (*rdbgwiz.exe*) は、リモート ツールをインストールした場合にのみ使用できます。 リモート デバッガーをサービスとして実行する場合は、構成にウィザードの使用が必要になることがあります。 詳細については、「[(オプション) リモート デバッガーをサービスとして構成する](../../debugger/remote-debugging.md#bkmk_configureService)」を参照してください。

>[!NOTE]
>- ARM デバイスで Windows 10 アプリをデバッグするには、最新バージョンのリモート ツールで使用できる ARM64 を使用します。
>- Windows RT デバイスで Windows 10 アプリをデバッグするには、ARM を使用します。これは、Visual Studio 2015 リモート ツールのダウンロードでのみ使用できます。
