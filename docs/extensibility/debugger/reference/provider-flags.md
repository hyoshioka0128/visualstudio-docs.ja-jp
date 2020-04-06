---
title: PROVIDER_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_FLAGS
helpviewer_keywords:
- PROVIDER_FLAGS enumeration
ms.assetid: 8cbd2312-ed2f-4477-b192-c3f25c6098c3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d2333b62f21aa7b2b2bc70bddb50cbb3983cedf5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713816"
---
# <a name="provider_flags"></a>PROVIDER_FLAGS
プログラム プロバイダーから取得する必要なプロパティを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PROVIDER_FLAGS {
   PFLAG_NONE                    = 0x00,
   PFLAG_REMOTE_PORT             = 0x01,
   PFLAG_DEBUGGEE                = 0x02,
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,
   PFLAG_REASON_WATCH            = 0x08,
   PFLAG_GET_PROGRAM_NODES       = 0x10,
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20
};
typedef DWORD PROVIDER_FLAGS;
```

```csharp
public enum enum_PROVIDER_FLAGS {
   PFLAG_NONE                    = 0x00,
   PFLAG_REMOTE_PORT             = 0x01,
   PFLAG_DEBUGGEE                = 0x02,
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,
   PFLAG_REASON_WATCH            = 0x08,
   PFLAG_GET_PROGRAM_NODES       = 0x10,
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20
};
```

## <a name="fields"></a>フィールド
 `PFLAG_NONE`\
 フラグが指定されていません。

 `PFLAG_REMOTE_PORT`\
 呼び出し元は、 とは異[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]なるマシン上のプログラムの一覧を必要とします。

 `PFLAG_DEBUGGEE`\
 プロセスは現在、このインスタンスによってデバッグされています[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]。

 `PFLAG_ATTACH_TODEBUGGEE`\
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]はデバッグ中のプログラムにアタッチされていますが、起動しませんでした。

 `PFLAG_REASON_WATCH`\
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]イベントを見ています。

 `PFLAG_GET_PROGRAM_NODES`\
 呼び出`ProgramNodes`し元は[、PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)構造体のフィールドを必要とします。

 `PFLAG_GET_IS_DEBUGGER_PRESENT`\
 呼び出`fIsTheDebuggerPresent`し元は`PROVIDER_PROCESS_DATA`構造体のフィールドを必要とします。

## <a name="remarks"></a>Remarks
 これらのフラグは、次のメソッドに渡されます。

- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)

- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)

- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)

  これらの値はビット単位`OR`で組み合わせることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
