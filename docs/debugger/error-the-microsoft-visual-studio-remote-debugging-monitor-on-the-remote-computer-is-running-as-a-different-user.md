---
title: リモート コンピューター上の Microsoft Visual Studio リモート デバッグ モニターは、別のユーザーで実行しています。
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: error-reference
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
ms.openlocfilehash: 5acf69b980221c0d953e22e66502672477656dbc
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90851763"
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