---
title: エラー - ローカル コンピューターのファイアウォール | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.firewall.localmachine
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
ms.openlocfilehash: 115546a0fd3a9aad804391816ce8bac88429d0ec
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460753"
---
# <a name="error-firewall-on-local-machine"></a>エラー :ローカル コンピューターのファイアウォール
Visual Studio を実行するローカル コンピューターのインターネット接続ファイアウォールは、リモート デバッグを許可するように設定されていません。 既定のトランスポートを使用したマネージド リモート デバッグまたはネイティブ リモート デバッグでは、DCOM トラフィック用に TCP 135 ポートを開く必要があります。 ファイルおよびプリンターの共有を有効にし、devenv.exe を例外リストに追加することも必要です。 また、IPSEC ポートを開く必要がある場合もあります。

 詳細については、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。