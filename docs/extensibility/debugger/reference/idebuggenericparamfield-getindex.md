---
title: を使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericParamField::GetIndex
ms.assetid: 8e0bdb26-1247-44d9-8d80-ec6e35187fb4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6b31acd57685058795186fcecb73164218d5ad15
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727987"
---
# <a name="idebuggenericparamfieldgetindex"></a>IDebugGenericParamField::GetIndex
このジェネリック パラメーターのインデックスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetIndex(
    DWORD* pIndex
);
```

```csharp
int GetIndex(
    out uint pIndex
);
```

## <a name="parameters"></a>パラメーター
`pIndex`\
[アウト]このジェネリック パラメーターのインデックス値。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
例えば、辞書(K,V)の場合、Kはインデックス0、Vはインデックス1です。

## <a name="example"></a>例
インターフェイスを公開する**オブジェクト**に対してこの[メソッドを実装](../../../extensibility/debugger/reference/idebuggenericparamfield.md)する方法を次の例に示します。

```cpp
HRESULT CDebugGenericParamFieldType::GetIndex(DWORD* pIndex)
{
    HRESULT hr = S_OK;

    METHOD_ENTRY( CDebugGenericParamFieldType::GetIndex );

    IfFalseGo(pIndex, E_INVALIDARG );
    IfFailGo( this->LoadProps() );
    *pIndex = m_index;

Error:

    METHOD_EXIT( CDebugGenericParamFieldType::GetIndex, hr );
    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)
