---
title: 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetProjPath
helpviewer_keywords:
- SccGetProjPath function
ms.assetid: 1079847e-d45f-4cb8-9d92-1e01ce5d08f6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 281787da3499c081fbbe6f59b7b8175a4dbf24d7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700701"
---
# <a name="sccgetprojpath-function"></a>関数
この関数は、ソース管理プラグインにのみ意味のある文字列であるプロジェクト パスを指定するようにユーザーに求めます。 これは、ユーザーが次の場合に呼び出されます。

- 新しいプロジェクトの作成

- 既存のプロジェクトをバージョン管理に追加する

- 既存のバージョン管理プロジェクトを検索しようとしています

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetProjPath (
   LPVOID pvContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPSTR  lpProjName,
   LPSTR  lpLocalPath,
   LPSTR  lpAuxProjPath,
   BOOL   bAllowChangePath,
   LPBOOL pbNew
);
```

### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ユーザー数を指定します。

[イン、アウト]ユーザー名 (NULL 終端文字を含むSCC_USER_SIZEを超えないようにする)

 プファル・プロイナ

[イン、アウト]IDE プロジェクト、プロジェクト ワークスペース、またはメイクファイルの名前 (null 終端文字を含むSCC_PRJPATH_SIZEを超えないようにします)。

 ローカルパス

[イン、アウト]プロジェクトの作業パス。 が`bAllowChangePath`場合`TRUE`、ソース管理プラグインはこの文字列を変更できます (null 終端文字を含む_MAX_PATHを超えないようにしてください)。

 プロウプロイパス

[イン、アウト]返されたプロジェクト パスのバッファー (null 終端文字を含むSCC_PRJPATH_SIZEを超えないようにします)。

 パスを変更する

[in]が場合、`TRUE`ソース管理プラグインは`lpLocalPath`文字列の入力を求め、変更できます。

 pbNew

[イン、アウト][値が入る] は、新しいプロジェクトを作成するかどうかを示します。 返された値は、プロジェクトの作成が成功したことを示します。

|受信|解釈|
|--------------|--------------------|
|TRUE|ユーザーは新しいプロジェクトを作成できます。|
|FALSE|ユーザーは新しいプロジェクトを作成できません。|

|送信|解釈|
|--------------|--------------------|
|TRUE|新しいプロジェクトが作成されました。|
|FALSE|既存のプロジェクトが選択されました。|

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトが正常に作成または取得されました。|
|SCC_I_OPERATIONCANCELED|操作が取り消されました。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。|
|SCC_E_CONNECTIONFAILURE|ソース管理システムへの接続に問題が発生しました。|
|SCC_E_NONSPECIFICERROR|未指定のエラーが発生しました。|

## <a name="remarks"></a>Remarks
 この関数の目的は、IDE がパラメータ`lpProjName`を取得することです。 `lpAuxProjPath` ソース管理プラグインは、この情報の入力を求めるメッセージをユーザーに求めた後、これらの 2 つの文字列を IDE に返します。 IDE は、これらの文字列をソリューション ファイルに保存し、ユーザーがこのプロジェクトを開くたびに[SccOpenProject](../extensibility/sccopenproject-function.md)に渡します。 これらの文字列を使用すると、プラグインはプロジェクトに関連付けられた情報を追跡できます。

 関数が最初に呼び出`lpAuxProjPath`されたときは、空の文字列に設定されます。 `lProjName`また、ソース管理プラグインが使用または無視する IDE プロジェクト名を含む場合もあります。 関数が正常に戻ると、プラグインは対応する 2 つの文字列を返します。 IDE はこれらの文字列について何も想定せず、使用せず、ユーザーが変更することを許可しません。 ユーザーが設定を変更する場合、IDE は、前`SccGetProjPath`の時刻に受信した値を渡して、再度呼び出します。 これにより、プラグインは、これらの 2 つの文字列を完全に制御できます。

 の`lpUser`場合、IDE はユーザー名を渡すか、空の文字列へのポインタを渡すだけです。 ユーザー名がある場合、ソース管理プラグインは、既定として使用する必要があります。 ただし、名前が渡されなかった場合、またはログインが指定された名前で失敗した場合、プラグインはユーザーにログインを求め、有効なログインを`lpUser`受け取ったときに名前を戻す必要があります。 プラグインはこの文字列を変更する可能性があるため、IDE は常にサイズ (+1)`SCC_USER_LEN`のバッファを割り当てます。

> [!NOTE]
> IDE が実行する最初のアクションは、関数または関数の`SccOpenProject`呼び出`SccGetProjPath`しです。 したがって、両方とも同じ`lpUser`パラメータを持ち、ソース管理プラグインは、いずれかの時点でユーザーをログインできます。 関数からの戻り値が失敗を示している場合でも、プラグインはこの文字列に有効なログイン名を入力する必要があります。

 `lpLocalPath`は、ユーザーがプロジェクトを保持しているディレクトリです。 空の文字列である可能性があります。 (ソース管理システムからプロジェクトをダウンロードしようとするユーザーの場合のように) 現在定義されているディレクトリがない場合`bAllowChangePath`、ソース管理プラグインは`TRUE`、ユーザーに入力を求めるか、または他の方法を使用して独自の文字列を`lpLocalPath`に配置できます。 `FALSE`が存在する場合`bAllowChangePath`、ユーザーは指定されたディレクトリで既に作業しているため、プラグインは文字列を変更しないでください。

 ユーザーがソース管理下に置く新しいプロジェクトを作成した場合、ソース管理プラグインは、呼び出された時点`SccGetProjPath`でソース管理システムで実際に作成されない可能性があります。 代わりに、ソース管理システムでプロジェクトが作成されることを示す、0`pbNew`以外の値と共に文字列を返します。

 たとえば、Visual Studio の**新しいプロジェクト**ウィザードのユーザーがプロジェクトをソース管理に追加すると、Visual Studio はこの関数を呼び出し、プラグインは、Visual Studio プロジェクトを含むソース管理システムで新しいプロジェクトを作成できるかどうかを判断します。 ウィザードを完了する前にユーザーが **[キャンセル]** をクリックした場合、プロジェクトは作成されません。 ユーザーが **[OK]** をクリックすると`SccOpenProject`、Visual `SCC_OPT_CREATEIFNEW`Studio が を呼び出し、 を渡すと、ソース管理されたプロジェクトがその時点で作成されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
