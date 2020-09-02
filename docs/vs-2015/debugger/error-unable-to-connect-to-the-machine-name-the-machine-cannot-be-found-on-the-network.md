---
title: エラー :コンピューター &lt;name&gt; に接続できません。 ネットワーク上にコンピューターが見つかりません。 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.remote.dcom_disabled
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- DCOM, unable to connect error
ms.assetid: b584b5db-ef52-45ed-8561-1314da3cc5b8
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dd1402a476ce2dceaaaf78580b36db20c3eed24f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682555"
---
# <a name="error-unable-to-connect-to-the-machine-ltnamegt-the-machine-cannot-be-found-on-the-network"></a>エラー :コンピューター &lt;name&gt; に接続できません。 ネットワーク上にコンピューターが見つかりません。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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
  
## <a name="see-also"></a>参照  
 [デバイスにリモートツールを設定する](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)   
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
