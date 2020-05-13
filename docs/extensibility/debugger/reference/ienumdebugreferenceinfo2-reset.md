---
title: 2::リセット |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2::Reset
helpviewer_keywords:
- IEnumDebugReferenceInfo2::Reset
ms.assetid: cf8ce649-5ce1-44a6-9d5a-89760021bde4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 06d22f9b183352314c7554da9481290328a3865e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715304"
---
# <a name="ienumdebugreferenceinfo2reset"></a>IEnumDebugReferenceInfo2::Reset
列挙を最初の要素にリセットします。

## <a name="syntax"></a>構文

```cpp
HRESULT Reset(
   void
);
```

```csharp
int Reset();
```

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドが呼び出されると[、Next](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-next.md)メソッドの次の呼び出しは、列挙体の最初の要素を返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
