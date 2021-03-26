---
description: スタックフレームオブジェクトについて取得する情報を指定します。
title: FRAMEINFO_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO_FLAGS
helpviewer_keywords:
- FRAMEINFO_FLAGS enumeration
ms.assetid: 41578062-8455-412a-9d8b-1e1e9dc8d52e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d4214dd81945c3e7e2711a500e2e3a2b173e33e0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059263"
---
# <a name="frameinfo_flags"></a>FRAMEINFO_FLAGS
スタックフレームオブジェクトについて取得する情報を指定します。

## <a name="syntax"></a>Syntax

```cpp
enum enum_FRAMEINFO_FLAGS {
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
public enum enum_FRAMEINFO_FLAGS {
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
フィールドを初期化/使用 `m_bstrFuncName` します。

`FIF_RETURNTYPE`\
フィールドを初期化/使用 `m_bstrReturnType` します。

`FIF_ARGS`\
フィールドを初期化/使用 `m_bstrArgs` します。

`FIF_LANGUAGE`\
フィールドを初期化/使用 `m_bstrLanguage` します。

`FIF_MODULE`\
フィールドを初期化/使用 `m_bstrModule` します。

`FIF_STACKRANGE`\
`m_addrMin`および `m_addrMax` (スタック範囲) フィールドを初期化/使用します。

`FIF_FRAME`\
フィールドを初期化/使用 `m_pFrame` します。

`FIF_DEBUGINFO`\
フィールドを初期化/使用 `m_fHasDebugInfo` します。

`FIF_STALECODE`\
フィールドを初期化/使用 `m_fStaleCode` します。

`FIF_ANNOTATEDFRAME`\
フィールドを初期化/使用 `m_fAnnotatedFrame` します。

`FIF_DEBUG_MODULEP`\
フィールドを初期化/使用 `m_pModule` します。

`FIF_FUNCNAME_FORMAT`\
関数名を書式設定します。 結果はフィールドに返され、 `m_bstrFunName` 他のフィールドは入力されません。

`FIF_FUNCNAME_RETURNTYPE`\
フィールドに戻り値の型を追加し `m_bstrFuncName` ます。

`FIF_FUNCNAME_ARGS`\
フィールドに引数を追加し `m_bstrFuncName` ます。

`FIF_FUNCNAME_LANGUAGE`\
フィールドに言語を追加し `m_bstrFuncName` ます。

`FIF_FUNCNAME_MODULE`\
モジュール名をフィールドに追加し `m_bstrFuncName` ます。

`FIF_FUNCNAME_LINES`\
フィールドに行の数を追加し `m_bstrFuncName` ます。

`FIF_FUNCNAME_OFFSET`\
`m_bstrFuncName`が指定されている場合、行の先頭からのオフセット (バイト単位) をフィールドに追加し `FIF_FUNCNAME_LINES` ます。 が指定されていない場合 `FIF_FUNCNAME_LINES` 、または行番号が使用できない場合は、関数の先頭からのオフセットをバイト単位で加算します。

`FIF_FUNCNAME_ARGS_TYPES`\
フィールドに各関数の引数の型を追加し `m_bstrFuncName` ます。

`FIF_FUNCNAME_ARGS_NAMES`\
各関数の引数の名前をフィールドに追加し `m_bstrFuncName` ます。

`FIF_FUNCNAME_ARGS_VALUES`\
各関数の引数の値をフィールドに追加し `m_bstrFuncName` ます。

`FIF_FUNCNAME_ARGS_ALL`\
フィールドにすべての引数の型、名前、および値を追加し `m_bstrFuncName` ます。

`FIF_ARGS_TYPES`\
引数の型が取得および書式設定されます。

`FIF_ARGS_NAMES`\
引数名が取得および書式設定されます。

`FIF_ARGS_VALUES`\
引数の値は取得および書式設定されます。

`FIF_ARGS_ALL`\
すべての引数の型、名前、および値を取得して書式設定します。

`FIF_ARGS_NOFORMAT`\
引数が書式設定されていないことを指定します (たとえば、引数リストの始めかっこと終わりかっこを追加したり、引数の間に区切り記号を追加したりしないでください)。

`FIF_ARGS_NO_FUNC_EVAL`\
引数の値を取得するときに、関数 (プロパティ) の評価を使用しないことを指定します。

`FIF_FILTER_NON_USER_CODE`\
デバッグエンジンは、非ユーザーコードフレームをフィルター処理して、含まれないようにします。

`FIF_ARGS_NO_TOSTRING`\
関数 `ToString()` の引数を返すときに関数の評価または書式設定を許可しないでください。

`FIF_DESIGN_TIME_EXPR_EVAL`\
フレーム情報は、ホストプロセスではなく、ホストされているアプリケーションドメインからのものである必要があります。

## <a name="remarks"></a>注釈
これらのフラグは、[フレーム情報](../../../extensibility/debugger/reference/frameinfo.md)の構造体または構造体で初期化されるフィールドを示すために、 [enumフレーム情報](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)メソッドと[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)メソッドに渡されます。

これらのフラグは、 [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 構造のどのフィールドが使用され、構造体が返されたときに有効であるかを示すためにも使用されます。 これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
