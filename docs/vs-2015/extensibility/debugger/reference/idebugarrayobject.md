---
title: IDebugArrayObject |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayObject
helpviewer_keywords:
- IDebugArrayObject method
ms.assetid: a1c8e77e-dee1-4748-a516-6ab032a8f54f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f8ec4c883078663d0e252d6a04ae7441f12f31d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686985"
---
# <a name="idebugarrayobject"></a>IDebugArrayObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 このインターフェイスは、配列オブジェクトを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugArrayObject : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 式エバリュエーターは、配列を表すためにこのインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスは、オブジェクトが配列を表す場合、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を使用してこのインターフェイスを取得できます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 インターフェイスのメソッドに加えて `IDebugObject` 、次のメソッドがインターフェイスに実装され `IDebugArrayObject` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)|配列内の要素の数を取得します。|  
|[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)|配列の要素を取得します。|  
|[GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)|配列のすべての要素を取得します。|  
|[GetRank](../../../extensibility/debugger/reference/idebugarrayobject-getrank.md)|配列のランクを取得します。|  
|[GetDimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)|配列の次元を取得します。|  
  
## <a name="remarks"></a>注釈  
 式エバリュエーターは、このインターフェイスを使用して、解析ツリー内の配列を表します。  
  
## <a name="requirements"></a>要件  
 ヘッダー: ee  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
