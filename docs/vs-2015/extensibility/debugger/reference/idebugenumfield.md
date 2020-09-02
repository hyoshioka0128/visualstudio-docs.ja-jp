---
title: IDebugEnumField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEnumField
helpviewer_keywords:
- IDebugEnumField interface
ms.assetid: 42f685bf-0f39-47f4-98b0-6022efe2bf97
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ac993e3a4676f1c84a193ddbf6e9a3b5bc8fa235
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65676515"
---
# <a name="idebugenumfield"></a>IDebugEnumField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、列挙型を表します。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugEnumField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 シンボルプロバイダーは、このインターフェイスを実装して列挙体を表します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md)がを返す場合は、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を使用して、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスからこのインターフェイスを取得し `FIELD_TYPE_ENUM` ます。  
  
## <a name="methods-in-vtable-order"></a>VTable の順序でのメソッド  
 インターフェイスおよびインターフェイスのメソッドに加え `IDebugField` て `IDebugContainerField` 、このインターフェイスは次のメソッドを実装します。  
  
|Method|説明|  
|------------|-----------------|  
|[GetUnderlyingSymbol](../../../extensibility/debugger/reference/idebugenumfield-getunderlyingsymbol.md)|この列挙型の名前を記述する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を返します。|  
|[GetStringFromValue](../../../extensibility/debugger/reference/idebugenumfield-getstringfromvalue.md)|指定された値に関連付けられている列挙定数の名前を返します。|  
|[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)|指定した列挙定数名に関連付けられている値を返します。|  
|[GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)|指定した列挙定数名に関連付けられている値を返しますが、大文字と小文字は区別しません。|  
  
## <a name="remarks"></a>解説  
 これは、 [バインド](../../../extensibility/debugger/reference/idebugbinder-bind.md)がある場所に実際にバインドされている、基になるシンボルです。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [シンボルプロバイダーインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)   
 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)
