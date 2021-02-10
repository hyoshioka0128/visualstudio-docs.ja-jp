---
title: リモート コンピューターにアクセスしようとしたときに、DCOM エラーが発生しました。 アクセスが拒否されました。
titleSuffix: ''
description: "\"リモート コンピューターにアクセスしようとしたときに、DCOM エラーが発生しました。 アクセスが拒否されました。\" この Visual Studio リモート デバッグのエラー参照に関する情報を表示します。"
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.remote.dcom_access_denied
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, DCOM error
- remote DCOM access denied error
- DCOM, access errors
ms.assetid: 9d7dfc1b-9fe0-4f54-9c50-9c0e0f8358c5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4e4c33065feff6b4a2a0d3e292004b51fda744cf
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858034"
---
# <a name="a-dcom-error-occurred-trying-to-contact-the-remote-computer-access-is-denied"></a>リモート コンピューターにアクセスしようとしたときに、DCOM エラーが発生しました。 アクセスが拒否されました。
リモート デバッグでは、DCOM を使用して次のような状況でローカル コンピューターとリモート コンピューターとの間で通信します。

- **[ツール] > [オプション] > [デバッグ]** ページで、デバッガーが **[ネイティブ互換モード]** に設定されるか、または **[マネージド互換モード]** がオンに設定されている場合。

- マネージド C++ (C + +/CLI) コードをデバッグする場合。

- Visual Studio 2013 で、 **[ツール] > [オプション] > [デバッグ]** ページの **[ネイティブのエディット コンティニュを有効にする]** がオンになっている場合。

- 一部のサード パーティのデバッグ シナリオ

  このエラーが発生するのは、Visual Studio のプロセスが DCOM 経由でリモート デバッガープロセスに対して自己認証できない (入力した資格情報が不十分と見なされた) 場合です。 次のいずれかの回避策で問題を解決できることがあります。

- **[ネイティブ互換モード]** と **[マネージド互換モード]** をオフにします。

- Visual Studio 2013 で、 **[ネイティブのエディット コンティニュを有効にする]** をオフにします。

- 両方のコンピューターを再起動する。

- リモート デバッグで資格情報の入力が必要な場合は、資格情報の保存のチェック ボックスをオンにする。

## <a name="see-also"></a>関連項目

- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Remote Debugging](../debugger/remote-debugging.md)