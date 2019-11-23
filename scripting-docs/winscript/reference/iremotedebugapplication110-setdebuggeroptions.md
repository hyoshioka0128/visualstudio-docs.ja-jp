---
title: 'IRemoteDebugApplication110:: Setデバッガオプション |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplication110::SetDebuggerOptions
ms.assetid: 58e9fd18-3e0d-47fa-8893-f316146bde84
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e7168a4ef8ec70368c0ff691ba1f721275f9d65d
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577419"
---
# <a name="iremotedebugapplication110setdebuggeroptions"></a>IRemoteDebugApplication110::SetDebuggerOptions
デバッガーオプションを更新するために呼び出されます。 このメソッドは、 [Iremotedebugapplication:: ConnectDebugger](../../winscript/reference/iremotedebugapplication-connectdebugger.md)の後に呼び出す必要があります。 [Iremotedebugapplication::D isconnectDebugger](../../winscript/reference/iremotedebugapplication-disconnectdebugger.md)メソッドは、自動的に既定のオプションにリセットされます。 既定では、オプションは 0 (SDO_NONE) です。  
  
> [!IMPORTANT]
> [Iremotedebugapplication インターフェイス](../../winscript/reference/iremotedebugapplication-interface.md)は、PDM version 11.0 以上で実装されています。 activdbg100.h にあります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetDebuggerOptions(        [in] enum SCRIPT_DEBUGGER_OPTIONS mask,        [in] enum SCRIPT_DEBUGGER_OPTIONS value    );  
```  
  
#### <a name="parameters"></a>パラメーター  
 `mask`  
 [SCRIPT_DEBUGGER_OPTIONS 列挙](../../winscript/reference/script-debugger-options-enumeration.md)マスク。  
  
 `value`  
 [SCRIPT_DEBUGGER_OPTIONS 列挙](../../winscript/reference/script-debugger-options-enumeration.md)値。  
  
## <a name="see-also"></a>参照  
 [Iremotedebugapplication インターフェイス](../../winscript/reference/iremotedebugapplication-interface.md)   
 [IRemoteDebugApplication110 インターフェイス](../../winscript/reference/iremotedebugapplication110-interface.md)