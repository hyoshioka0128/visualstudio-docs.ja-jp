---
title: を指定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElement
helpviewer_keywords:
- IDebugArrayObject::GetElement method
ms.assetid: 08b44341-7bf1-4a8c-8b79-98ae5785b195
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e29fe09905119057224b45b455e4f56e5ce904af
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736174"
---
# <a name="idebugarrayobjectgetelement"></a>IDebugArrayObject::GetElement
配列の要素を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetElement( 
   DWORD          dwIndex,
   IDebugObject** ppElement
);
```

```csharp
int GetElement(
   [In] uint dwIndex,
   out IDebugObject ppElement
);
```

## <a name="parameters"></a>パラメーター
`dwIndex`\
[in]要素のインデックス。

`ppElement`\
[アウト]要素を表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、配列オブジェクトが多次元であっても、配列オブジェクトのすべての要素を 1 次元配列として認識します。 たとえば、`myarray[3][2][6]`配列と`dwIndex`パラメータが 20 の場合、このメソッドは 要素を`myarray[1][1][2]`から返し`dwIndex`、パラメータ 21 は 要素`myarray[1][1][3]`を 返します。 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)メソッドを使用して、配列内の要素の総数を調べます。

## <a name="see-also"></a>関連項目
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
