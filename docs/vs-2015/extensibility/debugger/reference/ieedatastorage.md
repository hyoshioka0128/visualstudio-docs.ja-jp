---
title: IEEDataStorage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEEDataStorage
helpviewer_keywords:
- IEEDataStorage interface
ms.assetid: 704e932d-2325-410e-89c4-ce88c6ec19da
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ad398380c7c951b99e7d84283355ee9d31955173
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704731"
---
# <a name="ieedatastorage"></a>IEEDataStorage
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、バイトの配列を表します。  
  
## <a name="syntax"></a>構文  
  
```  
IEEDataStorage : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 式エバリュエーター (EE) は、バイトの配列を表すために、このインターフェイスを実装します ( [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスを使用してデータを取得および変更するために型ビジュアライザーによって使用されます)。 EE は、通常、外部型ビジュアライザーをサポートするために、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 インターフェイスのメソッドは `IPropertyProxyEESide` すべて、このインターフェイスを返します。 [Getpropertyproxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)を呼び出して、 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)インターフェイスを取得します。 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスで[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を呼び出して、 [IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)インターフェイスを取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 インターフェイスには `IEEDataStorage` 、次のメソッドが実装されています。  
  
|Method|説明|  
|------------|-----------------|  
|[GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)|指定したバッファーに、指定したデータバイト数を取得します。|  
|[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)|使用可能なデータバイト数を取得します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスは、特定のオブジェクトによって保持されているデータにアクセスするために、型ビジュアライザーによって使用されます。 データはバイト配列として扱われます。これにより、型ビジュアライザーは、このデータをユーザーに提示するために必要な任意の方法で操作できます。  
  
 カスタムビューアーでは、必要に応じてこのインターフェイスを使用することもできますが、通常はカスタムビューアーでカスタムインターフェイス、 [Getmemorybytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) 、または [getmemorybytes](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md) (文字列指向データ用) を使用します。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)   
 [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
