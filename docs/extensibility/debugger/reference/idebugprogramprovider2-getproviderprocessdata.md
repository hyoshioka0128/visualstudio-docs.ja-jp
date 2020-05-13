---
title: プログラムプロバイダ2:::ゲットプロバイダプロセスデータ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProcessData
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProcessData
ms.assetid: 90cf7b7f-53d2-487e-b793-94501a6e24dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4e958900307f5f7915f58679709c88f80c2abfc9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721857"
---
# <a name="idebugprogramprovider2getproviderprocessdata"></a>IDebugProgramProvider2::GetProviderProcessData
指定したプロセスから実行中のプログラムの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProviderProcessData(
   PROVIDER_FLAGS         Flags,
   IDebugDefaultPort2*    pPort,
   AD_PROCESS_ID          processId,
   CONST_GUID_ARRAY       EngineFilter,
   PROVIDER_PROCESS_DATA* pProcess
);
```

```csharp
int GetProviderProcessData(
   enum_PROVIDER_FLAGS     Flags,
   IDebugDefaultPort2      pPort,
   AD_PROCESS_ID           ProcessId,
   CONST_GUID_ARRAY        EngineFilter,
   PROVIDER_PROCESS_DATA[] pProcess
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
|`PFLAG_GET_PROGRAM_NODES`|呼び出し元は、返されるプログラム・ノードのリストを要求しています。|

`pPort`\
[in]呼び出し側プロセスが実行されているポート。

`processId`\
[in]問題のプログラムを含むプロセスの ID を保持する[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)構造体。

`EngineFilter`\
[in]このプロセスをデバッグするために割り当てられたデバッグ エンジン用の GUID の配列 (これらは、提供されたエンジンがサポートする内容に基づいて実際に返されるプログラムをフィルター処理するために使用されます。

`pProcess`\
[アウト]要求された情報を入力する[PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)構造体。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、通常、プロセスによって呼び出され、そのプロセスで実行されているプログラムの一覧を取得します。 返される情報は[、IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)オブジェクトのリストです。

## <a name="see-also"></a>関連項目
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
