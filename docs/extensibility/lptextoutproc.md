---
title: をクリックして |マイクロソフトドキュメント
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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 38c3e8263b9a30058c2de019e5e92160b716aa71
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702787"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC

ユーザーが統合開発環境 (IDE) 内からソース管理操作を実行する場合、ソース管理プラグインは、操作に関連するエラーまたはステータス メッセージを伝える必要があります。 プラグインは、この目的のために独自のメッセージ ボックスを表示できます。 ただし、よりシームレスな統合のために、プラグインは IDE に文字列を渡すことができます。 このメカニズムは`LPTEXTOUTPROC`関数ポインタです。 IDE はエラーとステータスを表示するためにこの機能を実装しています (詳細は後述します)。

[SccOpenProject](../extensibility/sccopenproject-function.md)を呼び出すときに、IDE は、この関数への関数`lpTextOutProc`ポインターをソース管理プラグインに渡します。 SCC 操作中に、たとえば、多くのファイルを含む[SccGet](../extensibility/sccget-function.md)の呼び出しの途中で、プラグインは定期的`LPTEXTOUTPROC`に表示する文字列を渡す関数を呼び出すことができます。 IDE では、これらの文字列をステータス バー、出力ウィンドウ、または別のメッセージ ボックスに表示できます。 オプションで、IDE は **[キャンセル]** ボタンを使用して特定のメッセージを表示できます。 これにより、ユーザーは操作をキャンセルでき、この情報をプラグインに渡すことができます。

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

表示するテキスト文字列。 この文字列は、復帰または改行で終了しないでください。

mesg_type

メッセージの種類。 次の表は、このパラメーターでサポートされる値の一覧です。

|[値]|説明|
|-----------|-----------------|
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|メッセージは、情報、警告、またはエラーと見なされます。|
|`SCC_MSG_STATUS`|メッセージはステータスを示し、ステータスバーに表示できます。|
|`SCC_MSG_DOCANCEL`|メッセージ文字列なしで送信されます。|
|`SCC_MSG_STARTCANCEL`|**[キャンセル]** ボタンの表示を開始します。|
|`SCC_MSG_STOPCANCEL`|**[キャンセル]** ボタンの表示を停止します。|
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|バックグラウンド操作を取り消すかどうかを IDE に確認します`SCC_MSG_RTN_CANCEL`。それ以外の`SCC_MSG_RTN_OK`場合は、 を返します。 パラメーター`display_string`は、ソース管理プラグインによって提供される[SccMsgDataIsIsed](#LinkSccMsgDataIsCancelled)構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|バージョン管理から取得する前に、ファイルに関する IDE に通知します。 パラメーター`display_string`は、ソース管理プラグインによって提供される[SccMsgDataOnBeforeGetFile](#LinkSccMsgDataOnBeforeGetFile)構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|バージョン管理から取得したファイルについて IDE に通知します。 パラメーター`display_string`は、ソース管理プラグインによって提供される[SccMsgDataOnAfterGetFile](#LinkSccMsgDataOnAfterGetFile)構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|バックグラウンド操作の現在の状態を IDE に通知します。 パラメーター`display_string`は、ソース管理プラグインによって提供される[SccMsgDataOnMessage](#LinkSccMsgDataOnMessage)構造体としてキャストされます。|

## <a name="return-value"></a>戻り値

|[値]|説明|
|-----------|-----------------|
|SCC_MSG_RTN_OK|文字列が表示されたか、操作が正常に完了しました。|
|SCC_MSG_RTN_CANCEL|ユーザーは操作をキャンセルします。|

## <a name="example"></a>例
 IDE が 20 のファイル名を持つ[SccGet](../extensibility/sccget-function.md)を呼び出したとします。 ソース管理プラグインは、ファイル取得の途中で操作をキャンセルしないようにします。 各ファイルを取得した後、`lpTextOutProc`各ファイルのステータス情報を渡して呼び出し、`SCC_MSG_DOCANCEL`報告するステータスがない場合はメッセージを送信します。 プラグインが IDE`SCC_MSG_RTN_CANCEL`から戻り値を受け取った場合は、すぐに取得操作をキャンセルし、ファイルが取得されないようにします。

## <a name="structures"></a>構造体

### <a name="sccmsgdataiscancelled"></a><a name="LinkSccMsgDataIsCancelled"></a>キャンセルされたメッセージ

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
} SccMsgDataIsCancelled;
```

 この構造体は、メッセージと`SCC_MSG_BACKGROUND_IS_CANCELLED`共に送信されます。 取り消されたバックグラウンド操作の ID を伝えるために使用されます。

### <a name="sccmsgdataonbeforegetfile"></a><a name="LinkSccMsgDataOnBeforeGetFile"></a>ファイルの前に

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
} SccMsgDataOnBeforeGetFile;
```

 この構造体は、メッセージと`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`共に送信されます。 取得しようとしているファイルの名前と、取得を行っているバックグラウンド操作の ID を伝えるために使用されます。

### <a name="sccmsgdataonaftergetfile"></a><a name="LinkSccMsgDataOnAfterGetFile"></a>取得ファイルの後に

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
   SCCRTN sResult;
} SccMsgDataOnAfterGetFile;
```

 この構造体は、メッセージと`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`共に送信されます。 指定したファイルの取得結果と、取得を行ったバックグラウンド操作の ID を伝えるために使用されます。 結果として与えられるものについては[、SccGet](../extensibility/sccget-function.md)の戻り値を参照してください。

### <a name="sccmsgdataonmessage"></a><a name="LinkSccMsgDataOnMessage"></a>メッセージ

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szMessage;
   BOOL bIsError;
} SccMsgDataOnMessage;
```

 この構造体は、メッセージと`SCC_MSG_BACKGROUND_ON_MESSAGE`共に送信されます。 これは、バックグラウンド操作の現在の状態を通知するために使用されます。 ステータスは、IDE によって表示される文字列として表され`bIsError`、メッセージの重大度 (エラー メッセージ`TRUE`の場合) を示します。`FALSE`警告または情報メッセージの場合)。 ステータスを送信するバックグラウンド操作の ID も指定されます。

## <a name="code-example"></a>コードの例
 以下は、メッセージを送信する`LPTEXTOUTPROC`呼び出`SCC_MSG_BACKGROUND_ON_MESSAGE`しの簡単な例で、呼び出しの構造をキャストする方法を示しています。

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

## <a name="see-also"></a>関連項目
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
