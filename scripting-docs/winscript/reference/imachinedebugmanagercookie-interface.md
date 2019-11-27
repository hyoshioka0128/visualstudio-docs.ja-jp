---
title: IMachineDebugManagerCookie インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IMachineDebugManagerCookie interface
ms.assetid: 04770935-3ccf-41e9-b0c1-c78376ab1e3c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6b39c286f389c99187b0f3250fc68af92ff5dcc8
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573886"
---
# <a name="imachinedebugmanagercookie-interface"></a>IMachineDebugManagerCookie インターフェイス
`IMachineDebugManager` インターフェイスと同様に、`IMachineDebugManagerCookie` インターフェイスはデバッグ cookie をサポートしています。  
  
 このインターフェイス (`IDebugCookie` インターフェイス) を使用すると、スクリプトをスクリプトデバッガープロセスで実行できます。デバッガーでそれらのスクリプトを追跡する必要はありません。  
  
 スクリプトデバッガーは、プロセスデバッグマネージャー (PDM) で `IDebugCookie::SetDebugCookie` メソッドを呼び出します。 次に、このクッキーは、`IMachineDebugManagerCookie` インターフェイスのメソッドを使用して、マシンデバッグマネージャー (MDM) との間でスクリプトアプリケーションを追加または削除するための要求と共に、この cookie を送信します。 その後、MDM は、その cookie を持つものを除き、変更のすべてのデバッガーに通知します。  
  
 `IMachineDebugManagerCookie` インターフェイスは、`IUnknown`から継承されたメソッドに加えて、次のメソッドを公開します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IMachineDebugManagerCookie::AddApplication](../../winscript/reference/imachinedebugmanagercookie-addapplication.md)|実行中のアプリケーションの一覧にアプリケーションを追加します。|  
|[IMachineDebugManagerCookie::EnumApplications](../../winscript/reference/imachinedebugmanagercookie-enumapplications.md)|実行中のアプリケーションの現在の一覧の列挙子を返します。|  
|[IMachineDebugManagerCookie::RemoveApplication](../../winscript/reference/imachinedebugmanagercookie-removeapplication.md)|実行中のアプリケーションの一覧からアプリケーションを削除します。|  
  
## <a name="see-also"></a>参照  
 [Imachinedebugmanager インターフェイス](../../winscript/reference/imachinedebugmanager-interface.md)   
 [IDebugCookie インターフェイス](../../winscript/reference/idebugcookie-interface.md)