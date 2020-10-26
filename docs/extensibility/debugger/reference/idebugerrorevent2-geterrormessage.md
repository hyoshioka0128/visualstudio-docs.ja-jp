---
title: 'IDebugErrorEvent2:: GetErrorMessage |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730045"
---
# <a name="idebugerrorevent2geterrormessage"></a>IDebugErrorEvent2::GetErrorMessage
人間が判読できるエラーメッセージの構築を可能にする情報を返します。

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
入出力メッセージの種類を記述して、 [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md) 列挙から値を返します。

`pbstrErrorFormat`\
入出力ユーザーへの最終メッセージの形式 (詳細については、「解説」を参照してください)。

`hrErrorReason`\
入出力メッセージのエラーコード。

`pdwType`\
入出力エラーの重大度 (の MB_XXX 定数を使用し `MessageBox` ます。たとえば、 `MB_EXCLAMATION` または `MB_WARNING` )。

`pbstrHelpFileName`\
入出力ヘルプファイルへのパス (ヘルプファイルがない場合は null 値に設定されます)。

`pdwHelpId`\
入出力表示するヘルプトピックの ID (ヘルプトピックがない場合は0に設定します)。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 エラーメッセージは、の行に沿って書式設定する必要があり `"What I was doing.  %1"` ます。 次に、は、 `"%1"` エラーコードから派生したエラーメッセージ (で返されます) を使用して、呼び出し元によって置き換えられ `hrErrorReason` ます。 パラメーターは、 `pMessageType` 最後のエラーメッセージをどのように表示するかを呼び出し元に指示します。

## <a name="see-also"></a>関連項目
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
