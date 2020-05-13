---
title: Iデバッグクラスフィールド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField
helpviewer_keywords:
- IDebugClassField interface
ms.assetid: 49358cbc-8973-4862-9dcc-79b1248e6712
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11b0e4cd7c851e65edf299f45ec97273804c25d8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734287"
---
# <a name="idebugclassfield"></a>IDebugClassField
このインターフェイスは、クラスを型として表します。

## <a name="syntax"></a>構文

```
IDebugClassField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは[、IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、クラス型を表す特殊化です。

## <a name="notes-for-callers"></a>発信者向けのメモ
 多くのインターフェイス[には、](../../../extensibility/debugger/reference/idebugmethodfield.md)[この](../../../extensibility/debugger/reference/idebugsymbolprovider.md)インターフェイスを返すことができるメソッド[があります。](../../../extensibility/debugger/reference/idebugcustomattribute.md) また[、GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) `FIELD_TYPE_CLASS`メソッドが[フラグを返](../../../extensibility/debugger/reference/idebugcontainerfield.md)す場合は、インターフェイスからこのインターフェイスを取得するのには[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスのメソッドに加えて、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)[このインターフェイスは](../../../extensibility/debugger/reference/idebugcontainerfield.md)、次を実装します。

|Method|説明|
|------------|-----------------|
|[EnumBaseClasses](../../../extensibility/debugger/reference/idebugclassfield-enumbaseclasses.md)|このクラスの基本クラスの列挙子を作成します。|
|[DoesInterfaceExist](../../../extensibility/debugger/reference/idebugclassfield-doesinterfaceexist.md)|特定のインターフェイスがクラスで定義されているかどうかを判断します。|
|[EnumNestedClasses](../../../extensibility/debugger/reference/idebugclassfield-enumnestedclasses.md)|このクラスの入れ子になったクラスの列挙子を作成します。|
|[GetEnclosingClass](../../../extensibility/debugger/reference/idebugclassfield-getenclosingclass.md)|このクラスを囲むクラスを取得します。|
|[EnumInterfacesImplemented](../../../extensibility/debugger/reference/idebugclassfield-enuminterfacesimplemented.md)|このクラスによって実装されるインターフェイスの列挙子を作成します。|
|[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)|このクラスのコンストラクターの列挙子を作成します。|
|[GetDefaultIndexer](../../../extensibility/debugger/reference/idebugclassfield-getdefaultindexer.md)|既定のインデクサーの名前を取得します。|
|[EnumNestedEnums](../../../extensibility/debugger/reference/idebugclassfield-enumnestedenums.md)|このクラスの入れ子になった列挙子の列挙子を作成します。|

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
