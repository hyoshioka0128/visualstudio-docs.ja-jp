---
title: フィールド::列挙体のローカルマイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08872160860d0d442f9807705dea70190dff9b28
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727207"
---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
メソッドの選択したローカル変数の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumLocals(
    IDebugAddress*     pAddress,
    IEnumDebugFields** ppLocals
);
```

```csharp
int EnumLocals(
    IDebugAddress        pAddress,
    out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
[in]ローカルの取得元のコンテキストまたはスコープを選択するデバッグ アドレスを表す[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)オブジェクト。

`ppLocals`\
[アウト]ローカルの[一](../../../extensibility/debugger/reference/ienumdebugfields.md)覧を表すオブジェクトを返します。それ以外の場合は、ローカルがない場合は null 値を返します。

## <a name="return-value"></a>戻り値
成功した場合は、S_OKを返すか、ローカルがない場合はS_FALSEを返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
指定されたデバッグ アドレスを含むブロック内で定義されている変数のみが列挙されます。 コンパイラで生成されたローカルを含むすべてのローカル変数が必要な場合は[、EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)メソッドを呼び出します。

メソッドには、複数のスコープ コンテキストまたはブロックを含めることができます。 たとえば、次の工夫されたメソッドには、2 つの内部ブロックとメソッド本体自体の 3 つのスコープが含まれています。

```csharp
public void func(int index)
{
    // Method body scope
    int a = 0;
    if (index == 1)
    {
        // Inner scope 1
        int temp1 = a;
    }
    else
    {
        // Inner scope 2
        int temp2 = a;
    }
}
```

オブジェクト[はメソッド](../../../extensibility/debugger/reference/idebugmethodfield.md)自体を`func`表します。 `EnumLocals` IDebugAddress を[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)アドレスに設定してメソッドを`Inner Scope 1`呼び出すと、変数`temp1`を含む列挙型が返されます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
