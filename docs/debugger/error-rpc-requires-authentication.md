---
title: エラー - 認証を要求する RPC | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.rpc_requires_authentication
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
ms.openlocfilehash: e98daf3697c86eec7767135c9ad85d67cd6e958a
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460586"
---
# <a name="error-rpc-requires-authentication"></a>エラー :認証を要求する RPC
Visual Studio デバッガーは、リモート コンピューターに接続できません。 リモート コンピューター上で、リモート デバッグを制限する RPC ポリシーが有効になっています。

### <a name="to-correct-this-error"></a>このエラーを解決するには

1. `\`*windir*`\system32\regedt32.exe` を実行します。

2. `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows NT\RPC\RestrictRemoteClients` を見つけて削除します。

3. コンピューターを再起動してレジストリの変更を有効にします。

4. 問題が解決されない場合は、 **[コンピューターの構成]、[管理用テンプレート]、[システム]、[リモート プロシージャ コール]、[認証されていない RPC クライアントの制限]** グループ ポリシー設定についてご自分のドメイン管理者にお問い合わせください。