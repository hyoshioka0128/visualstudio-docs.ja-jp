---
title: IDebugCodeContext3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext3 interface
ms.assetid: 524eb882-0ad5-4bfb-95eb-eb3abb3d0237
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 62b84bd77038c7a17b65f764bd303d6a6372a52c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68154166"
---
# <a name="idebugcodecontext3"></a>IDebugCodeContext3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)インターフェイスを拡張して、モジュールインターフェイスとプロセスインターフェイスを取得できるようにします。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugCodeContext3 : IDebugCodeContext2  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジンによって実装され、デバッグパッケージによって使用さ [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] れます。  
  
## <a name="methods"></a>メソッド  
 このインターフェイスには、インターフェイスのメソッドに加えて、 `IDebugCodeContext2` 次のメソッドが実装されています。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetModule](../../../extensibility/debugger/reference/idebugcodecontext3-getmodule.md)|デバッグモジュールのインターフェイスへの参照を取得します。|  
|[GetProcess](../../../extensibility/debugger/reference/idebugcodecontext3-getprocess.md)|デバッグプロセスのインターフェイスへの参照を取得します。|  
  
## <a name="remarks"></a>注釈  
 これは省略可能なインターフェイスであり、通常は実装する必要はありません。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
