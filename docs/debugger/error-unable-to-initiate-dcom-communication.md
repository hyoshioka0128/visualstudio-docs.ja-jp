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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2ddae1685935cbb5267d3cc4f994c16e99a542da
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99870923"
---
# <a name="error-unable-to-initiate-dcom-communication"></a>エラー :DCOM 通信を初期化できません。
ローカル コンピューターがリモート コンピューターと通信しようとしたときに DCOM エラーが発生しました。 このエラーは、リモート サーバーのファイアウォール、またはリモート コンピューターで Windows 認証が破損していることに原因があります。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- リモート コンピューターで Windows ファイアウォールが有効になっている場合は、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照し、ローカル デバッグを実行できるようにファイアウォールを設定する手順を確認してください。

- Windows 認証を復元するために、両方のコンピューターを再起動してみます。 Kerberos エラーがないかどうかローカル コンピューターとリモート コンピューターのイベント ログを確認し、既知の問題がないかどうかドメイン管理者に問い合わせてください。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)