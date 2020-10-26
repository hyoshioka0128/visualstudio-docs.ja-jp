---
title: SccOpenProject 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccOpenProject
helpviewer_keywords:
- SccOpenProject function
ms.assetid: d609510b-660a-46d7-b93d-2406df20434d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fbf566e593bb1ddbc31c70de1570d746a14fbdcf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700567"
---
# <a name="sccopenproject-function"></a>SccOpenProject 関数
この関数は、既存のソース管理プロジェクトを開くか、新しいプロジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccOpenProject (
   LPVOID        pvContext,
   HWND          hWnd,
   LPSTR         lpUser,
   LPCSTR        lpProjName,
   LPCSTR        lpLocalProjPath,
   LPSTR         lpAuxProjPath,
   LPCSTR        lpComment,
   LPTEXTOUTPROC lpTextOutProc,
   LONG          dwFlags
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力](NULL ターミネータを含む) SCC_USER_SIZE を超えないユーザーの名前。

 lpProjName

からプロジェクトの名前を識別する文字列。

 lpLocalProjPath

からプロジェクトの作業フォルダーへのパス。

 lpAuxProjPath

[入力、出力]プロジェクトを識別する補助文字列 (NULL 終端文字を含む SCC_AUXPATH_SIZE を超えない)。

 lpComment

から作成する新しいプロジェクトにコメントを追加します。

 lpTextOutProc

からソース管理プラグインからのテキスト出力を表示するオプションのコールバック関数。

 dwFlags

からプロジェクトがソース管理プラグインに対して不明な場合に、新しいプロジェクトを作成する必要があるかどうかを通知します。 値は、との組み合わせにすることができます。 `SCC_OP_CREATEIFNEW``SCC_OP_SILENTOPEN.`

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトを開く操作に成功します。|
|SCC_E_INITIALIZEFAILED|プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーは、ソース管理システムにログインできませんでした。|
|SCC_E_COULDNOTCREATEPROJECT|呼び出しの前にプロジェクトが存在しませんでした。 `SCC_OPT_CREATEIFNEW` フラグが設定されましたが、プロジェクトを作成できませんでした。|
|SCC_E_PROJSYNTAXERR|プロジェクトの構文が無効です。|
|SCC_E_UNKNOWNPROJECT|プロジェクトがソース管理プラグインに対して不明であり、 `SCC_OPT_CREATEIFNEW` フラグが設定されていません。|
|SCC_E_INVALIDFILEPATH|ファイルパスが無効であるか、使用できません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECFICERROR|不特定のエラーです。ソース管理システムが初期化されませんでした。|

## <a name="remarks"></a>注釈
 IDE はユーザー名 () を渡すことができ `lpUser` ます。または、単に空の文字列へのポインターを渡すこともできます。 ユーザー名がある場合は、ソース管理プラグインで既定値として使用する必要があります。 ただし、名前が渡されなかった場合、またはログインが指定された名前で失敗した場合、プラグインはユーザーにログインを求めるプロンプトを表示し、有効なログインを受け取ったときにの有効な名前を返します。これは、プラグインによっ `lpUser` `.` てユーザー名の SCC_USER_SIZE 文字列が変更される可能性があるためです `SCC_USER_LEN` 。

> [!NOTE]
> IDE が実行する必要のある最初のアクションは、 `SccOpenProject` 関数または [Sccgetprojpath](../extensibility/sccgetprojpath-function.md)の呼び出しである可能性があります。 このため、両方に同じパラメーターがあり `lpUser` ます。

 `lpAuxProjPath` と `lpProjName` は、ソリューションファイルから読み取られるか、関数の呼び出しから返され `SccGetProjPath` ます。 これらのパラメーターには、ソース管理プラグインによってプロジェクトに関連付けられ、プラグインにのみ意味がある文字列が含まれています。 ソリューションファイルにこのような文字列が含まれておらず、ユーザーが参照するように求められていない場合 (関数を通じて文字列が返される場合 `SccGetProjPath` )、IDE はとの両方に空の文字列を渡し、 `lpAuxProjPath` `lpProjName` この関数が返されたときにこれらの値がプラグインによって更新されることを想定します。

 `lpTextOutProc` は、コマンドの結果出力を表示するために IDE によってソース管理プラグインに提供されるコールバック関数へのポインターです。 このコールバック関数の詳細については、「 [Lptextoutproc](../extensibility/lptextoutproc.md)」を参照してください。

> [!NOTE]
> ソース管理プラグインがこの機能を利用する場合は、 `SCC_CAP_TEXTOUT` [Sccinitialize](../extensibility/sccinitialize-function.md)でフラグを設定する必要があります。 このフラグが設定されていない場合、または IDE がこの機能をサポートしていない場合、はになり `lpTextOutProc` `NULL` ます。

 パラメーターは、 `dwFlags` 開いているプロジェクトが現在存在していないイベントの結果を制御します。 これは、との2つのビットフラグで構成さ `SCC_OP_CREATEIFNEW` `SCC_OP_SILENTOPEN` れます。 開いているプロジェクトが既に存在する場合、この関数は単にプロジェクトを開き、を返し `SCC_OK` ます。 プロジェクトが存在しない場合、 `SCC_OP_CREATEIFNEW` フラグがオンの場合、ソース管理プラグインは、ソース管理システムでプロジェクトを作成して開き、を返すことができ `SCC_OK` ます。 プロジェクトが存在しない場合、フラグがオフになっている場合は、 `SCC_OP_CREATEIFNEW` プラグインがフラグを確認する必要があり `SCC_OP_SILENTOPEN` ます。 このフラグがオンになっていない場合は、プラグインによってユーザーにプロジェクト名の入力が求められることがあります。 このフラグがオンの場合、プラグインは単にを返す必要があり `SCC_E_UNKNOWNPROJECT` ます。

## <a name="calling-order"></a>呼び出し順序
 通常のイベントでは、最初に [Sccinitialize](../extensibility/sccinitialize-function.md) を呼び出してソース管理セッションを開きます。 セッションは、の呼び出しで構成 `SccOpenProject` され、その後に他のソース管理プラグイン API 関数呼び出しが含まれる場合があり、 [Scccloseproject](../extensibility/scccloseproject-function.md)の呼び出しで終了します。 このようなセッションは、 [Sccuninitialize](../extensibility/sccuninitialize-function.md) 解除が呼び出される前に何度も繰り返される場合があります。

 ソース管理プラグインによってのビットが設定されている場合、 `SCC_CAP_REENTRANT` `SccInitialize` 上記のセッションシーケンスは並列で何度も繰り返される可能性があります。 さまざまな `pvContext` 構造が異なるセッションを追跡します。各セッションは、一度 `pvContext` に1つの開いているプロジェクトに関連付けられています。 パラメーターに基づいて、 `pvContext` プラグインは特定の呼び出しで参照されているプロジェクトを特定できます。 機能ビットが設定されて `SCC_CAP_REENTRANT` いない場合、非再入可能なソース管理プラグインは、複数のプロジェクトで作業できるように制限されます。

> [!NOTE]
> この `SCC_CAP_REENTRANT` ビットは、ソース管理プラグイン API のバージョン1.1 で導入されました。 バージョン1.0 では設定されていないか、または無視され、すべてのバージョン1.0 ソース管理プラグインは再入可能でないと見なされます。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [文字列長の制限](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
