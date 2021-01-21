---
title: DCOM 通信を初期化できません | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.unmarshal_server_failed
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
ms.openlocfilehash: 00846f0ef0593ec7d12c657a40079ff1cdfb0bb5
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90851438"
---
# <a name="error-unable-to-initiate-dcom-communication"></a>エラー :DCOM 通信を初期化できません。
ローカル コンピューターがリモート コンピューターと通信しようとしたときに DCOM エラーが発生しました。 このエラーは、リモート サーバーのファイアウォール、またはリモート コンピューターで Windows 認証が破損していることに原因があります。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- リモート コンピューターで Windows ファイアウォールが有効になっている場合は、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照し、ローカル デバッグを実行できるようにファイアウォールを設定する手順を確認してください。

- Windows 認証を復元するために、両方のコンピューターを再起動してみます。 Kerberos エラーがないかどうかローカル コンピューターとリモート コンピューターのイベント ログを確認し、既知の問題がないかどうかドメイン管理者に問い合わせてください。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)