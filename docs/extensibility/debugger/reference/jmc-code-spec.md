---
title: JMC_CODE_SPEC |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- JMC_CODE_SPEC
helpviewer_keywords:
- JMC_CODE_SPEC structure
ms.assetid: d89498f1-4234-46d9-b4e2-abbcbca5068a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0a6746ed0df400efc7feb3fb541c57c88f78cc2c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714741"
---
# <a name="jmc_code_spec"></a>JMC_CODE_SPEC
この構造体は、モジュールの JustMyCode 情報を設定するために使用されます。

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
モジュールをユーザー`TRUE`コードと見なす場合は、非ゼロ ( ) 。それ以外の場合`FALSE`は、モジュールが外部コードとして扱われ、デバッグされない場合は、ゼロ ( ) 。

`bstrModuleName`\
問題のモジュールの名前。

## <a name="remarks"></a>Remarks
この構造体は、このような構造体のリストとして[メソッド](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)に渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)
