---
title: EXCEPTION_STATE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_STATE
helpviewer_keywords:
- EXCEPTION_STATE enumeration
ms.assetid: 597f4f4c-9b70-485c-b5dc-3c2e3aecc664
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cd2e280cd03ae413e0853950d13fbfefb69bc15f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736954"
---
# <a name="exception_state"></a>EXCEPTION_STATE
例外状態を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
typedef DWORD EXCEPTION_STATE;
```

```csharp
public enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
```

## <a name="fields"></a>フィールド
`EXCEPTION_NONE`\
例外で停止しないでください。

`EXCEPTION_STOP_FIRST_CHANCE`\
例外の最初の起動を停止します。 例外イベントを記述する場合、このフラグは、例外イベントが初回例外イベントであることを示します。

`EXCEPTION_STOP_SECOND_CHANCE`\
例外の 2 回目の起動で停止します。 例外イベントを記述する場合、例外イベントが 2 番目の例外イベントであることを示します。

`EXCEPTION_STOP_USER_FIRST_CHANCE`\
ユーザー モード例外の最初の発生を停止します。 例外イベントを記述する場合、例外イベントが初回ユーザー例外イベントであることを示します。

`EXCEPTION_STOP_USER_UNCAUGHT`\
ユーザー モード例外がキャッチされない場合は停止します。 例外イベントを記述する場合、例外イベントがキャッチされていないユーザー モード例外イベントであることを示します。

`EXCEPTION_STOP_ALL`\
例外を除いて停止します。 例外イベントを記述するときには使用されません。

`EXCEPTION_CANNOT_BE_CONTINUED`\
例外イベントを記述する場合、例外を続行できないことを示します。

`EXCEPTION_CODE_SUPPORTED`\
例外に、それをサポートするコードがあることを示します。 例外の表示に使用

`EXCEPTION_CODE_DISPLAY_IN_HEX`\
例外コードを 16 進数で表示することを示します。 例外の表示に使用されます。

`EXCEPTION_JUST_MY_CODE_SUPPORTED`\
例外コードが JustMyCode をサポートすることを示します。 例外の表示に使用されます。

`EXCEPTION_MANAGED_DEBUG_ASSISTANT`\
マネージ コード デバッガーが例外を処理する必要があることを示します。 設定されていない場合、既定のデバッガーは例外を処理します。 これは[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)メソッドに渡され[、EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)構造体では使用されません。

`EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT`\
古い、使用しないでください。

`EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT`\
古い、使用しないでください。

`EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT`\
古い、使用しないでください。

`EXCEPTION_STOP_USER_SECOND_CHANCE_USE_PARENT`\
古い、使用しないでください。

## <a name="remarks"></a>Remarks
例外の`dwState`状態と、その例外に対して何ができるかを示すために[、EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)構造体のメンバーとして使用されます。

これらの値は、すべての例外の状態を設定する[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)メソッドにも渡されます。

これらのフラグはビットごとの OR と組み合わせられます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)
