---
title: 'IDebugFunctionObject2:: CreateStringObjectWithLength |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CreateStringObjectWithLength
- IDebugFunctionObject2::CreateStringObjectWithLength
ms.assetid: 1f43ec66-1615-4a4c-8b9d-e933f549f96d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6dd46d7cc2d142b3c62ab7b1b2b9eb65b92d6754
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921036"
---
# <a name="idebugfunctionobject2createstringobjectwithlength"></a>IDebugFunctionObject2::CreateStringObjectWithLength
指定された長さの文字列オブジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateStringObjectWithLength (
   LPCOLESTR      pcstrString,
   UINT           uiLength,
   IDebugObject** ppObject
);
```

```csharp
int CreateStringObjectWithLength (
   string           pcstrString,
   uint             uiLength,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`pcstrString`\
から文字列オブジェクトの文字列値。

`uiLength`\
から文字列の長さ (バイト単位)。

`ppObject`\
入出力新しく作成された文字列オブジェクトを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
