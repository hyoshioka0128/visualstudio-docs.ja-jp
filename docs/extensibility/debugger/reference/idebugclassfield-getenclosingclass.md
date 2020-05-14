---
title: Iデバッグクラスフィールド::ゲットエンクロージングクラス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::GetEnclosingClass
helpviewer_keywords:
- IDebugClassField::GetEnclosingClass method
ms.assetid: a0c12e3c-9ea0-4dfb-9e45-8cea18725022
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e5a68e32da370d6881eb2b74cbca157f7b899329
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734395"
---
# <a name="idebugclassfieldgetenclosingclass"></a>IDebugClassField::GetEnclosingClass
このクラスを囲むクラスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEnclosingClass(
    IDebugClassField** ppClassField
);
```

```csharp
int GetEnclosingClass(
    out IDebugClassField ppClassField
);
```

## <a name="parameters"></a>パラメーター
`ppClassField`\
[アウト]外側の[クラス](../../../extensibility/debugger/reference/idebugclassfield.md)を表すオブジェクトを返します。 外側のクラスがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
この[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)オブジェクトによって表されるクラスが入れ子になったクラスである`ppClassField`場合、パラメーター`IDebugClassField`は外側のクラスを表すオブジェクトを返します。 たとえば、次のクラス定義を指定します。

```
class RootClass {
    class NestedClass { }
};
```

クラスを`GetEnclosingClass``IDebugClassField`表すオブジェクトのメソッドを呼`NestedClass`び出すと`IDebugClassField`、 クラス`RootClass`を表すオブジェクトが返されます。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
