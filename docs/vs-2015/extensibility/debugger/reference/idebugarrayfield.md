---
title: IDebugArrayField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayField
helpviewer_keywords:
- IDebugArrayField interface
ms.assetid: 9667b0a5-4295-46cc-9388-b75c1350be15
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 20d5df8df3e556f0908668b98a836cbedbbce47e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686999"
---
# <a name="idebugarrayfield"></a>IDebugArrayField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、配列のシンボルまたは型を表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugArrayField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 シンボルプロバイダーは、 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、配列オブジェクトを表す特殊化です。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md)がフラグを返す場合は、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を使用して、 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスからこのインターフェイスを取得し `FIELD_TYPE_ARRAY` ます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 このインターフェイスは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスと [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスのメソッドに加えて、次のものを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetNumberOfElements](../../../extensibility/debugger/reference/idebugarrayfield-getnumberofelements.md)|配列内の要素の数を取得します。|  
|[GetElementType](../../../extensibility/debugger/reference/idebugarrayfield-getelementtype.md)|配列内の要素の型を取得します。|  
|[GetRank](../../../extensibility/debugger/reference/idebugarrayfield-getrank.md)|配列のランクを取得します。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [シンボルプロバイダーインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
