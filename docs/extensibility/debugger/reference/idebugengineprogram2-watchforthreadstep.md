---
title: プログラム2:::ウォッチフォースレッドステップ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cf0474d527b7c6f1d180201a463f52a0b17d18fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730358"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
指定されたスレッドで実行を監視 (または実行の監視を停止) します。

## <a name="syntax"></a>構文

```cpp
HRESULT WatchForThreadStep( 
   IDebugProgram2* pOriginatingProgram,
   DWORD           dwTid,
   BOOL            fWatch,
   DWORD           dwFrame
);
```

```csharp
int WatchForThreadStep( 
   IDebugProgram2 pOriginatingProgram,
   uint           dwTid,
   int            fWatch,
   uint           dwFrame
);
```

## <a name="parameters"></a>パラメーター
`pOriginatingProgram`\
[in]ステップ実行されるプログラムを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクト。

`dwTid`\
[in]監視するスレッドの識別子を指定します。

`fWatch`\
[in]非ゼロ (`TRUE`) は、 で`dwTid`識別されるスレッドでの実行を監視開始する、それ以外の場合`FALSE`は、 0 ( `dwTid`) は、 での実行を監視しなくなることを意味します。

`dwFrame`\
[in]ステップの種類を制御するフレーム インデックスを指定します。 この値がゼロ (0) の場合、ステップ・タイプは「ステップ・イン」になり、指定された`dwTid`スレッドが実行されるたびにプログラムを停止する必要があります。 ゼロ`dwFrame`以外の場合、ステップの種類は "ステップ オーバー" になり、指定された`dwTid`スレッドがスタック上でのインデックス以上のフレームで実行されている場合にのみ、プログラムを停止する必要`dwFrame`があります。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 セッション デバッグ マネージャー (SDM) は、パラメーターで識別`pOriginatingProgram`されるプログラムをステップするときに、このメソッドを呼び出すことによって、他のすべての接続されたプログラムを通知します。

 このメソッドは、同じスレッドのステップ実行にのみ適用されます。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
