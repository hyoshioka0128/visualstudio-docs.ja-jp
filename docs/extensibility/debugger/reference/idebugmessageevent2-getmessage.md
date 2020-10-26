---
title: 'IDebugMessageEvent2:: GetMessage |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727403"
---
# <a name="idebugmessageevent2getmessage"></a>IDebugMessageEvent2::GetMessage
表示されるメッセージを取得します。

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
入出力メッセージの種類を示す [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md) 列挙から値を返します。

`pbstrMessage`\
入出力メッセージを返します。

`pdwType`\
入出力Win32 関数の規約を使用して、メッセージの型を返し `MessageBox` ます。 詳細については、 [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox) 関数を参照してください。

`pbstrHelpFileName`\
[入力、出力]ヘルプファイル名を返します。 ヘルプファイルがない場合は、null (C++) または空 (C#) の値を指定できます。

`pdwHelpId`\
[入力、出力]ヘルプ識別子を返します。 このメッセージにヘルプが関連付けられていない場合は0になることがあります。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
- [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)
