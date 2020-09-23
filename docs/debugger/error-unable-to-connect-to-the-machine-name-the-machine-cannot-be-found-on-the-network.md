---
title: コンピューター &lt;name&gt; に接続できません。 ネットワーク上にコンピューターが見つかりません。 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.remote.dcom_disabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- DCOM, unable to connect error
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1ab43773b4aa9d2535eb6ac157ec39333907731
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90852512"
---
# <a name="error-unable-to-connect-to-the-machine-ltnamegt-the-machine-cannot-be-found-on-the-network"></a>エラー :コンピューター &lt;name&gt; に接続できません。 ネットワーク上にコンピューターが見つかりません。
このエラーは、次の条件のいずれかが満たされると発生します。

- リモート コンピューターへの接続が解除された。

- リモート コンピューターのユーザー アカウントが無効になっている。

- リモート コンピューターのパスワードの有効期限が切れている。

### <a name="to-resolve-this-behavior"></a>この問題を解決するには

- ローカル コンピューターとリモート コンピューターが同じネットワーク上に存在することを確認します。 これを行うには、Microsoft Windows エクスプローラー (ファイル エクスプローラー) を使用してリモート コンピューターにアクセスしてみます。

     および

- リモート コンピューターへの接続に使用しているユーザー アカウントが有効になっていることを確認します。

     および

- リモート コンピューターへの接続に使用しているパスワードが有効であり、有効期限が切れていないことを確認します。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)