---
title: エラー :リモート コンピューター上の Microsoft Visual Studio リモート デバッグ モニターは、別のユーザーで実行しています。
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: troubleshooting
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- -anyuser option
- anyuser option
- Remote Debugging Monitor
- remote debugging, Remote Debugging Monitor
- msvsmon.exe
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b5ff383b279bbdac85ce85de6e65b857cec6a8e7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737486"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user"></a>エラー :リモート コンピューター上の Microsoft Visual Studio リモート デバッグ モニターは、別のユーザーで実行しています。
リモート デバッグを行おうとすると、次のエラー メッセージが表示される場合があります。

 リモート コンピューター上の Microsoft Visual Studio リモート デバッグ モニターは、別のユーザーで実行しています。

## <a name="cause"></a>原因
 このメッセージは、認証なしモードでのデバッグ中に、msvsmon を起動したユーザーが Visual Studio を実行中のユーザーと一致しない場合に発生します。

## <a name="solution"></a>ソリューション
 最も安全で適切な解決策は、Visual Studio と同じユーザー アカウントでリモート デバッグ モニター (msvsmon.exe) を実行することです。 これができない場合は、リモート デバッグ モニターの **[オプション]** ダイアログ ボックスの **[すべてのユーザーにデバッグを許可する]** をオンにして他のアカウントでリモート デバッグ モニターを実行します。

> [!CAUTION]
> 他のユーザーに接続する許可を与えると、誤ったリモート デバッグ セッションに接続してしまう可能性があります。 **認証なし**モードでのデバッグは決して安全ではなく、使用には注意が必要です。

## <a name="see-also"></a>関連項目
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Remote Debugging](../debugger/remote-debugging.md)