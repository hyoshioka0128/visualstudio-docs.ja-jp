---
title: SccGetProjPath 関数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700701"
---
# <a name="sccgetprojpath-function"></a>SccGetProjPath 関数
この関数は、ソース管理プラグインにのみ意味のある文字列であるプロジェクトパスをユーザーに要求します。 これは、ユーザーが次の場合に呼び出されます。

- 新しいプロジェクトの作成

- 既存のプロジェクトをバージョン管理に追加する

- 既存のバージョンコントロールプロジェクトを検索しようとしています

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
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力]ユーザー名 (NULL 終端文字を含む SCC_USER_SIZE を超えることはできません)

 lpProjName

[入力、出力]IDE プロジェクト、プロジェクトワークスペース、またはメイクファイルの名前。 NULL 終端文字を含め、SCC_PRJPATH_SIZE を超えないようにします。

 lpLocalPath

[入力、出力]プロジェクトの作業パス。 がの場合 `bAllowChangePath` `TRUE` 、ソース管理プラグインはこの文字列を変更できます (null ターミネータを含む _MAX_PATH を超えることはできません)。

 lpAuxProjPath

[入力、出力]返されたプロジェクトパスのバッファー。 NULL 終端文字を含め、SCC_PRJPATH_SIZE を超えないようにします。

 bAllowChangePath

からこれがの場合 `TRUE` 、ソース管理プラグインは文字列の入力を要求したり、変更したりでき `lpLocalPath` ます。

 pbNew

[入力、出力][受信した値は、新しいプロジェクトを作成するかどうかを示します。 返される値は、プロジェクトの作成が成功したことを示します。

|受信|解釈|
|--------------|--------------------|
|TRUE|ユーザーは、新しいプロジェクトを作成できます。|
|FALSE|ユーザーは、新しいプロジェクトを作成することはできません。|

|送信|解釈|
|--------------|--------------------|
|TRUE|新しいプロジェクトが作成されました。|
|FALSE|既存のプロジェクトが選択されました。|

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトが正常に作成または取得されました。|
|SCC_I_OPERATIONCANCELED|操作は取り消されました。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。|
|SCC_E_CONNECTIONFAILURE|ソース管理システムに接続しようとして問題が発生しました。|
|SCC_E_NONSPECIFICERROR|未指定のエラーが発生しました。|

## <a name="remarks"></a>注釈
 この関数の目的は、IDE でパラメーターとを取得することです `lpProjName` `lpAuxProjPath` 。 ソース管理プラグインは、この情報の入力をユーザーに求めた後、これらの2つの文字列を IDE に戻します。 IDE では、ソリューションファイルにこれらの文字列が保持され、ユーザーがこのプロジェクトを開くたびに [Sccopenproject](../extensibility/sccopenproject-function.md) に渡されます。 これらの文字列を使用すると、プラグインはプロジェクトに関連付けられている情報を追跡できます。

 関数が最初に呼び出されると、 `lpAuxProjPath` は空の文字列に設定されます。 `lProjName` 空の場合もあります。また、ソース管理プラグインが使用または無視する IDE プロジェクト名が含まれている場合もあります。 関数が正常にを返した場合、プラグインは、対応する2つの文字列を返します。 IDE では、これらの文字列に関する仮定は行われず、使用されません。ユーザーが変更することはできません。 ユーザーが設定を変更したい場合は、IDE が再びを呼び出して、 `SccGetProjPath` 以前の時刻と同じ値を渡します。 これにより、プラグインはこれら2つの文字列を完全に制御できます。

 の場合、 `lpUser` IDE はユーザー名を渡すことができます。または、単に空の文字列へのポインターを渡すこともできます。 ユーザー名がある場合は、ソース管理プラグインで既定値として使用する必要があります。 ただし、名前が渡されなかった場合、またはログインが指定された名前で失敗した場合、プラグインはユーザーにログインを求めるプロンプトを表示し、 `lpUser` 有効なログインを受け取ったときにその名前を再度渡します。 この文字列はプラグインによって変更される可能性があるため、IDE では常にサイズ (+ 1) のバッファーが割り当てられ `SCC_USER_LEN` ます。

> [!NOTE]
> IDE によって実行される最初のアクションは、関数または関数を呼び出すことができ `SccOpenProject` `SccGetProjPath` ます。 そのため、どちらにも同一のパラメーターがあり `lpUser` ます。これにより、ソース管理プラグインは、ユーザーをいつでもログインできます。 関数からの戻り値がエラーを示す場合でも、プラグインはこの文字列に有効なログイン名を入力する必要があります。

 `lpLocalPath` は、ユーザーがプロジェクトを保持するディレクトリです。 空の文字列の場合もあります。 現在定義されているディレクトリが存在しない場合 (ユーザーがソース管理システムからプロジェクトをダウンロードしようとした場合など)、がの場合、 `bAllowChangePath` `TRUE` ソース管理プラグインはユーザーに入力を要求するか、他のメソッドを使用して独自の文字列をに配置することができ `lpLocalPath` ます。 がの場合 `bAllowChangePath` `FALSE` 、ユーザーは指定されたディレクトリで既に作業しているため、プラグインは文字列を変更しないようにする必要があります。

 ユーザーがソース管理下に配置される新しいプロジェクトを作成する場合は、が呼び出されたときにソース管理プラグインによって実際にソース管理システムに作成されないことがあり `SccGetProjPath` ます。 代わりに、文字列をの0以外の値と共に返し `pbNew` ます。これは、プロジェクトがソース管理システムで作成されることを示します。

 たとえば、Visual Studio の **新しいプロジェクト** ウィザードのユーザーがプロジェクトをソース管理に追加すると、visual studio はこの関数を呼び出します。このプラグインは、visual studio プロジェクトを格納するための新しいプロジェクトをソース管理システムに作成することができているかどうかを判断します。 ウィザードを完了する前にユーザーが **[キャンセル]** をクリックした場合、プロジェクトは作成されません。 ユーザーが **[OK]** をクリックすると、Visual Studio はを呼び出し、を `SccOpenProject` 渡し `SCC_OPT_CREATEIFNEW` ます。その時点で、ソース管理されたプロジェクトが作成されます。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
