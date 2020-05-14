---
title: EXCEPTION_INFO |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_INFO
helpviewer_keywords:
- EXCEPTION_INFO structure
ms.assetid: d046957a-b97d-420b-b46b-c67cbaef709e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a305d34123d02b1fdbd545a438db4461643ed185
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737022"
---
# <a name="exception_info"></a>EXCEPTION_INFO
デバッグ中のプログラムによってスローされる例外または実行時エラーについて説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagEXCEPTION_INFO {
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    BSTR            bstrExceptionName;
    DWORD           dwCode;
    EXCEPTION_STATE dwState;
    GUID            guidType;
} EXCEPTION_INFO;
```

```csharp
public struct EXCEPTION_INFO {
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public string         bstrExceptionName;
    public uint           dwCode;
    public uint           dwState;
    public Guid           guidType;
};
```

## <a name="members"></a>メンバー
`pProgram`\
例外が発生したプログラムを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクト。

`bstrProgramName`\
例外が発生したプログラムの名前。

`bstrExceptionName`\
例外の名前。

`dwCode`\
例外または実行時エラーの識別コード。

`dwState`\
例外の状態を定義する[EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)列挙体の値。

`guidType`\
GUID 言語識別子 、 `guidLang` `guidEng`または .

## <a name="remarks"></a>Remarks
この構造体は、パラメーターとして渡されます、 [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)と[メソッドを削除します](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)。 この構造体は[、GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)メソッドにも渡され、埋められます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)
- [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)
