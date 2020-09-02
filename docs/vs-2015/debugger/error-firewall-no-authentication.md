---
title: エラー :ファイアウォールの認証が設定されていません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.firewall.noauth
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: dda1acb8-bed7-4bc8-9991-9cdc49c2ac1e
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: db13165c584399952dc491cf714ac84ee4de7598
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697426"
---
# <a name="error-firewall-no-authentication"></a>エラー :ファイアウォールの認証が設定されていません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リモート コンピューターのインターネット接続ファイアウォールが、リモート デバッグを許可するように設定されていません。 `No Authentication` を使用してリモート デバッグを実行するには、例外リストに msvsmon.exe を追加する必要があります。 また、IPSEC ポートを開く必要がある場合もあります。  
  
> [!NOTE]
> リモート デバッガーでは Windows ファイアウォールの自動構成が可能です。 サード パーティのソフトウェア ファイアウォールやハードウェア ファイアウォールなど、Windows ファイアウォール以外のファイアウォールを使用する場合は、リモート デバッグを許可するようにファイアウォールを手動で構成する必要があります。 そのためには、msvsmon.exe がリッスンしている TCP/IP ポートのトラフィックを許可します。 既定では、これらのポートは 4018 と 4019 です。4018 はすべてのオペレーティング システムで使用され、4019 は Windows x64 でのみ使用されます。該当するポートで x86 プロセスのデバッグを許可します。  
  
 詳細については、「 [デバイスにリモートツールを設定する](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)」を参照してください。
