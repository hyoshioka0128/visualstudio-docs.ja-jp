---
title: LPTEXTOUTPROC |Microsoft Docs
description: LPTEXTOUTPROC 関数ポインターについて説明します。 Visual Studio IDE では、エラーと状態を表示する関数が実装されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- LPTEXTOUTPROC
helpviewer_keywords:
- SccMsgDataOnMessage structure
- SccMsgDataOnBeforeGetFile structure
- SccMsgDataIsCancelled structure
- LPTEXTOUTPROC callback function
- SccMsgDataOnAfterGetFile structure
ms.assetid: 2025c969-e3c7-4cf4-a5c5-099d342895ea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e014d72fb3ae2b691f4a6eed28f14ff21656ef64
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073184"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC

ユーザーが統合開発環境 (IDE) 内からソース管理操作を実行する場合、ソース管理プラグインは、操作に関連するエラーメッセージまたはステータスメッセージを伝達することがあります。 プラグインは、この目的のために独自のメッセージボックスを表示できます。 ただし、シームレスな統合のために、プラグインは、IDE に文字列を渡すことができます。これにより、状態情報を表示するためのネイティブな方法で表示されます。 この機構は、 `LPTEXTOUTPROC` 関数ポインターです。 IDE では、エラーと状態を表示するために、この関数 (以下で詳しく説明します) が実装されています。

`lpTextOutProc` [Sccopenproject](../extensibility/sccopenproject-function.md)を呼び出すと、IDE は、この関数への関数ポインターをパラメーターとしてソース管理プラグインに渡します。 SCC 操作で、たとえば、多数のファイルが含まれている [Sccget](../extensibility/sccget-function.md) の呼び出しの途中で、プラグインは関数を呼び出して `LPTEXTOUTPROC` 、表示する文字列を定期的に渡すことができます。 これらの文字列は、必要に応じて、ステータスバー、出力ウィンドウ、または別のメッセージボックスに表示されることがあります。 必要に応じて、IDE は **[キャンセル** ] ボタンを使用して特定のメッセージを表示できます。 これにより、ユーザーは操作を取り消すことができ、IDE はこの情報をプラグインに返すことができます。

## <a name="signature"></a>署名
 IDE の出力関数には、次のシグネチャがあります。

```cpp
typedef LONG (*LPTEXTOUTPROC) (
   LPSTR display_string,
   LONG mesg_type
);
```

## <a name="parameters"></a>パラメーター

display_string

表示するテキスト文字列。 この文字列は、復帰または改行で終了することはできません。

mesg_type

メッセージの種類。 次の表に、このパラメーターでサポートされている値を示します。

