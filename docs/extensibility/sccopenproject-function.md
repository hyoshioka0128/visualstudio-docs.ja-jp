---
title: プロジェクト関数 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
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
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ユーザー数を指定します。

[イン、アウト]ユーザーの名前 (null 終端文字を含むSCC_USER_SIZEを超えないようにします)。

 プファル・プロイナ

[in]プロジェクトの名前を識別する文字列。

 プリュチプチポックプロジパス

[in]プロジェクトの作業フォルダーへのパス。

 プロウプロイパス

[イン、アウト]プロジェクトを識別するオプションの補助文字列 (null 終端文字を含むSCC_AUXPATH_SIZEを超えないようにする)。

 ル・コメント

[in]作成中の新しいプロジェクトにコメントします。

 をクリックします。

[in]ソース管理プラグインからのテキスト出力を表示するオプションのコールバック関数。

 dwFlags

[in]プロジェクトがソース管理プラグインに不明な場合に、新しいプロジェクトを作成する必要があるかどうかを示します。 値は、と の`SCC_OP_CREATEIFNEW`組み合わせとすることができます。`SCC_OP_SILENTOPEN.`

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトを開くことに成功しました。|
|SCC_E_INITIALIZEFAILED|プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーはソース管理システムにログインできませんでした。|
|SCC_E_COULDNOTCREATEPROJECT|プロジェクトは呼び出しの前に存在しませんでした。 フラグ`SCC_OPT_CREATEIFNEW`が設定されましたが、プロジェクトを作成できませんでした。|
|SCC_E_PROJSYNTAXERR|プロジェクト構文が無効です。|
|SCC_E_UNKNOWNPROJECT|プロジェクトがソース管理プラグインに不明であり、フラグが`SCC_OPT_CREATEIFNEW`設定されていません。|
|SCC_E_INVALIDFILEPATH|無効なファイル パスまたは使用できないファイル パスです。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECFICERROR|非特異的な障害。ソース管理システムが初期化されませんでした。|

## <a name="remarks"></a>Remarks
 IDE はユーザー名 ( )`lpUser`を渡すか、空の文字列へのポインタを渡すだけかもしれません。 ユーザー名がある場合、ソース管理プラグインは、既定として使用する必要があります。 ただし、名前が渡されなかった場合、またはログインに指定された名前でログインできなかった場合、プラグインはユーザーにログインを求め SCC_USER_SIZE、`lpUser``.``SCC_USER_LEN`有効なログインを受け取ったときに有効な名前を返す必要があります。

> [!NOTE]
> IDE が実行する必要がある最初の`SccOpenProject`アクションは、関数または[SccGetProjPath](../extensibility/sccgetprojpath-function.md)の呼び出しである場合があります。 このため、両方とも同じ`lpUser`パラメータを持ちます。

 `lpAuxProjPath`を`lpProjName`使用してソリューション ファイルから読み取るか、`SccGetProjPath`関数の呼び出しから返されます。 これらのパラメーターには、ソース管理プラグインがプロジェクトに関連付ける文字列が含まれ、プラグインにのみ意味があります。 このような文字列がソリューション ファイル内になく、ユーザーが参照を求めず (`SccGetProjPath`関数を通じて文字列を返す)、IDE は両方`lpAuxProjPath`の空の文字列を`lpProjName`渡し、この関数が返されるときにこれらの値がプラグインによって更新されることを予期します。

 `lpTextOutProc`は、コマンド結果出力を表示するために、ソース管理プラグインに対して IDE によって提供されるコールバック関数へのポインターです。 このコールバック関数については[、LPTEXTOUTPROC](../extensibility/lptextoutproc.md)で詳しく説明します。

> [!NOTE]
> ソース管理プラグインがこれを利用する場合は`SCC_CAP_TEXTOUT`[、SccInitialize](../extensibility/sccinitialize-function.md)でフラグを設定している必要があります。 そのフラグが設定されていない場合、または IDE がこの機能をサポートしていない場合`lpTextOutProc`は、`NULL`になります。

 この`dwFlags`パラメーターは、開いているプロジェクトが現在存在しない場合の結果を制御します。 2 つのビットフラグ`SCC_OP_CREATEIFNEW`と`SCC_OP_SILENTOPEN`で構成されています。 開いているプロジェクトが既に存在する場合、この関数はプロジェクトを開`SCC_OK`いてを返すだけです。 プロジェクトが存在せず、`SCC_OP_CREATEIFNEW`フラグがオンの場合、ソース管理プラグインは、ソース管理システムでプロジェクトを作成し、開いて、 を返`SCC_OK`すことができます。 プロジェクトが存在せず、フラグが`SCC_OP_CREATEIFNEW`オフの場合、プラグインはフラグをチェックする`SCC_OP_SILENTOPEN`必要があります。 このフラグがオンでない場合、プラグインはユーザーにプロジェクト名の入力を求めるメッセージを表示することがあります。 このフラグがオンの場合、プラグインは単に を`SCC_E_UNKNOWNPROJECT`返す必要があります。

## <a name="calling-order"></a>呼び出し順序
 通常のイベントでは[、SccInitialize](../extensibility/sccinitialize-function.md)が最初に呼び出され、ソース管理セッションが開かれます。 セッションは、 への呼び出`SccOpenProject`しと、その後に他のソース管理プラグイン API 関数呼び出しで構成され[、SccCloseProject](../extensibility/scccloseproject-function.md)への呼び出しで終了します。 このようなセッションは[、SccUninitialize](../extensibility/sccuninitialize-function.md)が呼び出される前に数回繰り返されることがあります。

 ソース管理プラグインが ビット`SCC_CAP_REENTRANT``SccInitialize`を に設定すると、上記のセッションシーケンスが並列で何度も繰り返されることがあります。 異`pvContext`なる構造は、各`pvContext`セッションが一度に 1 つの開いているプロジェクトに関連付けられている異なるセッションを追跡します。 プラグインは、`pvContext`パラメーターに基づいて、特定の呼び出しで参照されるプロジェクトを判別できます。 機能ビット`SCC_CAP_REENTRANT`が設定されていない場合、未再入可能なソース管理プラグインは、複数のプロジェクトで作業する能力に制限されます。

> [!NOTE]
> この`SCC_CAP_REENTRANT`ビットは、ソース管理プラグイン API のバージョン 1.1 で導入されました。 バージョン 1.0 では設定されていないか無視され、すべてのバージョン 1.0 ソース管理プラグインは再入不能であると見なされます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [文字列長の制限](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
