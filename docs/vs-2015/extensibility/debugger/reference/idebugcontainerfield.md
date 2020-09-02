---
title: IDebugContainerField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugContainerField
helpviewer_keywords:
- IDebugContainerField interface
ms.assetid: a8bbe061-c382-4fe9-a193-3f7d12216041
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2656d3f5a3313a4538e3e0e6454dd671da635904
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686972"
---
# <a name="idebugcontainerfield"></a>IDebugContainerField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、他のシンボルまたは型のコンテナーであるシンボルまたは型を表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugContainerField : IDebugField  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 シンボルプロバイダーは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、コンテナーを表すすべてのインターフェイスの基本クラスでもあります。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 多くのインターフェイスの多くのメソッドは、このインターフェイスを返します。 これはすべてのコンテナーの基本クラスであるため、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を使用して、このインターフェイスからより特殊化されたインターフェイスを取得できます。 このようなインターフェイスには、 [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)、 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)、 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)、 [IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)などがあります。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 このインターフェイスは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)|コンテナーのフィールドの列挙子を作成します。|  
  
## <a name="remarks"></a>注釈  
 配列 (変数のコンテナー)、クラス (メソッドと変数のコンテナー)、およびメソッド (パラメーターとローカル変数のコンテナー) はすべて、コンテナーの例です。  
  
## <a name="requirements"></a>要件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [シンボルプロバイダーインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
