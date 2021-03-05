---
description: 'IDebugProgramNode2:: GetProgramName プログラムの名前を取得します。'
title: 'IDebugProgramNode2:: GetProgramName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetProgramName
helpviewer_keywords:
- IDebugProgramNode2::GetProgramName
ms.assetid: 510c7f5d-48ff-4d9f-ad79-fbad9f15239d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 88a4bc58f5d91cdb52482f4dc862446cfc9e7eb1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161386"
---
# <a name="idebugprogramnode2getprogramname"></a>IDebugProgramNode2::GetProgramName
プログラムの名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProgramName (
    BSTR* pbstrProgramName
);
```

```csharp
int GetProgramName (
    out string pbstrProgramName
);
```

## <a name="parameters"></a>パラメーター
`pbstrProgramName`\
入出力プログラムの名前を返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
プログラムの名前は、プログラムのパスと同じではありませんが、プログラムの名前はそのようなパスの一部である場合があります。

## <a name="example"></a>例
次の例は、IDebugProgramNode2 インターフェイスを実装する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CProgram` います。 [](../../../extensibility/debugger/reference/idebugprogramnode2.md) 関数は、 `MakeBstr` 指定された文字列のコピーを BSTR として割り当てます。

```cpp
HRESULT CProgram::GetProgramName(BSTR* pbstrProgramName) {
    if (!pbstrProgramName)
        return E_INVALIDARG;

    // Assign the member program name to the passed program name.
    *pbstrProgramName = MakeBstr(m_pszProgramName);
    return NOERROR;
}
```

## <a name="see-also"></a>関連項目
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
