---
description: このインターフェイスは、変数の型を表します。
title: IDebugDynamicField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDynamicField
helpviewer_keywords:
- IDebugDynamicField interface
ms.assetid: caffbd95-7596-4714-84b1-b964e89a78bb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dcf148294a7c18c2b717bb4de63dac7e656e25d6
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167231"
---
# <a name="idebugdynamicfield"></a>IDebugDynamicField
このインターフェイスは、変数の型を表します。

## <a name="syntax"></a>構文

```
IDebugDynamicField : IDebugField
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、実行時に決定できる任意の型の基本クラスとしてシンボルプロバイダーによって実装されます。 これはマネージコードのみです。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、より特殊化されたインターフェイスの派生元となる基底クラスを表します。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスは、から継承されたメソッド以外のメソッドを提供しません `IDebugField` 。

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
