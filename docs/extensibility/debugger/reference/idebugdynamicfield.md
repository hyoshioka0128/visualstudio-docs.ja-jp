---
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
ms.openlocfilehash: 6cd81f393b81adb37059106e2d56fd4a3bf2c461
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921160"
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

## <a name="requirements"></a>要件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
