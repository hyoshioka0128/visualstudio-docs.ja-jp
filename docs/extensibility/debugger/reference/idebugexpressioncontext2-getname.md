---
title: 'IDebugExpressionContext2:: GetName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2::GetName
helpviewer_keywords:
- IDebugExpressionContext2::GetName
ms.assetid: c2b70d22-17af-4986-a7e3-930910367216
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8529e83de0f5de3d5d202885cf37b29d21fa3e59
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949533"
---
# <a name="idebugexpressioncontext2getname"></a>IDebugExpressionContext2::GetName
評価コンテキストの名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetName( 
   BSTR* pbstrName
);
```

```csharp
int GetName( 
   out string pbstrName
);
```

## <a name="parameters"></a>パラメーター
`pbstrName`\
入出力評価コンテキストの名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 名前は、この評価コンテキストの説明です。 通常は、この正確な評価コンテキストを参照する式エバリュエーターによって解析できるものです。 たとえば、C++ では、名前は次のようになります。

```
"{ function-name, source-file-name, module-file-name }"
```

## <a name="see-also"></a>関連項目
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
