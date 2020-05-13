---
title: エラーイベント2::エラーメッセージを取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2::GetErrorMessage
helpviewer_keywords:
- IDebugErrorEvent2::GetErrorMessage
ms.assetid: 9e3b0d74-a2dd-4eaa-bd95-21b2f9c79409
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1ff1da2f2a2d24b958a613e6fe5cb58c0081ed3e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730045"
---
# <a name="idebugerrorevent2geterrormessage"></a>IDebugErrorEvent2::GetErrorMessage
人間が判読できるエラー メッセージを構築できる情報を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetErrorMessage(
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrErrorFormat,
   HRESULT*     hrErrorReason,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetErrorMessage(
   out enum_MESSAGETYPE   pMessageType,
   out string             pbstrErrorFormat,
   out int                phrErrorReason,
   out uint               pdwType,
   out string             pbstrHelpFileName,
   out uint               pdwHelpId
);
```

## <a name="parameters"></a>パラメーター
`pMessageType`\
[アウト]メッセージの種類を示す[MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)列挙体から値を返します。

`pbstrErrorFormat`\
[アウト]ユーザーへの最終メッセージの形式 (詳細については「解説」を参照)。

`hrErrorReason`\
[アウト]メッセージに関するエラー コード。

`pdwType`\
[アウト]エラーの重大度 (たとえば、 に対`MessageBox`してMB_XXX定数を`MB_EXCLAMATION`使用`MB_WARNING`する、 または )。

`pbstrHelpFileName`\
[アウト]ヘルプ ファイルへのパス (ヘルプ ファイルがない場合は null 値に設定)。

`pdwHelpId`\
[アウト]表示するヘルプ トピックの ID (ヘルプ トピックがない場合は 0 に設定)。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 エラー メッセージは、 の`"What I was doing.  %1"`行に沿って書式設定する必要があります。 その`"%1"`後、呼び出し元に置き換えられ、エラー コードから派生したエラー`hrErrorReason`メッセージが返されます ( で返されます)。 この`pMessageType`パラメーターは、最終的なエラー メッセージの表示方法を呼び出し元に指示します。

## <a name="see-also"></a>関連項目
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [メッセージタイプ](../../../extensibility/debugger/reference/messagetype.md)
