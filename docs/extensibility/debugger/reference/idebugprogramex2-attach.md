---
title: プログラムの追加 2::アタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 33b22b2f-431e-4205-9441-d28a9c928c97
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fcb52a96074b783043af1e908cf454466df74c30
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722379"
---
# <a name="idebugprogramex2attach"></a>IDebugProgramEx2::Attach
セッションをプログラムにアタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason,
   IDebugSession2*       pSession
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   uint                 dwReason,
   IDebugSession2       pSession
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
[in]アタッチされたデバッグ エンジンがイベントを送信するコールバック関数を表す[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)オブジェクト。

`dwReason`\
[in]アタッチ操作の理由を説明する[ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)列挙体の値。

`pSession`\
[in]プログラムにアタッチしているセッションを一意に識別する値。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 プログラムが既に`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`アタッチされている場合は、このメソッドは返す必要があります。

## <a name="remarks"></a>Remarks
 プログラムを含むポートは、 の`pSession`値を使用して、どのセッションがプログラムに接続しようとしているかを判別できます。 たとえば、ポートでプロセスに 1 つのデバッグ セッションのみをアタッチできる場合、ポートはプロセス内の他のプログラムに同じセッションが既に接続されているかどうかを判断できます。

> [!NOTE]
> 渡される`pSession`インターフェイスは、Cookie としてのみ扱われるため、このプログラムにアタッチするセッション デバッグ マネージャーを一意に識別する値です。指定されたインターフェイス上のメソッドはどれも機能しません。

## <a name="see-also"></a>関連項目
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
