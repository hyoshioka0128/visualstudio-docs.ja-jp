---
title: を指定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetCount
helpviewer_keywords:
- IDebugArrayObject::GetCount method
ms.assetid: 7931f3f7-033c-4bf8-8abd-95183952ebb0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d9d5e322b7bcd5238335c74caa21989f1f1962ce
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736201"
---
# <a name="idebugarrayobjectgetcount"></a>IDebugArrayObject::GetCount
配列内の要素の数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCount( 
   DWORD* pdwElements
);
```

```csharp
int GetCount(
   out uint pdwElements
);
```

## <a name="parameters"></a>パラメーター
`pdwElements`\
[アウト]カウントを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、配列オブジェクトが多次元であっても、配列オブジェクトのすべての要素を 1 次元配列として認識します。 たとえば、配列`myarray[3][2][6]`を指定すると、このメソッドはパラメータの 36`pdwElements`を返します。 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)メソッドを使用して、個々の要素を一度に 1 つずつ取得します。

## <a name="see-also"></a>関連項目
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
