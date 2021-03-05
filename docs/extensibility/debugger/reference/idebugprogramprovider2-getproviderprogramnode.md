---
description: 特定のプログラムのプログラムノードを取得します。
title: 'IDebugProgramProvider2:: GetProviderProgramNode |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
ms.assetid: e62e8e83-acbb-4c52-aedf-ffbd4670db29
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9d672c5b8277e418efdde047c7a49bf5e05ec0be
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167075"
---
# <a name="idebugprogramprovider2getproviderprogramnode"></a>IDebugProgramProvider2::GetProviderProgramNode
特定のプログラムのプログラムノードを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProviderProgramNode(
   PROVIDER_FLAGS       Flags,
   IDebugDefaultPort2*  pPort,
   AD_PROCESS_ID        processId,
   REFGUID              guidEngine,
   UINT64               programId,
   IDebugProgramNode2** ppProgramNode
);
```

```csharp
int GetProviderProgramNode(
   enum_PROVIDER_FLAGS    Flags,
   IDebugDefaultPort2     pPort,
   AD_PROCESS_ID          ProcessId,
   ref Guid               guidEngine,
   ulong                  programId,
   out IDebugProgramNode2 ppProgramNode
);
```

## <a name="parameters"></a>パラメーター
`Flags`\
から [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) 列挙型のフラグの組み合わせ。 この呼び出しでは、次のフラグが一般的に使用されます。

|フラグ|説明|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|リモートコンピューターで呼び出し元が実行されています。|
|`PFLAG_DEBUGGEE`|呼び出し元は現在デバッグ中です (各ノードに対してマーシャリングに関する追加情報が返されます)。|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|呼び出し元はにアタッチされましたが、デバッガーによって起動されませんでした。|

`pPort`\
から呼び出しプロセスが実行されているポート。

`processId`\
から対象のプログラムを含むプロセスの ID を保持する [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体。

`guidEngine`\
からプログラムがアタッチされているデバッグエンジンの GUID (存在する場合)。

`programId`\
からプログラムノードを取得するプログラムの ID。

`ppProgramNode`\
入出力要求されたプログラムノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
