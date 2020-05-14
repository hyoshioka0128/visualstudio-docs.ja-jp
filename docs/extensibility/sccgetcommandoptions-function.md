---
title: 関数を選択する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: eeefa26422476ca40e782df3ff35eee9d429a149
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700834"
---
# <a name="sccgetcommandoptions-function"></a>関数
この関数は、特定のコマンドの詳細オプションをユーザーに求めます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetCommandOptions(
   LPVOID pvContext,
   HWND hWnd,
   enum SCCCOMMAND iCommand,
   LPCMDOPTS* ppvOptions
);
```

### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 Icommand

[in]拡張オプションが要求されるコマンド (可能な値については[、コマンド・コード](../extensibility/command-code-enumerator.md)を参照してください)。

 オプション

[in]オプション構造 (も可能`NULL`)

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|正常終了しました。|
|SCC_I_ADV_SUPPORT|ソース管理プラグインは、コマンドの詳細オプションをサポートします。|
|SCC_I_OPERATIONCANCELED|ユーザーは、ソース管理プラグインの **[オプション]** ダイアログ ボックスをキャンセルしました。|
|SCC_E_OPTNOTSUPPORTED|ソース管理プラグインは、この操作をサポートしていません。|
|SCC_E_ISCHECKEDOUT|現在チェックアウトされているファイルに対してこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 IDE は、ソース管理プラグインが指定された`ppvOptions`=`NULL`コマンドの詳細オプション機能をサポートしているかどうかを判断するために、この関数を初めて呼び出します。 プラグインがそのコマンドの機能をサポートしている場合、IDE は、ユーザーが詳細オプション (通常はダイアログ ボックスの **[詳細]** ボタンとして実装) を要求したときに、この関数を再度呼び`ppvOptions`出し、ポインター`NULL`を指す NULL 以外のポインターを提供します。 プラグインは、ユーザーが指定した詳細オプションをプライベート構造体に格納し、 内の`ppvOptions`その構造体へのポインターを返します。 この構造体は、その関数の後続の呼び出しを含め、その関数について知る必要がある他のすべてのソース`SccGetCommandOptions`管理プラグイン API 関数に渡されます。

 例を挙すると、この状況を明確にする場合があります。

 ユーザーが **[取得**] コマンドを選択すると、IDE に [**取得**] ダイアログ ボックスが表示されます。 IDE は、`SccGetCommandOptions`関数を`iCommand`に`SCC_COMMAND_GET`設定`ppvOptions`し、`NULL`に設定して関数を呼び出します。 これは、ソース管理プラグインによって、「このコマンドの詳細オプションはありますか」という質問として解釈されます。 プラグインが戻る`SCC_I_ADV_SUPPORT`場合、IDE は **[取得**]ダイアログ ボックスに **[詳細設定**] ボタンを表示します。

 ユーザーが [**詳細設定**] ボタンをクリックすると、今度はポインターを`SccGetCommandOptions`指す非-を`NULL``ppvOptions`使用して、関数が`NULL`再度呼び出されます。 プラグインは、独自の **[Get Options]** ダイアログ ボックスを表示し、ユーザーに情報を求め、その情報を独自の`ppvOptions`構造に入れ、その構造体へのポインタを 返します。

 ユーザーが同じダイアログ ボックスで **[詳細設定**] を再度クリックすると`SccGetCommandOptions`、IDE は`ppvOptions`、変更せずに関数を再度呼び出し、構造体がプラグインに戻されます。 これにより、プラグインは、ユーザーが以前に設定した値に対してダイアログ ボックスを再初期化できます。 プラグインは、返す前にインプレースの構造を変更します。

 最後に、IDE の **[取得**] ダイアログ ボックスでユーザーが **[OK] を**クリックすると、IDE は`ppvOptions`[SccGet](../extensibility/sccget-function.md)を呼び出し、詳細オプションを含むで返される構造体を渡します。

> [!NOTE]
> このコマンド`SCC_COMMAND_OPTIONS`は、IDE が **[オプション]** ダイアログ ボックスを表示するときに使用され、統合の動作を制御する環境設定をユーザーが設定できるようにします。 ソース管理プラグインが独自の環境設定ダイアログボックスを提供する場合は、IDE の環境設定ダイアログボックスの **[詳細設定**]ボタンから表示できます。 プラグインは、この情報を取得し、永続化する責任を負います。IDE は、IDE で使用したり、変更したりしません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [コマンド コード](../extensibility/command-code-enumerator.md)
