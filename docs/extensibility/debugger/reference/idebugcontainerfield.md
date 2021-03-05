---
description: このインターフェイスは、他のシンボルまたは型のコンテナーであるシンボルまたは型を表します。
title: IDebugContainerField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField
helpviewer_keywords:
- IDebugContainerField interface
ms.assetid: a8bbe061-c382-4fe9-a193-3f7d12216041
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 752eb7d77035a25ad1d0ddc8aec45afe95d898c7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154783"
---
# <a name="idebugcontainerfield"></a>IDebugContainerField
このインターフェイスは、他のシンボルまたは型のコンテナーであるシンボルまたは型を表します。

## <a name="syntax"></a>構文

```
IDebugContainerField : IDebugField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボルプロバイダーは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、コンテナーを表すすべてのインターフェイスの基本クラスでもあります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 多くのインターフェイスの多くのメソッドは、このインターフェイスを返します。 これはすべてのコンテナーの基本クラスであるため、 [QueryInterface](/cpp/atl/queryinterface)を使用して、このインターフェイスからより特殊化されたインターフェイスを取得できます。 このようなインターフェイスには、 [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)、 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)、 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)、 [IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)などがあります。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)|コンテナーのフィールドの列挙子を作成します。|

## <a name="remarks"></a>解説
 配列 (変数のコンテナー)、クラス (メソッドと変数のコンテナー)、およびメソッド (パラメーターとローカル変数のコンテナー) はすべて、コンテナーの例です。

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
