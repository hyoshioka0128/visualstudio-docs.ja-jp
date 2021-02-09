---
title: 'IDebugFunctionPosition2:: GetOffset |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionPosition2::GetOffset
helpviewer_keywords:
- IDebugFunctionPosition2::GetOffset
ms.assetid: 60943782-aec7-4be2-b222-1984ed53a543
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 29f883af8f048a38320a49493257354ad3b60188
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99929837"
---
# <a name="idebugfunctionposition2getoffset"></a>IDebugFunctionPosition2::GetOffset
ソースドキュメント内の関数の位置を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetOffset( 
   TEXT_POSITION* pPosition
);
```

```csharp
int GetOffset(
   TEXT_POSITION[] pPosition
);
```

## <a name="parameters"></a>パラメーター
`pPosition`\
[入力、出力]ドキュメント内の関数の位置を使用して入力される [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
