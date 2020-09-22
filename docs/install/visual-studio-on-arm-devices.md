---
title: ARM 搭載デバイスの Visual Studio
description: ARM ベースのプロセッサを搭載したデバイスで Visual Studio を使用する場合の推奨事項。
ms.date: 09/10/2020
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 6aacd4639e440998a5123dae8c38a64c84ebb948
ms.sourcegitcommit: d9dd86c421532cfca6c0c5761d160f35829419c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90026302"
---
# <a name="visual-studio-on-arm-powered-devices"></a>ARM 搭載デバイスの Visual Studio

> [!IMPORTANT]
> Visual Studio は、x86 または AMD64/x64 ベースのプロセッサを使用しているデバイスでのみサポートされています。

Visual Studio は、x86 アーキテクチャに基づくプロセッサを対象とするように構築されており、ARM ベースのプロセッサを対象とした Visual Studio のバージョンはありません。 ただし、Windows には、Visual Studio を実行できる [ARM 用の x86 エミュレーション](https://www.docs.microsoft.com/windows/uwp/porting/apps-on-arm-x86-emulation)が用意されています。 x86 エミュレーションを使用して ARM プロセッサで Visual Studio を実行すると、Visual Studio のパフォーマンスが著しく低下します。また、Visual Studio のいくつかの機能は、このシナリオで動作するように設計されていません。 そのため、ARM ベースのプロセッサを使用するデバイスで Visual Studio を実行することはお勧めしません。代わりに、リモートを対象とする ARM デバイスを使用することをお勧めします。

## <a name="remote-targeting-arm-devices"></a>リモートを対象とする ARM デバイス
最適なエクスペリエンスを実現するために、Visual Studio を x86 を搭載した別のコンピューターで使用し、Visual Studio のリモート展開およびデバッグ機能を使用して ARM ベースのデバイスを対象にすることをお勧めします。 デバイスに既にインストールされている Windows ユニバーサル アプリケーションをデバッグするには、[インストール済みアプリ パッケージのデバッグ](../debugger/debug-installed-app-package.md)に関する記事を参照してください。 新しいアプリを展開するには、[Windows Store アプリのリモート実行](../debugger/run-windows-store-apps-on-a-remote-machine.md)に関する記事を参照してください。 その他すべてのアプリケーションの種類については、「[リモート デバッグ](../debugger/remote-debugging.md)」のドキュメントを参照してください。

## <a name="tips-for-running-visual-studio-on-arm-devices"></a>ARM デバイスでの Visual Studio の実行に関するヒント

### <a name="use-only-when-needed"></a>必要な場合にのみ使用する
時間を最適化するため、Visual Studio は ARM 固有の作業に必要な場合にのみ使用します。 ARM 搭載デバイスのパフォーマンスは、通常の用途では許容できないほど低下する可能性があります。

### <a name="install-time"></a>インストール時間
Visual Studio のインストールには時間がかかることを見込んでください。一定時間の停止、または再起動が必要になります。
 
### <a name="remote-tools"></a>［リモート ツール］
リモート デバイスで実行されているアプリをデバッグするには、ARM 用の[リモート ツールをダウンロードしてインストールする](../debugger/remote-debugging.md#download-and-install-the-remote-tools)必要があります。

### <a name="start-debugging-f5"></a>デバッグを開始する (F5)
ARM デバイスからデバッグを開始する (**F5**) ときに、すべての Visual Studio プロジェクトがローカルでプロジェクトを起動するように構成されているわけではありません。 アプリがローカルで実行されている場合でも、リモート デバッグのために Visual Studio の構成が必要になる場合があります。 詳細については、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

## <a name="we-need-your-help"></a>あなたのサポートが必要です。
Visual Studio を ARM デバイスでネイティブに実行する場合に必要なシナリオとサポートについてのご意見をお待ちしております。 ご連絡をいただく場合は、[開発者コミュニティ](https://developercommunity.visualstudio.com/idea/1161018/native-arm-support-for-visual-studio.html)に投稿してください。 
