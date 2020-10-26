---
title: フレーム情報 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736783"
---
# <a name="frameinfo"></a>FRAMEINFO
スタックフレームについて説明します。

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
入力するフィールドを指定する、 [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md) 列挙のフラグの組み合わせ。

`m_bstrFuncName`\
スタックフレームに関連付けられている関数名。

`m_bstrReturnType`\
スタックフレームに関連付けられた戻り値の型。

`m_bstrArgs`\
スタックフレームに関連付けられている関数の引数。

`m_bstrLanguage`\
関数が実装されている言語。

`m_bstrModule`\
スタックフレームに関連付けられているモジュール名。

`m_addrMin`\
最小物理スタックアドレス。

`m_addrMAX`\
最大物理スタックアドレス。

`m_pFrame`\
このスタックフレームを表す [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) オブジェクト。

`m_pModule`\
このスタックフレームを含むモジュールを表す [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) オブジェクト。

`m_fHasDebugInfo`\
指定された `TRUE` フレームにデバッグ情報が存在する場合は0以外 ()。

`m_fStaleCode`\
`TRUE`スタックフレームが無効になっているコードに関連付けられている場合は0以外 ()。

`m_fAnnotatedFrame`\
`TRUE`セッションデバッグマネージャー (SDM) によってスタックフレームに注釈が付けられている場合は0以外 ()。

## <a name="remarks"></a>解説
この構造体は、入力する [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md) メソッドに渡されます。 この構造体は、 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) インターフェイスに含まれるリストにも含まれています。この一覧は、 [enumフレーム情報](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) メソッドの呼び出しから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
