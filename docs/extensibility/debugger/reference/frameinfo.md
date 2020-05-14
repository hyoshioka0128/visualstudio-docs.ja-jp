---
title: フレーム情報 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO
helpviewer_keywords:
- FRAMEINFO structure
ms.assetid: 95001b89-dddb-45bb-889d-8327994e38a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c40361a9739bf468de2038df4325fa1ac98337c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736783"
---
# <a name="frameinfo"></a>FRAMEINFO
スタック フレームを表します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagFRAMEINFO {
    FRAMEINFO_FLAGS    m_dwValidFields;
    BSTR               m_bstrFuncName;
    BSTR               m_bstrReturnType;
    BSTR               m_bstrArgs;
    BSTR               m_bstrLanguage;
    BSTR               m_bstrModule;
    UINT64             m_addrMin;
    UINT64             m_addrMax;
    IDebugStackFrame2* m_pFrame;
    IDebugModule2*     m_pModule;
    BOOL               m_fHasDebugInfo;
    BOOL               m_fStaleCode;
    BOOL               m_fAnnotatedFrame;
} FRAMEINFO;
```

```csharp
public struct FRAMEINFO {
    public uint              m_dwValidFields;
    public string            m_bstrFuncName;
    public string            m_bstrReturnType;
    public string            m_bstrArgs;
    public string            m_bstrLanguage;
    public string            m_bstrModule;
    public ulong             m_addrMin;
    public ulong             m_addrMax;
    public IDebugStackFrame2 m_pFrame;
    public IDebugModule2     m_pModule;
    public int               m_fHasDebugInfo;
    public int               m_fStaleCode;
    public int               m_fAnnotatedFrame;
} FRAMEINFO;
```

## <a name="members"></a>メンバー
`m_dwValidFields`\
FRAMEINFO_FLAGS[列挙体](../../../extensibility/debugger/reference/frameinfo-flags.md)のフラグの組み合わせで、どのフィールドが入力されているかを指定します。

`m_bstrFuncName`\
スタック フレームに関連付けられている関数名。

`m_bstrReturnType`\
スタック フレームに関連付けられている戻り値の型。

`m_bstrArgs`\
スタック フレームに関連付けられている関数の引数。

`m_bstrLanguage`\
関数が実装される言語。

`m_bstrModule`\
スタック フレームに関連付けられているモジュール名。

`m_addrMin`\
最小の物理スタック アドレス。

`m_addrMAX`\
物理スタックアドレスの最大値。

`m_pFrame`\
このスタック フレームを表す[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)オブジェクト。

`m_pModule`\
このスタック フレームを含むモジュールを表す[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)オブジェクト。

`m_fHasDebugInfo`\
指定されたフレームに`TRUE`デバッグ情報が存在する場合は、ゼロ以外 ( ) 。

`m_fStaleCode`\
スタック フレームが`TRUE`有効でなくなったコードに関連付けられている場合は、ゼロ以外 ( ) 。

`m_fAnnotatedFrame`\
スタック フレームに`TRUE`セッション デバッグ マネージャー (SDM) によってアノフィトが付けられた場合は、ゼロ以外 ( ) 。

## <a name="remarks"></a>Remarks
この構造体は[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)メソッドに渡され、入力されます。 この構造体は、メソッドの呼び出しから返される[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)インターフェイスに含まれているリストにも[含まれています。](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
