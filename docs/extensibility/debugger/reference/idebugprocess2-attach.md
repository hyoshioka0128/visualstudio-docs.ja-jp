---
title: IDebugプロセス2::アタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fb6ea896285c784021402400597ba168f6ccf716
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724192"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
セッション デバッグ マネージャー (SDM) をプロセスにアタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   GUID*                 rgguidSpecificEngines,
   DWORD                 celtSpecificEngines,
   HRESULT*              rghrEngineAttach
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   Guid[]               rgguidSpecificEngines,
   uint                 celtSpecificEngines,
   int[]                rghrEngineAttach
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
[in]デバッグ イベント通知に使用される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)オブジェクト。

`rgguidSpecificEngines`\
[in]プロセスで実行されているプログラムのデバッグに使用するデバッグ エンジンの GUID の配列。 このパラメーターには、NULL 値を指定できます。 詳細については、「解説」を参照してください。

`celtSpecificEngines`\
[in]配列内のデバッグ エンジンの`rgguidSpecificEngines`数と`rghrEngineAttach`配列のサイズ。

`rghrEngineAttach`\
[イン、アウト]デバッグ エンジンによって返される HRESULT コードの配列。 この配列のサイズは`celtSpecificEngines`、パラメーターで指定されます。 各コードは通常、 `S_OK` `S_ATTACH_DEFERRED`または のいずれかです。 後者は、DE が現在プログラムに接続されていることを示します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 次の表に、その他の値を示します。

|[値]|説明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定されたプロセスは既にデバッガーにアタッチされています。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|アタッチ処理中にセキュリティ違反が発生しました。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|デスクトップ プロセスをデバッガにアタッチすることはできません。|

## <a name="remarks"></a>Remarks
 プロセスにアタッチすると、配列で指定されたデバッグ エンジン (DE) によってデバッグできる、そのプロセスで実行されているすべてのプログラムに SDM が`rgguidSpecificEngines`アタッチされます。 このパラメータ`rgguidSpecificEngines`を null 値に設定`GUID_NULL`するか、またはプロセス内のすべてのプログラムにアタッチする配列に含めます。

 プロセスで発生するすべてのデバッグ イベントは、指定された[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)オブジェクトに送信されます。 この`IDebugEventCallback2`オブジェクトは、SDM がこのメソッドを呼び出したときに提供されます。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
