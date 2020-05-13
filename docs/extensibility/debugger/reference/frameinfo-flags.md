---
title: FRAMEINFO_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO_FLAGS
helpviewer_keywords:
- FRAMEINFO_FLAGS enumeration
ms.assetid: 41578062-8455-412a-9d8b-1e1e9dc8d52e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3510726400623c5ddf3e7a4d58a4903763b91245
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736803"
---
# <a name="frameinfo_flags"></a>FRAMEINFO_FLAGS
スタック フレーム オブジェクトに関して取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_FRAMEINFO_FLAGS {
    FIF_FUNCNAME              = 0x00000001,
    FIF_RETURNTYPE            = 0x00000002,
    FIF_ARGS                  = 0x00000004,
    FIF_LANGUAGE              = 0x00000008,
    FIF_MODULE                = 0x00000010,
    FIF_STACKRANGE            = 0x00000020,
    FIF_FRAME                 = 0x00000040,
    FIF_DEBUGINFO             = 0x00000080,
    FIF_STALECODE             = 0x00000100,
    FIF_ANNOTATEDFRAME        = 0x00000200,
    FIF_DEBUG_MODULEP         = 0x00000400,
    FIF_FUNCNAME_FORMAT       = 0x00001000,
    FIF_FUNCNAME_RETURNTYPE   = 0x00002000,
    FIF_FUNCNAME_ARGS         = 0x00004000,
    FIF_FUNCNAME_LANGUAGE     = 0x00008000,
    FIF_FUNCNAME_MODULE       = 0x00010000,
    FIF_FUNCNAME_LINES        = 0x00020000,
    FIF_FUNCNAME_OFFSET       = 0x00040000,
    FIF_FUNCNAME_ARGS_TYPES   = 0x00100000,
    FIF_FUNCNAME_ARGS_NAMES   = 0x00200000,
    FIF_FUNCNAME_ARGS_VALUES  = 0x00400000,
    FIF_FUNCNAME_ARGS_ALL     = 0x00700000,
    FIF_ARGS_TYPES            = 0x01000000,
    FIF_ARGS_NAMES            = 0x02000000,
    FIF_ARGS_VALUES           = 0x04000000,
    FIF_ARGS_ALL              = 0x07000000,
    FIF_ARGS_NOFORMAT         = 0x08000000,
    FIF_ARGS_NO_FUNC_EVAL     = 0x10000000,
    FIF_FILTER_NON_USER_CODE  = 0x20000000,
    FIF_ARGS_NO_TOSTRING      = 0x40000000,
    FIF_DESIGN_TIME_EXPR_EVAL = 0x80000000
};
typedef DWORD FRAMEINFO_FLAGS;
```

```csharp
public enum enum_FRAMEINFO_FLAGS {
    FIF_FUNCNAME              = 0x00000001,
    FIF_RETURNTYPE            = 0x00000002,
    FIF_ARGS                  = 0x00000004,
    FIF_LANGUAGE              = 0x00000008,
    FIF_MODULE                = 0x00000010,
    FIF_STACKRANGE            = 0x00000020,
    FIF_FRAME                 = 0x00000040,
    FIF_DEBUGINFO             = 0x00000080,
    FIF_STALECODE             = 0x00000100,
    FIF_ANNOTATEDFRAME        = 0x00000200,
    FIF_DEBUG_MODULEP         = 0x00000400,
    FIF_FUNCNAME_FORMAT       = 0x00001000,
    FIF_FUNCNAME_RETURNTYPE   = 0x00002000,
    FIF_FUNCNAME_ARGS         = 0x00004000,
    FIF_FUNCNAME_LANGUAGE     = 0x00008000,
    FIF_FUNCNAME_MODULE       = 0x00010000,
    FIF_FUNCNAME_LINES        = 0x00020000,
    FIF_FUNCNAME_OFFSET       = 0x00040000,
    FIF_FUNCNAME_ARGS_TYPES   = 0x00100000,
    FIF_FUNCNAME_ARGS_NAMES   = 0x00200000,
    FIF_FUNCNAME_ARGS_VALUES  = 0x00400000,
    FIF_FUNCNAME_ARGS_ALL     = 0x00700000,
    FIF_ARGS_TYPES            = 0x01000000,
    FIF_ARGS_NAMES            = 0x02000000,
    FIF_ARGS_VALUES           = 0x04000000,
    FIF_ARGS_ALL              = 0x07000000,
    FIF_ARGS_NOFORMAT         = 0x08000000,
    FIF_ARGS_NO_FUNC_EVAL     = 0x10000000,
    FIF_FILTER_NON_USER_CODE  = 0x20000000,
    FIF_ARGS_NO_TOSTRING      = 0x40000000,
    FIF_DESIGN_TIME_EXPR_EVAL = 0x80000000
};
```

## <a name="fields"></a>フィールド
`FIF_FUNCNAME`\
フィールドを初期化/`m_bstrFuncName`使用します。

`FIF_RETURNTYPE`\
フィールドを初期化/`m_bstrReturnType`使用します。

`FIF_ARGS`\
フィールドを初期化/`m_bstrArgs`使用します。

`FIF_LANGUAGE`\
フィールドを初期化/`m_bstrLanguage`使用します。

`FIF_MODULE`\
フィールドを初期化/`m_bstrModule`使用します。

`FIF_STACKRANGE`\
および (スタック`m_addrMin`範囲`m_addrMax`) フィールドを初期化/使用します。

`FIF_FRAME`\
フィールドを初期化/`m_pFrame`使用します。

`FIF_DEBUGINFO`\
フィールドを初期化/`m_fHasDebugInfo`使用します。

`FIF_STALECODE`\
フィールドを初期化/`m_fStaleCode`使用します。

`FIF_ANNOTATEDFRAME`\
フィールドを初期化/`m_fAnnotatedFrame`使用します。

`FIF_DEBUG_MODULEP`\
フィールドを初期化/`m_pModule`使用します。

`FIF_FUNCNAME_FORMAT`\
関数名をフォーマットします。 結果はフィールドに返され`m_bstrFunName`、他のフィールドには入力されません。

`FIF_FUNCNAME_RETURNTYPE`\
戻り値の型を`m_bstrFuncName`フィールドに追加します。

`FIF_FUNCNAME_ARGS`\
フィールドに引数を`m_bstrFuncName`追加します。

`FIF_FUNCNAME_LANGUAGE`\
フィールドに言語を`m_bstrFuncName`追加します。

`FIF_FUNCNAME_MODULE`\
モジュール名をフィールドに追加`m_bstrFuncName`します。

`FIF_FUNCNAME_LINES`\
フィールドに行数を`m_bstrFuncName`追加します。

`FIF_FUNCNAME_OFFSET`\
行の`m_bstrFuncName`先頭からのオフセットをバイト単位でフィールドに追加します (`FIF_FUNCNAME_LINES`指定されている場合)。 指定`FIF_FUNCNAME_LINES`しない場合、または行番号が使用できない場合は、関数の先頭からのオフセットをバイト単位で加算します。

`FIF_FUNCNAME_ARGS_TYPES`\
各関数引数の型をフィールドに`m_bstrFuncName`追加します。

`FIF_FUNCNAME_ARGS_NAMES`\
各関数引数の名前をフィールドに追加`m_bstrFuncName`します。

`FIF_FUNCNAME_ARGS_VALUES`\
各関数引数の値をフィールドに`m_bstrFuncName`追加します。

`FIF_FUNCNAME_ARGS_ALL`\
すべての引数の型、名前、および値をフィールドに`m_bstrFuncName`追加します。

`FIF_ARGS_TYPES`\
引数の型が取得され、書式設定されます。

`FIF_ARGS_NAMES`\
引数名が取得され、フォーマットされます。

`FIF_ARGS_VALUES`\
引数値が取得され、書式設定されます。

`FIF_ARGS_ALL`\
すべての引数の型、名前、および値を取得して書式を設定します。

`FIF_ARGS_NOFORMAT`\
引数の書式を設定しないことを指定します (たとえば、引数リストの前後に左かっこと右かっこを追加したり、引数の間に区切り記号を追加したりしません)。

`FIF_ARGS_NO_FUNC_EVAL`\
引数の値を取得するときに関数 (プロパティ) の評価を使用しないことを指定します。

`FIF_FILTER_NON_USER_CODE`\
デバッグ エンジンは、非ユーザー コード フレームをフィルター処理して、含まれないようにします。

`FIF_ARGS_NO_TOSTRING`\
関数の引数`ToString()`を返すときに、関数の評価や書式設定を許可しないでください。

`FIF_DESIGN_TIME_EXPR_EVAL`\
フレーム情報は、ホスト プロセスではなく、ホストされるアプリ ドメインから取得する必要があります。

## <a name="remarks"></a>Remarks
これらのフラグは[、FrameInfo](../../../extensibility/debugger/reference/frameinfo.md)構造体または構造体で初期化されるフィールドを示すために[、列挙型](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)のメソッドと[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)メソッドに渡されます。

これらのフラグは[、FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体のどのフィールドが使用され、構造体が戻されたときに有効かを示すためにも使用されます。 これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
