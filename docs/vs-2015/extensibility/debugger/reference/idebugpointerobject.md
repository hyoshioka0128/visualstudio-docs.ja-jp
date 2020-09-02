---
title: IDebugPointerObject |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPointerObject
helpviewer_keywords:
- IDebugPointerObject interface
ms.assetid: 257fa167-b46e-4ffb-9a12-272efbf26702
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4cd84c3580d94491e09ce9e8cde8175f9e437be0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65693396"
---
# <a name="idebugpointerobject"></a>IDebugPointerObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 このインターフェイスは、ポインターオブジェクトを表します。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugPointerObject : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 式エバリュエーターは、このインターフェイスを実装してポインターオブジェクトを表します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 がポインターを表す場合、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスは [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を使用してこのインターフェイスを取得できます `IDebugObject` 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 インターフェイスは、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)から継承されたメソッドに加えて、 `IDebugPointerObject` 次のメソッドを公開します。  
  
|Method|説明|  
|------------|-----------------|  
|[Dereference](../../../extensibility/debugger/reference/idebugpointerobject-dereference.md)|インターフェイスが指すオブジェクトを取得します。|  
|[GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)|インターフェイスが連続する一連のバイトとして指す値を取得します。|  
|[SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)|インターフェイスが連続する一連のバイトを指す値を設定します。|  
  
## <a name="remarks"></a>解説  
 式エバリュエーターは、このインターフェイスを使用して、解析ツリー内のポインターを表します。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: ee  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [式の評価インターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
