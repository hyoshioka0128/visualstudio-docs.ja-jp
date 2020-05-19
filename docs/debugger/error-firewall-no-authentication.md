---
title: エラー :ファイアウォールの認証が設定されていません | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.firewall.noauth
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4a72d16869c92b1965fae8db0ae32146a3a57e67
ms.sourcegitcommit: 3fe6bed9ef8fb1478106645f655c7472009ae43a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64823946"
---
# <a name="error-firewall-no-authentication"></a>エラー :ファイアウォールの認証が設定されていません
リモート コンピューターのインターネット接続ファイアウォールが、リモート デバッグを許可するように設定されていません。 `No Authentication` を使用してリモート デバッグを実行するには、例外リストに msvsmon.exe を追加する必要があります。 また、IPSEC ポートを開く必要がある場合もあります。

> [!NOTE]
> リモート デバッガーでは Windows ファイアウォールの自動構成が可能です。 サード パーティのソフトウェア ファイアウォールやハードウェア ファイアウォールなど、Windows ファイアウォール以外のファイアウォールを使用する場合は、リモート デバッグを許可するようにファイアウォールを手動で構成する必要があります。 そのためには、msvsmon.exe がリッスンしている TCP/IP ポートのトラフィックを許可します。 既定では、これらのポートは 4018 と 4019 です。4018 はすべてのオペレーティング システムで使用され、4019 は Windows x64 でのみ使用されます。該当するポートで x86 プロセスのデバッグを許可します。

 詳細については、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。