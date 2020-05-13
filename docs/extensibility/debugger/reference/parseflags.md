---
title: パースフラグ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PARSEFLAGS
helpviewer_keywords:
- PARSEFLAGS enumeration
ms.assetid: 47943f0a-54cb-4493-a62e-5dba97bd4c35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0cc70fdd9fe1279e4d419a422b970eb3d3b07c65
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714119"
---
# <a name="parseflags"></a>PARSEFLAGS
式を解析する方法を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
typedef DWORD PARSEFLAGS;
```

```csharp
public enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
```

## <a name="fields"></a>フィールド
 `PARSE_EXPRESSION`\
 式がステートメントではないことを示します。

 `PARSE_FUNCTION_AS_ADDRESS`\
 式をアドレスとして解析 (後で評価) することを示します。

 `PARSE_DESIGN_TIME_EXPR_EVAL`\
 デザイン時 (デザイナーが開いている場合) に式が解析されることを示します。

## <a name="remarks"></a>Remarks
 パラメーターとして渡されます、 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)メソッドと[解析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)メソッド。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [解析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
