---
title: リモート コンピューター上の Microsoft Visual Studio リモート デバッグ モニターには、このコンピューターに接続するアクセス許可がありません
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.access_denied_oncallback
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, Windows version error
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e7baed5cc2c4c8dbaa01cd3dfadc386b6db1834c
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90851087"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-does-not-have-permission-to-connect-to-this-computer"></a>エラー :リモート コンピューター上の Microsoft Visual Studio リモート デバッグ モニターには、このコンピューターに接続するアクセス許可がありません

このエラーは、Visual Studio リモート デバッグ モニター (msvsmon) を実行しようとしたユーザーのアカウントがローカル コンピューターにない場合に発生します。 このエラーは、レガシ デバッグ エンジンを使用したリモート デバッグ時に発生する可能性があります。

## <a name="to-fix-this-problem"></a>この問題を解決するには

- リモート コンピューターで msvsmon を実行しているユーザー アカウントと同じ名前およびパスワードを使用して、Visual Studio デバッガー ホスト コンピューターにユーザー アカウントを追加します。

   \- または

- ローカル コンピューターを呼び出すアクセス許可を持つユーザーとして msvsmon を実行します。 つまり、ユーザーは msvsmon コンピューターのドメイン ユーザーおよび管理者である必要があります。 msvsmon を実行するユーザー アカウントは次の 2 とおりの方法で指定できます。

  - msvsmon アイコンを右クリックし、ショートカット メニューの **[別のユーザーとして実行]** をクリックします。

    \- または

  - コマンド プロンプトで `runas.exe` を実行します。

## <a name="see-also"></a>関連項目

- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Remote Debugging](../debugger/remote-debugging.md)