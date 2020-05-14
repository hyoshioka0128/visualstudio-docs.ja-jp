---
title: フィールドを使用する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField
helpviewer_keywords:
- IDebugContainerField interface
ms.assetid: a8bbe061-c382-4fe9-a193-3f7d12216041
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a72296517a64c6dcfcb8e347fb00588504aa75a4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733207"
---
# <a name="idebugcontainerfield"></a>IDebugContainerField
このインターフェイスは、他のシンボルまたは型のコンテナーであるシンボルまたは型を表します。

## <a name="syntax"></a>構文

```
IDebugContainerField : IDebugField
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは[、IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、コンテナーを表すすべてのインターフェイスの基本クラスでもあります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 多くのインターフェイスの多くのメソッドは、このインターフェイスを返します。 これはすべてのコンテナの基本クラスであるため、より特化したインターフェイスを使用して[QueryInterface](/cpp/atl/queryinterface)を使用してこのインターフェイスから取得できます。 このようなインターフェイスには、IDebugArrayField、IDebugClassField、IDebugMethodField、および[IDebugPropertyField が](../../../extensibility/debugger/reference/idebugpropertyfield.md)含まれます。 [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md) [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [インターフェイス](../../../extensibility/debugger/reference/idebugfield.md)のメソッドに加えて、このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)|コンテナーのフィールドの列挙子を作成します。|

## <a name="remarks"></a>Remarks
 配列 (変数のコンテナー)、クラス (メソッドと変数のコンテナー) およびメソッド (パラメーターとローカル変数のコンテナー) はすべてコンテナーの例です。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
