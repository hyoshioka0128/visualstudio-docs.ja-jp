---
description: この構造体は、モジュールのジャスト Mycode 情報を設定するために使用されます。
title: JMC_CODE_SPEC |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- JMC_CODE_SPEC
helpviewer_keywords:
- JMC_CODE_SPEC structure
ms.assetid: d89498f1-4234-46d9-b4e2-abbcbca5068a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6c862a2897b45d89f95963ce7adfe2da8d4d350f
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225566"
---
# <a name="jmc_code_spec"></a>JMC_CODE_SPEC
この構造体は、モジュールのジャスト Mycode 情報を設定するために使用されます。

## <a name="syntax"></a>構文

```cpp
typedef struct _JMC_CODE_SPEC {
    BOOL fIsUserCode;
    BSTR bstrModuleName;
} JMC_CODE_SPEC;
```

```csharp
public struct JMC_CODE_SPEC {
    public int    fIsUserCode;
    public string bstrModuleName;
};
```

## <a name="members"></a>メンバー
`fIsUserCode`\
`TRUE`モジュールがユーザーコードと見なされる場合は0以外 ()。それ以外の場合は、 `FALSE` モジュールが外部コードとして扱われ、デバッグされない場合は 0 ()。

`bstrModuleName`\
対象のモジュールの名前。

## <a name="remarks"></a>解説
この構造体は、 [Setジャスト Mycodestate](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md) メソッドにそのような構造体のリストとして渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)
