---
title: '[リモート デバッグのファイアウォールの構成] ダイアログ ボックス | Microsoft Docs'
description: '[リモート デバッグのファイアウォールの構成] ダイアログ ボックスについて説明します。これは、Windows ファイアウォールによってデバッガーがネットワーク経由でデータを受信できなくなったときに表示されます。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.firewallconfiguration
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Configure Firewall for Remote Debugging dialog box
- remote debugging, configuring firewalls
- firewalls, configuring for remote debugging
ms.assetid: 5dff3393-fdeb-4129-a2f6-31f653107a82
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 86a0cac2e42e1271e689f2b1880eef8ca6d14644
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97728964"
---
# <a name="configure-firewall-for-remote-debugging-dialog-box"></a>[リモート デバッグのファイアウォールの構成] ダイアログ ボックス
このダイアログ ボックスは、Windows ファイアウォールによってデバッガーがネットワーク経由で情報を受信できないときに表示されます。 リモート デバッグを続行するには、デバッガーが情報を受信できるようにファイアウォールに穴を開ける必要があります。

> [!CAUTION]
> ファイアウォールに穴を開けると、ファイアウォールによってセキュリティ上の脅威がブロックされなくなるため、コンピューターが脅威にさらされる可能性があります。 リモート デバッグのための穴を開けると、Visual Studio 2015 のポート 4020 と 4021 のブロックが解除されます。 その他のバージョンの Visual Studio では、他のポート番号を使用します。 詳細については、「[リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください。 また、デバッガーが追加のポートを開くことができるようになります。 詳細については、「[Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)」を参照してください。

## <a name="uielement-list"></a>UIElement の一覧
 **リモート デバッグを取り消す** リモート デバッグの試行を取り消します。 コンピューターのセキュリティ設定はそのままの状態で保持されます。

 **[ローカル ネットワーク (サブネット) 上のコンピューターからのリモート デバッグは制限しない]** ローカル サブネット上のマシンのリモート デバッグを有効にします。 これにより、ローカル サブネット上のコンピューターが脆弱になることがありますが、引き続きファイアウォールによってサブネットの外部から入ってくる情報がブロックされます。

 **[すべてのコンピューターからのリモート デバッグを制限しない]** ネットワーク上のすべての場所にあるコンピューターのリモート デバッグを有効にします。 この設定では、セキュリティが最も低くなります。

## <a name="see-also"></a>関連項目

- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [Remote Debugging](../debugger/remote-debugging.md)
- [デバッグ用ユーザー インターフェイス リファレンス](../debugger/debugging-user-interface-reference.md)