---
title: エラー :DCOM 通信を初期化できません | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
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
ms.openlocfilehash: 8a5e45df06d4b9490160c94902457ea630548966
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72736728"
---
# <a name="error-unable-to-initiate-dcom-communication"></a>エラー :DCOM 通信を初期化できません。
ローカル コンピューターがリモート コンピューターと通信しようとしたときに DCOM エラーが発生しました。 このエラーは、リモート サーバーのファイアウォール、またはリモート コンピューターで Windows 認証が破損していることに原因があります。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- リモート コンピューターで Windows ファイアウォールが有効になっている場合は、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照し、ローカル デバッグを実行できるようにファイアウォールを設定する手順を確認してください。

- Windows 認証を復元するために、両方のコンピューターを再起動してみます。 Kerberos エラーがないかどうかローカル コンピューターとリモート コンピューターのイベント ログを確認し、既知の問題がないかどうかドメイン管理者に問い合わせてください。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)