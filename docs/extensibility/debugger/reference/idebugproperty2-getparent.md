---
title: プロパティ 2::ゲットペアレント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetParent
helpviewer_keywords:
- IDebugProperty2::GetParent
ms.assetid: 58780469-fe25-4d84-9187-67940ca0767f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7620c22d425a0426daa8c15d067a4d61c6bf96e2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721423"
---
# <a name="idebugproperty2getparent"></a>IDebugProperty2::GetParent
プロパティの親プロパティを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetParent ( 
   IDebugProperty2** ppParent
);
```

```csharp
int GetParent ( 
   out IDebugProperty2 ppParent
);
```

## <a name="parameters"></a>パラメーター
`ppParent`\
[アウト]プロパティの親を表す[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 親が存在しない場合は `S_GETPARENT_NO_PARENT` を返します。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
