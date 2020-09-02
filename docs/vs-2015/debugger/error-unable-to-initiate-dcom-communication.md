---
title: エラー :DCOM 通信を初期化できません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.unmarshal_server_failed
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 2a7b27e6-2526-4f32-bc4d-eaee447f24ec
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fff1c56915fe4a06d66bdb08ce60219642933b1b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682532"
---
# <a name="error-unable-to-initiate-dcom-communication"></a>エラー :DCOM 通信を初期化できません。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ローカル コンピューターがリモート コンピューターと通信しようとしたときに DCOM エラーが発生しました。 このエラーは、リモート サーバーのファイアウォール、またはリモート コンピューターで Windows 認証が破損していることに原因があります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- リモートコンピューターで Windows ファイアウォールが有効になっている場合、ローカルデバッグ用にファイアウォールを構成する手順については、「 [デバイスでのリモートツールの設定](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c) 」を参照してください。  
  
- Windows 認証を復元するために、両方のコンピューターを再起動してみます。 Kerberos エラーがないかどうかローカル コンピューターとリモート コンピューターのイベント ログを確認し、既知の問題がないかどうかドメイン管理者に問い合わせてください。  
  
## <a name="see-also"></a>参照  
 [Remote Debugging](../debugger/remote-debugging.md)
