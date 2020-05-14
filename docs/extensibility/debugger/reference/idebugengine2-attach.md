---
title: IDebugEngine2::アタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 93890885dbbdfd3cc26984590955681487977200
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731207"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
デバッグ エンジン (DE) をプログラムにアタッチします。 DE が SDM に対してインプロセスで実行されている場合に、セッション デバッグ マネージャー (SDM) によって呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugProgram2**      pProgram,
   IDebugProgramNode2**  rgpProgramNodes,
   DWORD                 celtPrograms,
   IDebugEventCallback2* pCallback,
   ATTACH_REASON         dwReason
);
```

```csharp
int Attach( 
   IDebugProgram2[]     pProgram,
   IDebugProgramNode2[] rgpProgramNodes,
   uint                 celtPrograms,
   IDebugEventCallback2 pCallback,
   Enum_ATTACH_REASON   dwReason
);
```

## <a name="parameters"></a>パラメーター
`pProgram`\
[in]アタッチするプログラムを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクトの配列。 これらはポート プログラムです。

`rgpProgramNodes`\
[in]プログラム ノードを表す[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)オブジェクトの配列です。 この配列のプログラム ノードは、 と同じ`pProgram`プログラムを表します。 プログラム・ノードは、DE が接続先のプログラムを識別できるように与えられます。

`celtPrograms`\
[in]配列内のプログラムおよびプログラム ノード`pProgram``rgpProgramNodes`の数。

`pCallback`\
[in]SDM にデバッグ イベントを送信するために使用[されるオブジェクト。](../../../extensibility/debugger/reference/idebugeventcallback2.md)

`dwReason`\
[in]これらのプログラムをアタッチする理由を指定する[ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)列挙体の値。 詳細については、「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 プログラムにアタッチする理由は、次の 3 つがあります。

- `ATTACH_REASON_LAUNCH`は、ユーザーがプログラムを含むプロセスを起動したために、DE がプログラムにアタッチされていることを示します。

- `ATTACH_REASON_USER`ユーザーが、プログラム (またはプログラムを含むプロセス) にアタッチする DE を明示的に要求したことを示します。

- `ATTACH_REASON_AUTO`DE は、特定のプロセスで他のプログラムをデバッグしているため、特定のプログラムにアタッチされていることを示します。 これは自動アタッチとも呼ばれます。

  このメソッドが呼び出されると、DE は次のイベントを順番に送信する必要があります。

1. [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) (デバッグ エンジンの特定のインスタンスに対してまだ送信されていない場合)

2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

   さらに、アタッチの理由が`ATTACH_REASON_LAUNCH`の場合、DE は[IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)イベントを送信する必要があります。

   デは、デバッグ中のプログラムに対応する[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)オブジェクトを取得すると、プライベート インターフェイスのクエリを実行できます。

   または`pProgram``rgpProgramNodes`によって与えられた配列内のプログラム ノードのメソッドを呼び出す前に、必要に応じて`IDebugProgram2`偽装をプログラム ノードを表すインターフェイスで有効にする必要があります。 ただし、通常、この手順は必要ありません。 詳細については、「[セキュリティの問題](../../../extensibility/debugger/security-issues.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
