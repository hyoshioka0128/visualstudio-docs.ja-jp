---
title: IDebugIDECallback::D isplayMessage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugIDECallback::DisplayMessage
ms.assetid: c19b48ee-b370-4fce-91fe-f82bf1e63179
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7073cc3d142d0faabe145b775780c177fbf0d732
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727861"
---
# <a name="idebugidecallbackdisplaymessage"></a>IDebugIDECallback::DisplayMessage
指定したメッセージ文字列をデバッガーの出力ウィンドウに送信します。

## <a name="syntax"></a>構文

```cpp
HRESULT DisplayMessage (
   LPCOLESTR szMessage
);
```

```csharp
int DisplayMessage (
   string szMessage
);
```

## <a name="parameters"></a>パラメーター
`szMessage`\
からデバッガーの出力ウィンドウに表示するメッセージ文字列。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)
