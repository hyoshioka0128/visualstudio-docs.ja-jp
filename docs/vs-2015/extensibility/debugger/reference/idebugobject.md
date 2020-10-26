---
title: IDebugObject |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c179a4443c23373fb92adf522ee0af34acb19c3f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695267"
---
# <a name="idebugobject"></a>IDebugObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 このインターフェイスは、シンボルと式の値をカプセル化するためにバインダーによって作成されるオブジェクトを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugObject : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 式エバリュエーターは、このインターフェイスを実装してオブジェクトを表します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスは、解析された式で式エバリュエーターが使用するすべてのオブジェクトの基本クラスです。 これは、 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md) メソッドの呼び出しによって返されます。 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) は、このインターフェイスからより特殊化されたインターフェイスを取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugObject` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|オブジェクトのサイズを取得します。|  
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|オブジェクトの値を連続する一連のバイトとして取得します。|  
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|オブジェクトの値を連続する一連のバイトから設定します。|  
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|このオブジェクトの参照値を設定します。|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|オブジェクトの値のアドレスを表すメモリコンテキストを取得します。|  
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|デバッグエンジンのアドレス空間にマネージオブジェクトのコピーを作成します。|  
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|このオブジェクトが null 参照であるかどうかをテストします。|  
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|オブジェクトとこのオブジェクトを比較します。|  
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|このオブジェクトが読み取り専用かどうかを判断します。|  
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|オブジェクトが透過プロキシかどうかを判断します。|  
  
## <a name="remarks"></a>注釈  
 式エバリュエーターは、このインターフェイスを基底クラスとして使用して、解析ツリー内のオブジェクトを表します。  
  
## <a name="requirements"></a>要件  
 ヘッダー: ee  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [式の評価インターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)   
 [束縛](../../../extensibility/debugger/reference/idebugbinder-bind.md)
