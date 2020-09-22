---
title: IDebugAlias |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAlias
helpviewer_keywords:
- IDebugAlias interface
ms.assetid: 3cc4c9a4-7805-4239-b00e-eb4a024f3c55
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6c05b6987804681176abdde0e8c94a7463a9163c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841640"
---
# <a name="idebugalias"></a>IDebugAlias
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 変数の数値の別名を表します。 別名は、単に変数の異なる名前です。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugAlias : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 式エバリュエーター (EE) は、変数の数値のエイリアスをサポートするために、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [Createalias](../../../extensibility/debugger/reference/idebugobject2-createalias.md) は、特定のオブジェクトの別名を作成します。 エイリアスを検索するには、 [Findalias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md) または [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)を使用します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 インターフェイスでは、次のメソッドが定義されてい `IDebugAlias` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)|このエイリアスが参照するオブジェクトを取得します。|  
|[GetName](../../../extensibility/debugger/reference/idebugalias-getname.md)|エイリアス名を取得します。|  
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugalias-geticordebugvalue.md)|`ICorDebugValue`このオブジェクトに関するマネージコード情報へのアクセスを提供するインターフェイスを取得します (マネージコードのみ)。|  
|[Dispose](../../../extensibility/debugger/reference/idebugalias-dispose.md)|このエイリアスは使用されなくなったものとしてマークします。|  
  
## <a name="remarks"></a>注釈  
 エイリアスは、文字列形式の10進数の後に # 文字が続きます (たとえば、1001 #)。  
  
## <a name="requirements"></a>要件  
 ヘッダー: ee  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [式の評価インターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)   
 [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)   
 [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)