|値|説明|
|-----------|-----------------|
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|このメッセージは、情報、警告、またはエラーと見なされます。|
|`SCC_MSG_STATUS`|メッセージには状態が表示され、ステータスバーに表示できます。|
|`SCC_MSG_DOCANCEL`|メッセージ文字列なしで送信されました。|
|`SCC_MSG_STARTCANCEL`|**[キャンセル**] ボタンの表示を開始します。|
|`SCC_MSG_STOPCANCEL`|**[キャンセル**] ボタンの表示を停止します。|
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|バックグラウンド操作をキャンセルするかどうかを IDE に要求します。 `SCC_MSG_RTN_CANCEL` 操作が取り消された場合、ide はを返します。それ以外の場合は、を返し `SCC_MSG_RTN_OK` ます。 パラメーターは、 `display_string` ソース管理プラグインによって提供される [Sccmsgdataiscancelled](#LinkSccMsgDataIsCancelled) 構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|バージョンコントロールから取得される前に、ファイルについて IDE に通知します。 パラメーターは、 `display_string` ソース管理プラグインによって提供される [Sccmsgdataonbeforegetfile](#LinkSccMsgDataOnBeforeGetFile) 構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|バージョンコントロールから取得されたファイルを IDE に通知します。 パラメーターは、 `display_string` ソース管理プラグインによって提供される [SccMsgDataOnAfterGetFile](#LinkSccMsgDataOnAfterGetFile) 構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|バックグラウンド操作の現在の状態を IDE に通知します。 パラメーターは、 `display_string` ソース管理プラグインによって提供される [SccMsgDataOnMessage](#LinkSccMsgDataOnMessage) 構造体としてキャストされます。|

## <a name="return-value"></a>戻り値

|値|説明|
|-----------|-----------------|
|SCC_MSG_RTN_OK|文字列が表示されたか、操作が正常に完了しました。|
|SCC_MSG_RTN_CANCEL|ユーザーが操作をキャンセルしようとしています。|

## <a name="example"></a>例
 たとえば、IDE が20個のファイル名で [Sccget](../extensibility/sccget-function.md) を呼び出したとします。 ソース管理プラグインは、ファイル get の途中で操作がキャンセルされないようにしたいと考えています。 各ファイルを取得した後、 `lpTextOutProc` を呼び出し、各ファイルのステータス情報を渡して、 `SCC_MSG_DOCANCEL` 報告するステータスがない場合はメッセージを送信します。 プラグインが IDE からの戻り値を受け取った場合は、 `SCC_MSG_RTN_CANCEL` すぐに取得操作が取り消されるので、それ以上ファイルは取得されません。

## <a name="structures"></a>構造体

### <a name="sccmsgdataiscancelled"></a><a name="LinkSccMsgDataIsCancelled"></a> SccMsgDataIsCancelled れました

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
} SccMsgDataIsCancelled;
```

 この構造体は、メッセージと共に送信され `SCC_MSG_BACKGROUND_IS_CANCELLED` ます。 これは、取り消されたバックグラウンド操作の ID を伝えるために使用されます。

### <a name="sccmsgdataonbeforegetfile"></a><a name="LinkSccMsgDataOnBeforeGetFile"></a> SccMsgDataOnBeforeGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
} SccMsgDataOnBeforeGetFile;
```

 この構造体は、メッセージと共に送信され `SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE` ます。 このメソッドは、取得するファイルの名前、および取得しようとしているバックグラウンド操作の ID を伝えるために使用されます。

### <a name="sccmsgdataonaftergetfile"></a><a name="LinkSccMsgDataOnAfterGetFile"></a> SccMsgDataOnAfterGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
   SCCRTN sResult;
} SccMsgDataOnAfterGetFile;
```

 この構造体は、メッセージと共に送信され `SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE` ます。 これは、指定されたファイルを取得した結果と、取得を行ったバックグラウンド操作の ID を伝えるために使用されます。 結果として得られる結果については、 [Sccget](../extensibility/sccget-function.md) の戻り値を参照してください。

### <a name="sccmsgdataonmessage"></a><a name="LinkSccMsgDataOnMessage"></a> SccMsgDataOnMessage

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szMessage;
   BOOL bIsError;
} SccMsgDataOnMessage;
```

 この構造体は、メッセージと共に送信され `SCC_MSG_BACKGROUND_ON_MESSAGE` ます。 バックグラウンド操作の現在の状態を伝えるために使用されます。 状態は、IDE によって表示される文字列として表され、 `bIsError` メッセージの重要度を示し `TRUE` ます (エラーメッセージの場合 `FALSE` は、警告または情報メッセージの場合)。 ステータスを送信するバックグラウンド操作の ID も指定されています。

## <a name="code-example"></a>コードの例
 `LPTEXTOUTPROC` `SCC_MSG_BACKGROUND_ON_MESSAGE` 呼び出しの構造体をキャストする方法を示す、メッセージを送信する呼び出しの簡単な例を次に示します。

```cpp
LONG SendStatusMessage(
    LPTEXTOUTPROC pTextOutProc,
    DWORD         dwBackgroundID,
    LPCTSTR       pStatusMsg,
    BOOL          bIsError)
{
    SccMsgDataOnMessage msgData = { 0 };
    LONG                result  = 0;

    msgData.dwBackgroundOperationID = dwBackgroundID;
    msgData.szMessage               = pStatusMsg;
    msgData.bIsError                = bIsError;

    result = pTextOutProc(reinterpret_cast<LPCTSTR>(&msgData), SCC_MSG_BACKGROUND_ON_MESSAGE);
    return result;
}
```

## <a name="see-also"></a>こちらもご覧ください
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
