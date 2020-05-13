---
title: メッセージイベント2::メッセージを取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2::GetMessage
helpviewer_keywords:
- GetMessage method
- IDebugMessageEvent2::GetMessage method
ms.assetid: 9fca7285-f7f1-422d-8565-92bf0e0db60a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 819b796a656f0ef8775fbb1c9e800e3019b81729
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727403"
---
# <a name="idebugmessageevent2getmessage"></a>IDebugMessageEvent2::GetMessage
表示するメッセージを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMessage( 
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrMessage,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetMessage( 
   out enum_MESSAGETYPE pMessageType,
   out string           pbstrMessage,
   out uint             pdwType,
   out string           pbstrHelpFileName,
   out uint             dwHelpId
);
```

## <a name="parameters"></a>パラメーター
`pMessageType`\
[アウト]メッセージの種類を記述する[MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)列挙体から値を返します。

`pbstrMessage`\
[アウト]メッセージを返します。

`pdwType`\
[アウト]Win32`MessageBox`関数の規則を使用して、メッセージの種類を返します。 詳細については[、Afx メッセージ ボックス](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)関数を参照してください。

`pbstrHelpFileName`\
[イン、アウト]ヘルプ ファイル名を返します。 ヘルプ ファイルがない場合は、null (C++) または空の値 (C#) を指定できます。

`pdwHelpId`\
[イン、アウト]ヘルプ識別子を返します。 このメッセージに関連するヘルプがない場合は、0 になることがあります。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [メッセージタイプ](../../../extensibility/debugger/reference/messagetype.md)
- [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)
