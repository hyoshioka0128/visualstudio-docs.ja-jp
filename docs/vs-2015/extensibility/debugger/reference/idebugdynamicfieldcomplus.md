---
title: IDebugDynamicFieldCOMPlus |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugDynamicFieldCOMPlus interface
ms.assetid: c3a25f27-327a-4bdb-b026-27d436ddcd0c
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 71756b4c4df0768520f72219cf50e5407604635d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198499"
---
# <a name="idebugdynamicfieldcomplus"></a>IDebugDynamicFieldCOMPlus
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)オブジェクトの動的フィールドを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugDynamicFieldCOMPlus : IDebugDynamicField  
```  
  
## <a name="methods"></a>メソッド  
 このインターフェイスは、 [IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetTypeFromPrimitive](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromprimitive.md)|プリミティブ型を指定して型を取得します。|  
|[GetTypeFromTypeDef](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromtypedef.md)|トークンを指定して型を取得します。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: Sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
