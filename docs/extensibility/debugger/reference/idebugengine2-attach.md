---
description: プログラムまたはプログラムにデバッグエンジン (DE) をアタッチします。
title: 'IDebugEngine2:: Attach |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 38275cc623fcb8b30646c9d84ef194f584369ef2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093913"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
プログラムまたはプログラムにデバッグエンジン (DE) をアタッチします。 DE が SDM に対してインプロセスで実行されているときに、セッションデバッグマネージャー (SDM) によって呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugProgram2**      pProgram,
   IDebugProgramNode2**  rgpProgramNodes,
   DWORD                 celtPrograms,
   IDebugEventCallback2* pCallback,
   ATTACH_REASON         dwReason
);
```

```csharp
int Attach( 
   IDebugProgram2[]     pProgram,
   IDebugProgramNode2[] rgpProgramNodes,
   uint                 celtPrograms,
   IDebugEventCallback2 pCallback,
   Enum_ATTACH_REASON   dwReason
);
```

## <a name="parameters"></a>パラメーター
`pProgram`\
からアタッチされるプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトの配列。 これらはポートプログラムです。

`rgpProgramNodes`\
からプログラムノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトの配列 (プログラムごとに1つ)。 この配列のプログラムノードは、と同じプログラムを表し `pProgram` ます。 プログラムノードを指定すると、にアタッチするプログラムを、DE が識別できるようになります。

`celtPrograms`\
から配列および配列内のプログラムまたはプログラムノードの数 `pProgram` `rgpProgramNodes` 。

`pCallback`\
からデバッグイベントを SDM に送信するために使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`dwReason`\
からこれらのプログラムをアタッチする理由を指定する [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 列挙の値です。 詳細については、「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 プログラムにアタッチする理由には、次の3つがあります。

- `ATTACH_REASON_LAUNCH` ユーザーがプログラムを含むプロセスを起動したため、DE がプログラムにアタッチされていることを示します。

- `ATTACH_REASON_USER` ユーザーがプログラム (またはプログラムを含むプロセス) にアタッチするための DE を明示的に要求したことを示します。

- `ATTACH_REASON_AUTO` 特定のプロセス内の他のプログラムが既にデバッグされているため、DE が特定のプログラムにアタッチされていることを示します。 これは、自動アタッチとも呼ばれます。

  このメソッドが呼び出されると、DE は次の順序でこれらのイベントを送信する必要があります。

1. [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) (デバッグエンジンの特定のインスタンスに対してまだ送信されていない場合)

2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

   さらに、をアタッチする理由がの場合、 `ATTACH_REASON_LAUNCH` DE は [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) イベントを送信する必要があります。

   逆に、デバッグ中のプログラムに対応する [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトを取得すると、任意のプライベートインターフェイスに対してクエリを実行できます。

   またはによって指定された配列内のプログラムノードのメソッドを呼び出す前に、 `pProgram` `rgpProgramNodes` プログラムノードを表すインターフェイスで、必要に応じて偽装を有効にする必要があり `IDebugProgram2` ます。 ただし、通常、この手順は必要ありません。 詳細については、「 [セキュリティの問題](../../../extensibility/debugger/security-issues.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
