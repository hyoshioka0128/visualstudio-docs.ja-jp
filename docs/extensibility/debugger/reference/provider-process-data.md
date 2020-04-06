---
title: PROVIDER_PROCESS_DATA |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_PROCESS_DATA
helpviewer_keywords:
- PROVIDER_PROCESS_DATA structure
ms.assetid: ec2362ed-4a0c-4a09-9d66-8ff04e4f41ee
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bdaf15d09af3199d026155cf7667f063f5bbe858
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713777"
---
# <a name="provider_process_data"></a>PROVIDER_PROCESS_DATA
この構造体は、マシン上で実行されているプロセスに関する情報を提供します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagPROVIDER_PROCESS_DATA {
   PROVIDER_FIELDS    Fields;
   PROGRAM_NODE_ARRAY ProgramNodes;
   BOOL               fIsDebuggerPresent;
} PROVIDER_PROCESS_DATA;
```

```csharp
public struct PROVIDER_PROCESS_DATA {
   public uint               Fields;
   public PROGRAM_NODE_ARRAY ProgramNodes;
   public int                fIsDebuggerPresent;
}
```

## <a name="members"></a>メンバー
 `Fields`\
 [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)列挙体のフラグの組み合わせで、どのフィールドが入力されているかを示します。

 `ProgramNodes`\
 プログラム ノードの配列を含む[PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)構造体。

 `fIsDebuggerPresent`\
 デバッガーが`TRUE`[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]実行されている場合は 0 以外 (`FALSE`) 以外の場合はゼロ ( ) 。

## <a name="remarks"></a>Remarks
 この構造体は、埋め込まれる[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)メソッドに渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)
- [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
