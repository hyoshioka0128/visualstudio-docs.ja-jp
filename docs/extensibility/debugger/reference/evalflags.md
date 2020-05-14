---
title: エバルフラッグス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVALFLAGS
helpviewer_keywords:
- EVALFLAGS enumeration
ms.assetid: 7b2cb14a-511a-4fef-9e4f-308139719fba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4136726e5c8b798121dbd38975d8f2bb935ed04a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737116"
---
# <a name="evalflags"></a>EVALFLAGS
式の評価を制御するフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
};
typedef DWORD EVALFLAGS;
```

```csharp
public enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
}
```

## <a name="fields"></a>フィールド
`EVAL_RETURNVALUE`\
戻り値がある場合は評価されることを指定します。

`EVAL_NOSIDEEFFECTS`\
副作用を許可しないことを指定します。

`EVAL_ALLOWBPS`\
ブレークポイントで停止を指定します。

`EVAL_ALLOWERRORREPORT`\
許可するホストへのエラー報告を指定します。 主に、Internet Explorer のスクリプトで式の評価に使用されます。

`EVAL_FUNCTION_AS_ADDRESS`\
関数を呼び出すのではなく、関数をアドレスとして評価するように強制します。

`EVAL_NOFUNCEVAL`\
関数が評価されないようにします。 たとえば、 式`int``myExpression(int) + 10`のトークンを考えてみましょう。 この関数は、アドレスとして正しく評価できますが、値としては評価できません。

`EVAL_NOEVENTS`\
式の評価中に発生したイベントをセッションデバッグ マネージャー (SDM) または IDE に送信しないことを示すフラグ。

## <a name="remarks"></a>Remarks
これらのフラグは、引数として渡されます、[評価 Async](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)メソッドと[評価同期](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)メソッドです。

これらのフラグはビットごとの OR と組み合わせられます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
