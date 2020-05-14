---
title: Iデバッグバインダー3::ゲットオールエイリアス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetAllAliases
helpviewer_keywords:
- IDebugBinder3::GetAllAliases method
ms.assetid: 1f9ab2ee-2ab3-4a61-8b99-95dd7fdf3511
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2d512fa6eb7529e11c766d7c173b318aa6f8f2f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735811"
---
# <a name="idebugbinder3getallaliases"></a>IDebugBinder3::GetAllAliases
このメソッドは、プログラムからエイリアスの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAllAliases(
   UINT          uRequest,
   IDebugAlias** ppAliases,
   UINT*         puFetched
);
```

```csharp
int GetAllAliases(
   uint          uRequest,
   IDebugAlias[] ppAliases,
   out uint      puFetched
);
```

## <a name="parameters"></a>パラメーター
`uRequest`\
[in]返すエイリアスの最大数 ( に渡される配列の長さを指定`ppAliases`します)

`ppAliases`\
[イン、アウト]別名を入力する配列 (これが null 値で`uRequest`0 の場合、返すことができるエイリアスの数は によって`puFetched`返されます)。

`puFetched`\
[アウト]取得したエイリアスの数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
