---
title: '[リモートデバッグ用にファイアウォールを構成する] ダイアログボックス |Microsoft Docs'
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
ms.openlocfilehash: 8a2511fc2adfa63ff28f8459f48cbdf4b4623ff5
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745661"
---
# <a name="configure-firewall-for-remote-debugging-dialog-box"></a>[リモート デバッグのファイアウォールの構成] ダイアログ ボックス
このダイアログ ボックスは、Windows ファイアウォールによってデバッガーがネットワーク経由で情報を受信できないときに表示されます。 リモート デバッグを続行するには、デバッガーが情報を受信できるようにファイアウォールに穴を開ける必要があります。

> [!CAUTION]
> ファイアウォールに穴を開けると、ファイアウォールによってセキュリティ上の脅威がブロックされなくなるため、コンピューターが脅威にさらされる可能性があります。 リモート デバッグのための穴を開けると、Visual Studio 2015 のポート 4020 と 4021 のブロックが解除されます。 その他のバージョンの Visual Studio では、他のポート番号を使用します。 詳細については、「[リモートデバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください。 また、デバッガーが追加のポートを開くことができるようになります。 詳細については、「[リモートデバッグのための Windows ファイアウォールの構成](../debugger/configure-the-windows-firewall-for-remote-debugging.md)」を参照してください。

## <a name="uielement-list"></a>UIElement の一覧
 **リモートデバッグのキャンセル**リモートデバッグの試行をキャンセルします。 コンピューターのセキュリティ設定はそのままの状態で保持されます。

 **ローカルネットワーク (サブネット) 上のコンピューターからのリモートデバッグのブロックを解除**するローカルサブネット上のコンピューターのリモートデバッグを有効にします。 これにより、ローカル サブネット上のコンピューターが脆弱になることがありますが、引き続きファイアウォールによってサブネットの外部から入ってくる情報がブロックされます。

 **任意のコンピューターからのリモートデバッグのブロック解除**ネットワーク上の任意の場所にあるコンピューターのリモートデバッグを有効にします。 この設定では、セキュリティが最も低くなります。

## <a name="see-also"></a>関連項目

- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [Remote Debugging](../debugger/remote-debugging.md)
- [デバッグ用ユーザー インターフェイス リファレンス](../debugger/debugging-user-interface-reference.md)
