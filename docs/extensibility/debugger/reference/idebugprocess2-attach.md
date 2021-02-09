---
title: 'IDebugProcess2:: Attach |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 462b2299a658359e81fc3641e590b95ab183a24e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99874179"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
セッションデバッグマネージャー (SDM) をプロセスにアタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   GUID*                 rgguidSpecificEngines,
   DWORD                 celtSpecificEngines,
   HRESULT*              rghrEngineAttach
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   Guid[]               rgguidSpecificEngines,
   uint                 celtSpecificEngines,
   int[]                rghrEngineAttach
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
からデバッグイベント通知に使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`rgguidSpecificEngines`\
からプロセスで実行されているプログラムをデバッグするために使用されるデバッグエンジンの Guid の配列。 このパラメーターには null 値を指定できます。 詳細については、「解説」を参照してください。

`celtSpecificEngines`\
から配列内のデバッグエンジンの数 `rgguidSpecificEngines` と配列のサイズ `rghrEngineAttach` 。

`rghrEngineAttach`\
[入力、出力]デバッグエンジンによって返される HRESULT コードの配列。 この配列のサイズは、パラメーターで指定し `celtSpecificEngines` ます。 各コードは通常、 `S_OK` または `S_ATTACH_DEFERRED` です。 後者は、DE が現在プログラムにアタッチされていないことを示します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、その他の使用可能な値を示します。

|値|説明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定されたプロセスは既にデバッガーにアタッチされています。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|Attach プロシージャの実行中にセキュリティ違反が発生しました。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|デスクトッププロセスをデバッガーにアタッチすることはできません。|

## <a name="remarks"></a>解説
 プロセスにアタッチすると、そのプロセスで実行されているすべてのプログラムに SDM がアタッチされます。このプロセスは、配列で指定されたデバッグエンジン (DE) によってデバッグでき `rgguidSpecificEngines` ます。 パラメーターを `rgguidSpecificEngines` null 値に設定するか、または `GUID_NULL` プロセス内のすべてのプログラムにアタッチする配列に含めます。

 プロセスで発生するすべてのデバッグイベントは、指定された [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクトに送信されます。 この `IDebugEventCallback2` オブジェクトは、SDM がこのメソッドを呼び出したときに提供されます。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
