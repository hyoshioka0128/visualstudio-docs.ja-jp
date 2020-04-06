---
title: Iデバッグダイナミックフィールド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDynamicField
helpviewer_keywords:
- IDebugDynamicField interface
ms.assetid: caffbd95-7596-4714-84b1-b964e89a78bb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 15f0ddf70849377d37ec74839550de6057b3450c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731319"
---
# <a name="idebugdynamicfield"></a>IDebugDynamicField
このインターフェイスは、変数の型を表します。

## <a name="syntax"></a>構文

```
IDebugDynamicField : IDebugField
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、実行時に決定できる任意の型の基本クラスとしてシンボル プロバイダーによって実装されます。 これはマネージ コード専用です。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、より特化されたインターフェイスを派生させることができる基本クラスを表します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 このインターフェイスは、 から`IDebugField`継承されたメソッド以外のメソッドを提供しません。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
