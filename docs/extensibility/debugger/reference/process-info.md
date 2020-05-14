---
title: PROCESS_INFO |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO
helpviewer_keywords:
- PROCESS_INFO structure
ms.assetid: 260c33cc-a05e-4645-84b6-536d0b3b0537
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ef73145fb0a2598dc5e4ee98e8652314e0bc1c89
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713884"
---
# <a name="process_info"></a>PROCESS_INFO
プロセスに関する情報を格納します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagPROCESS_INFO { 
   PROCESS_INFO_FIELDS Fields;
   BSTR                bstrFileName;
   BSTR                bstrBaseName;
   BSTR                bstrTitle;
   AD_PROCESS_ID       ProcessId;
   DWORD               dwSessionId;
   BSTR                bstrAttachedSessionName;
   FILETIME            CreationTime;
   PROCESS_INFO_FLAGS  Flags;
} PROCESS_INFO;
```

```csharp
public struct PROCESS_INFO { 
   public uint          Fields;
   public string        bstrFileName;
   public string        bstrBaseName;
   public string        bstrTitle;
   public AD_PROCESS_ID ProcessId;
   public uint          dwSessionId;
   public string        bstrAttachedSessionName;
   public FILETIME      CreationTime;
   public uint          Flags;
};
```

## <a name="members"></a>メンバー
 `Fields`\
 入力するフィールドを指定する[PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)列挙体のフラグの組み合わせ。

 `bstrFileName`\
 プロセスの完全パス名。 パラメーター`GN_FILENAME`を使用して[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)メソッドを呼び出すのと同じです。

 `bstrBaseName`\
 プロセスのファイル名と拡張子。 パラメーター を使用`IDebugProcess2::Getname`してメソッドを呼`GN_BASENAME`び出すのと同じ.

 `bstrTitle`\
 プロセスのタイトル (存在する場合)。 パラメーター を使用`IDebugProcess2::Getname`してメソッドを呼`GN_TITLE`び出すのと同じ.

 `ProcessId`\
 プロセスを識別する[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)構造。 メソッドを呼び出すの[と](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)同じです。

 `dwSessionId`\
 このプロセスが実行されているデバッグ セッションの識別子。

 `bstrAttachedSessionName`\
 アタッチされたセッション名。 メソッドを呼び出す[のと](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)同じです。

 `CreationTime`\
 プロセスが作成された時刻。

 `Flags`\
 プロセスのプロパティを指定する[PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)列挙体のフラグの組み合わせ。

## <a name="remarks"></a>Remarks
 この構造体は[、GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)メソッドに渡され、そこで格納されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)
- [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
- [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)
- [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)
