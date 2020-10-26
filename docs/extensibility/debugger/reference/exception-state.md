---
title: EXCEPTION_STATE |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736954"
---
# <a name="exception_state"></a>EXCEPTION_STATE
例外の状態を指定します。

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
例外では停止しないでください。

`EXCEPTION_STOP_FIRST_CHANCE`\
最初の例外の発生時に停止します。 例外イベントを記述する場合、このフラグは例外イベントが初回例外イベントであることを示します。

`EXCEPTION_STOP_SECOND_CHANCE`\
例外の2回目の発生時に停止します。 例外イベントを記述するときに、例外イベントが第2の例外イベントであることを示します。

`EXCEPTION_STOP_USER_FIRST_CHANCE`\
ユーザーモード例外の初回起動時に停止します。 例外イベントを記述するときに、例外イベントが初回ユーザー例外イベントであることを示します。

`EXCEPTION_STOP_USER_UNCAUGHT`\
ユーザーモードの例外がキャッチされない場合に停止します。 例外イベントを記述するときに、例外イベントがキャッチされていないユーザーモードの例外イベントであることを示します。

`EXCEPTION_STOP_ALL`\
例外で停止します。 例外イベントの記述時には使用されません。

`EXCEPTION_CANNOT_BE_CONTINUED`\
例外イベントを記述するときに、例外をから続行できないことを示します。

`EXCEPTION_CODE_SUPPORTED`\
例外にサポートするコードが含まれていることを示します。 例外の表示に使用されます

`EXCEPTION_CODE_DISPLAY_IN_HEX`\
例外コードを16進数で表示する必要があることを示します。 例外を表示するために使用されます。

`EXCEPTION_JUST_MY_CODE_SUPPORTED`\
例外コードがジャスト Mycode をサポートしていることを示します。 例外を表示するために使用されます。

`EXCEPTION_MANAGED_DEBUG_ASSISTANT`\
マネージコードデバッガーが例外を処理する必要があることを示します。 設定されていない場合、既定のデバッガーは例外を処理します。 これは [Setallexceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md) メソッドに渡され、 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体では使用されません。

`EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT`\
使用しないでください。

`EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT`\
使用しないでください。

`EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT`\
使用しないでください。

`EXCEPTION_STOP_USER_SECOND_CHANCE_USE_PARENT`\
使用しないでください。

## <a name="remarks"></a>解説
`dwState`例外の状態とそれに対して実行できることを示すために、 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)構造体のメンバーとして使用されます。

これらの値は、すべての例外の状態を設定するために [Setallexceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md) メソッドにも渡されます。

これらのフラグは、ビットごとの OR と組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)
