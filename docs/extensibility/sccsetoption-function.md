---
title: 関数の設定 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccSetOption
helpviewer_keywords:
- SccSetOption function
ms.assetid: 4b5e6666-c24c-438a-a9df-9c52f58f8175
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1adcbb47e9fce7037fe8942326e8836ade51e3eb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700310"
---
# <a name="sccsetoption-function"></a>SccSetOption 関数
この関数は、ソース管理プラグインの動作を制御するオプションを設定します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccSetOption(
   LPVOID pvContext,
   LONG   nOption,
   LONG   dwVal
);
```

#### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 nオプション

[in]設定されているオプション。

 ドヴァル

[in]オプションの設定。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|オプションは正常に設定されました。|
|SCC_I_SHARESUBPROJOK|が`nOption`返`SCC_OPT_SHARESUBPROJ`され、ソース管理プラグインによって IDE が宛先フォルダを設定できます。|
|SCC_E_OPNOTSUPPORTED|オプションは設定されておらず、頼りにするべきではありません。|

## <a name="remarks"></a>Remarks
 IDE はこの関数を呼び出して、ソース管理プラグインの動作を制御します。 最初のパラメータ`nOption`は、設定されている値を示し、2 番目の`dwVal`パラメータは、その値をどうするか示します。 プラグインは、この情報をに関連付けて`pvContext``,`保存するため、SccInitialize を呼び出した後に IDE がこの関数を呼び出す必要があります (ただし、SccOpenProject を呼び出した後は必ずしもそうではありません)。 [SccInitialize](../extensibility/sccinitialize-function.md) [SccOpenProject](../extensibility/sccopenproject-function.md)

 オプションとその値の概要:

|`nOption`|`dwValue`|説明|
|---------------|---------------|-----------------|
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|バックグラウンド イベント キューイングを有効または無効にします。|
|`SCC_OPT_USERDATA`|任意の値|[コールバック](../extensibility/optnamechangepfn.md)関数に渡すユーザー値を指定します。|
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|IDE が現在操作の取り消しをサポートしているかどうかを示します。|
|`SCC_OPT_NAMECHANGEPFN`|コールバック関数[への](../extensibility/optnamechangepfn.md)ポインター|名前変更コールバック関数へのポインターを設定します。|
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|IDE がソース管理のユーザー インターフェイスを介してファイルを手動でチェックアウトできるかどうか、またはソース管理プラグインを通じてのみチェックアウトする必要があるかどうかを示します。|
|`SCC_OPT_SHARESUBPROJ`|該当なし|ソース管理プラグインで IDE がローカルプロジェクトフォルダを指定できる場合、プラグインは を返します`SCC_I_SHARESUBPROJOK`。|

## <a name="scc_opt_eventqueue"></a>SCC_OPT_EVENTQUEUE
 が`nOption`有効`SCC_OPT_EVENTQUEUE`な場合、IDE はバックグラウンド処理を無効に (または再度有効にする) 処理を行います。 たとえば、コンパイル時に、IDE はソース管理プラグインに対して、アイドル状態の処理を停止するように指示する場合があります。 コンパイル後、プラグインのイベント キューを最新の状態に保つために、バックグラウンド処理を再度有効にします。 の`SCC_OPT_EVENTQUEUE`値に対応して`nOption`、 、 、`dwVal``SCC_OPT_EQ_ENABLE`および`SCC_OPT_EQ_DISABLE`の 2 つの値が使用できます。

## <a name="scc_opt_hascancelmode"></a>SCC_OPT_HASCANCELMODE
 の`nOption`値が`SCC_OPT_HASCANCELMODE`の場合、IDE では、長い操作をキャンセルできます。 (`dwVal`既定値`SCC_OPT_HCM_NO`) に設定すると、IDE にキャンセル モードが設定されません。 ソース管理プラグインは、ユーザーがキャンセルできるようにする場合は、独自のキャンセル ボタンを提供する必要があります。 `SCC_OPT_HCM_YES`は、IDE が操作をキャンセルする機能を提供していることを示しているので、SCC プラグインは独自の [キャンセル] ボタンを表示する必要はありません。 IDE が`dwVal`に`SCC_OPT_HCM_YES`設定されている場合は、コールバック関数`SCC_MSG_STATUS`に`DOCANCEL`応答し、メッセージ`lpTextOutProc`をコールバック関数に送信する準備が整います ( [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)を参照してください )。 IDE がこの変数を設定しない場合、プラグインはこれら 2 つのメッセージを送信しません。

## <a name="scc_opt_namechangepfn"></a>SCC_OPT_NAMECHANGEPFN
 nOption が に`SCC_OPT_NAMECHANGEPFN`設定され、ソース管理プラグインと IDE の両方で許可されている場合、プラグインはソース管理操作中にファイルの名前を変更したり移動したりできます。 は`dwVal` [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)型の関数ポインターに設定されます。 ソース管理操作中に、プラグインはこの関数を呼び出して、3 つのパラメーターを渡すことができます。 これらは、ファイルの古い名前 (完全修飾パス)、そのファイルの新しい名前 (完全修飾パス)、および IDE に関連する情報へのポインタです。 IDE は、データを指し示`SccSetOption`して`nOption`に`SCC_OPT_USERDATA`設定を`dwVal`指定して呼び出すことによって、この最後のポインターを送信します。 この関数のサポートはオプションです。 この機能を使用する VSSCI プラグは、関数ポインターとユーザー データ変数`NULL`を に初期化する必要があり、名前変更関数を呼び出す必要があります。 また、与えられた値を保持するか、新しい呼び出しに応じて変更する準備をしておく`SccSetOption`必要があります。 これは、ソース管理コマンド操作の途中では発生しませんが、コマンド間で発生する可能性があります。

## <a name="scc_opt_scccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY
 nOption が に`SCC_OPT_SCCCHECKOUTONLY`設定されている場合、IDE は、現在開いているプロジェクト内のファイルをソース管理システムのユーザーインターフェイスを使用して手動でチェックアウトしてはならないことを示しています。 代わりに、ファイルは IDE コントロールのソース管理プラグインを介してのみチェックアウトする必要があります。 に`dwValue``SCC_OPT_SCO_NO`設定されている場合、ファイルはプラグインによって通常どおりに処理され、ソース管理 UI でチェックアウトできます。 に`dwValue``SCC_OPT_SCO_YES`設定されている場合、プラグインのみがファイルのチェックアウトを許可され、ソース管理システムの UI を呼び出す必要はありません。 これは、IDE を使用してチェックアウトするだけの意味のある 「疑似ファイル」が IDE に含まれている可能性がある状況を対象にしています。

## <a name="scc_opt_sharesubproj"></a>SCC_OPT_SHARESUBPROJ
 `SCC_OPT_SHARESUBPROJ`に設定されている場合`nOption`、ソース管理プラグインがソース管理からファイルを追加するときに、指定したローカル フォルダーを使用できるかどうかをテストします。 この場合、`dwVal`パラメータの値は重要ではありません。 プラグインで[、SccAddFromScc](../extensibility/sccaddfromscc-function.md)が呼び出されたときにソース管理からファイルを追加するローカルの保存先フォルダーを IDE が指定できる場合、プラグインは`SCC_I_SHARESUBPROJOK``SccSetOption`関数が呼び出されたときに返す必要があります。 IDE は、関数`lplpFileNames`のパラメータを`SccAddFromScc`使用して、コピー先のフォルダに渡します。 プラグインは、ソース管理から追加されたファイルを配置するために、そのコピー先フォルダーを使用します。 オプションが設定されているときにプラグインが返`SCC_I_SHARESUBPROJOK`されない場合、IDE は、プラグインが現在のローカル フォルダー内のファイルのみを追加できると想定します。 `SCC_OPT_SHARESUBPROJ`

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccAddFromScc](../extensibility/sccaddfromscc-function.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
