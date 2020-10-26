---
title: エラー :認証を要求する RPC | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.rpc_requires_authentication
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 88362b3b-8fbe-431f-96a4-80e2d822bbc7
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dbf0c2d13668dbf380f326ee3a49e0389815a8fd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62535737"
---
# <a name="error-rpc-requires-authentication"></a>エラー :認証を要求する RPC
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio デバッガーは、リモート コンピューターに接続できません。 リモート コンピューター上で、リモート デバッグを制限する RPC ポリシーが有効になっています。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. `\`*windir*`\system32\regedt32.exe` を実行します。  
  
2. `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows NT\RPC\RestrictRemoteClients` を見つけて削除します。  
  
3. コンピューターを再起動してレジストリの変更を有効にします。  
  
4. 問題が解決しない場合は、ドメイン管理者にコンピューターの構成について問い合わせてください。 **>管理用テンプレート->システム->リモートプロシージャコール-認証されていない RPC クライアントに対する >の制限事項** ] グループポリシー設定です。
