---
title: IDebugObject2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 979ede5601f1f31ca972bb9067b626954b1296f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695209"
---
# <a name="idebugobject2"></a>IDebugObject2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 このインターフェイスは、オブジェクトに関する追加情報を提供します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugObject2 : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 式エバリュエーターは、このインターフェイスを実装して、エイリアスと、オブジェクトに関する情報へのアクセスをサポートします。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスは、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を使用してこのインターフェイスを取得できます。 また、このインターフェイスは [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md) によって返されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 インターフェイスには、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスのメソッドに加えて、 `IDebugObject2` 次のものが実装されています。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|このオブジェクトによって表されるプロパティをバッキングしている可能性のあるフィールドまたは変数 (存在する場合) を取得します。|  
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|このオブジェクトの値を表すマネージコードオブジェクトを取得します。|  
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|このオブジェクトの一意の ID を作成するか、既存のエイリアスを返します。|  
|[GetAlias](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|このオブジェクトに関連付けられているエイリアス (存在する場合) を取得します。|  
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|このオブジェクトの型を取得します。|  
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|このオブジェクトがユーザーデータを表すかどうかを判断します。|  
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|エディットコンティニュの状態が無効になっているかどうかを判断します。<br /><br /> カスタム式エバリュエーターは、このメソッドを実装していません (常にを返す必要があり `E_NOTIMPL` ます)。|  
  
## <a name="remarks"></a>注釈  
 エイリアスの詳細については、「 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 」を参照してください。  
  
## <a name="requirements"></a>要件  
 ヘッダー: ee  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [式の評価インターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)   
 [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)
