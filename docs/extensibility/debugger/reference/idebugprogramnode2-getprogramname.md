---
title: プログラムノード2::プログラム名を取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetProgramName
helpviewer_keywords:
- IDebugProgramNode2::GetProgramName
ms.assetid: 510c7f5d-48ff-4d9f-ad79-fbad9f15239d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9af930716725a62fff5ea3d1635b506b06b26086
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721988"
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
[アウト]プログラムの名前を返します。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
プログラムの名前はプログラムのパスと同じものではありませんが、プログラムの名前は、このようなパスの一部である場合があります。

## <a name="example"></a>例
次の例は[、IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイス`CProgram`を実装する単純なオブジェクトに対してこのメソッドを実装する方法を示しています。 この`MakeBstr`関数は、指定された文字列のコピーを BSTR として割り当てます。

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
