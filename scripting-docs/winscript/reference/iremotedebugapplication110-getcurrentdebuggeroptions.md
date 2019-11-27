---
title: 'IRemoteDebugApplication110:: Getcurrentデバッガ Options |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplication110::GetCurrentDebuggerOptions
ms.assetid: a6e9cae1-e8f3-4d62-b133-52e9ca12ba7a
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b6ae042a5d4d1c1ee350b328fdc5a9b7420d9928
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577429"
---
# <a name="iremotedebugapplication110getcurrentdebuggeroptions"></a>IRemoteDebugApplication110::GetCurrentDebuggerOptions
現在有効になっているオプションのセットを返します。  
  
> [!IMPORTANT]
> [Iremotedebugapplication インターフェイス](../../winscript/reference/iremotedebugapplication-interface.md)は、PDM version 11.0 以上で実装されています。 activdbg100.h にあります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCurrentDebuggerOptions([out] enum SCRIPT_DEBUGGER_OPTIONS* pCurrentOptions);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pCurrentOptions`  
 入出力現在のオプション。  
  
## <a name="see-also"></a>参照  
 [Iremotedebugapplication インターフェイス](../../winscript/reference/iremotedebugapplication-interface.md)   
 [IRemoteDebugApplication110 インターフェイス](../../winscript/reference/iremotedebugapplication110-interface.md)