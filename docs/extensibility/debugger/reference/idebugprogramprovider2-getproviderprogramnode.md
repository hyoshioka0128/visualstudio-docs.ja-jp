---
title: プログラムプロバイダ2::プロバイダープログラムノード |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
ms.assetid: e62e8e83-acbb-4c52-aedf-ffbd4670db29
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd8ca7d5120ba20695caef2e9021ee25869df72f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721796"
---
# <a name="idebugprogramprovider2getproviderprogramnode"></a>IDebugProgramProvider2::GetProviderProgramNode
特定のプログラムのプログラム ノードを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProviderProgramNode(
   PROVIDER_FLAGS       Flags,
   IDebugDefaultPort2*  pPort,
   AD_PROCESS_ID        processId,
   REFGUID              guidEngine,
   UINT64               programId,
   IDebugProgramNode2** ppProgramNode
);
```

```csharp
int GetProviderProgramNode(
   enum_PROVIDER_FLAGS    Flags,
   IDebugDefaultPort2     pPort,
   AD_PROCESS_ID          ProcessId,
   ref Guid               guidEngine,
   ulong                  programId,
   out IDebugProgramNode2 ppProgramNode
);
```

## <a name="parameters"></a>パラメーター
`Flags`\
[in][PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)列挙体のフラグの組み合わせ。 この呼び出しでは、次のフラグが一般的です。

|フラグ|説明|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|呼び出し元はリモート コンピューターで実行されています。|
|`PFLAG_DEBUGGEE`|現在、呼び出し元はデバッグ中です (マーシャリングに関する追加情報は各ノードに返されます)。|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|呼び出し元は、デバッガーにアタッチされましたが、起動されませんでした。|

`pPort`\
[in]呼び出し側プロセスが実行されているポート。

`processId`\
[in]問題のプログラムを含むプロセスの ID を保持する[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)構造体。

`guidEngine`\
[in]プログラムがアタッチされているデバッグ エンジンの GUID (存在する場合)。

`programId`\
[in]プログラム ノードを取得する対象のプログラムの ID。

`ppProgramNode`\
[アウト]要求されたプログラム ノードを表す[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
