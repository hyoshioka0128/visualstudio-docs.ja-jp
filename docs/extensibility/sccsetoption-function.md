---
description: この関数は、ソース管理プラグインの動作を制御するオプションを設定します。
title: SccSetOption 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccSetOption
helpviewer_keywords:
- SccSetOption function
ms.assetid: 4b5e6666-c24c-438a-a9df-9c52f58f8175
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 031de256b231bbd95e7535af80448db5140cba7e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090149"
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
 pvContext

からソース管理プラグインのコンテキスト構造。

 いいえ

から設定するオプション。

 dwVal

からオプションの設定。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|オプションが正常に設定されました。|
|SCC_I_SHARESUBPROJOK|がの場合に返され `nOption` `SCC_OPT_SHARESUBPROJ` ます。ソース管理プラグインでは、IDE でターゲットフォルダーを設定できます。|
|SCC_E_OPNOTSUPPORTED|オプションが設定されていないため、依存しないようにする必要があります。|

## <a name="remarks"></a>注釈
 IDE は、この関数を呼び出して、ソース管理プラグインの動作を制御します。 最初のパラメーターは、 `nOption` 設定される値を示します。2番目のパラメーターは、 `dwVal` その値の処理方法を示します。 プラグインは、に関連付けられたこの情報を格納するので、 `pvContext``,` IDE は [Sccinitialize](../extensibility/sccinitialize-function.md) を呼び出した後にこの関数を呼び出す必要があります (ただし、 [sccopenproject](../extensibility/sccopenproject-function.md)の各呼び出しの後では必ずしも必要ではありません)。

 オプションとその値の概要:

|`nOption`|`dwValue`|Description|
|---------------|---------------|-----------------|
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|バックグラウンドイベントキューを有効または無効にします。|
|`SCC_OPT_USERDATA`|任意の値|[Optnamechangepfn](../extensibility/optnamechangepfn.md)コールバック関数に渡されるユーザー値を指定します。|
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|IDE が現在操作のキャンセルをサポートしているかどうかを示します。|
|`SCC_OPT_NAMECHANGEPFN`|[Optnamechangepfn](../extensibility/optnamechangepfn.md)コールバック関数へのポインター|名前変更コールバック関数へのポインターを設定します。|
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|IDE で、ソース管理ユーザーインターフェイスを使用して手動でファイルのチェックアウトを許可するか、ソース管理プラグインを通じてのみチェックアウトする必要があるかを示します。|
|`SCC_OPT_SHARESUBPROJ`|該当なし|ソース管理プラグインで IDE でローカルプロジェクトフォルダーを指定できる場合、プラグインはを返し `SCC_I_SHARESUBPROJOK` ます。|

## <a name="scc_opt_eventqueue"></a>SCC_OPT_EVENTQUEUE
 がの場合 `nOption` `SCC_OPT_EVENTQUEUE` 、IDE はバックグラウンド処理を無効 (または再有効化) しています。 たとえば、コンパイル中に、IDE はソース管理プラグインに対して、任意の種類のアイドル状態の処理を停止するように指示する場合があります。 コンパイル後、プラグインのイベントキューを最新の状態に保つために、バックグラウンド処理を再び有効にします。 の値に対応するには、、、 `SCC_OPT_EVENTQUEUE` `nOption` およびの2つの値を使用でき `dwVal` `SCC_OPT_EQ_ENABLE` `SCC_OPT_EQ_DISABLE` ます。

## <a name="scc_opt_hascancelmode"></a>SCC_OPT_HASCANCELMODE
 の値がの `nOption` 場合 `SCC_OPT_HASCANCELMODE` 、IDE ではユーザーが長い操作を取り消すことができます。 `dwVal`を `SCC_OPT_HCM_NO` (既定値) に設定すると、IDE にキャンセルモードがないことを示します。 ユーザーがキャンセルできるようにするには、ソース管理プラグインが独自の [キャンセル] ボタンを提供している必要があります。 `SCC_OPT_HCM_YES` IDE が操作をキャンセルする機能を提供することを示します。そのため、SCC プラグインでは、独自の [キャンセル] ボタンを表示する必要がありません。 IDE がに設定されている場合 `dwVal` `SCC_OPT_HCM_YES` 、 `SCC_MSG_STATUS` `DOCANCEL` コールバック関数に送信されたメッセージとメッセージに応答する準備が `lpTextOutProc` あります (「 [lptextoutproc](../extensibility/lptextoutproc.md)」を参照してください)。 IDE でこの変数が設定されていない場合、プラグインはこれら2つのメッセージを送信しません。

## <a name="scc_opt_namechangepfn"></a>SCC_OPT_NAMECHANGEPFN
 NOption がに設定され `SCC_OPT_NAMECHANGEPFN` ていて、ソース管理プラグインと IDE の両方で許可されている場合、プラグインは実際にソース管理操作中にファイルの名前変更や移動を行うことができます。 は、 `dwVal` [Optnamechangepfn](../extensibility/optnamechangepfn.md)型の関数ポインターに設定されます。 ソース管理操作中に、プラグインはこの関数を呼び出して、3つのパラメーターを渡すことができます。 これらは、ファイルの古い名前 (完全修飾パスを持つ)、そのファイルの新しい名前 (完全修飾パス)、および IDE に関連する情報へのポインターです。 IDE は、 `SccSetOption` `nOption` データをポイントするをに設定してを呼び出すことにより、この最後のポインターでを送信し `SCC_OPT_USERDATA` `dwVal` ます。 この関数のサポートは省略可能です。 この機能を使用する VSSCI プラグは、関数ポインターとユーザーデータ変数をに初期化する必要があり `NULL` ます。また、名前を指定していない場合は、rename 関数を呼び出すことはできません。 また、指定された値を保持するように準備するか、への新しい呼び出しに応じて変更する必要があり `SccSetOption` ます。 これは、ソース管理コマンド操作の途中では発生しませんが、コマンド間で発生する可能性があります。

## <a name="scc_opt_scccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY
 NOption がに設定されている場合 `SCC_OPT_SCCCHECKOUTONLY` 、IDE は、現在開いているプロジェクト内のファイルをソース管理システムのユーザーインターフェイスを介して手動でチェックアウトしないことを示します。 代わりに、ファイルをチェックアウトするには、IDE コントロールのソース管理プラグインを使用する必要があります。 がに設定されている場合は、 `dwValue` `SCC_OPT_SCO_NO` ファイルがプラグインによって正常に処理され、ソース管理 UI でチェックアウトできることを意味します。 がに設定されている場合は、 `dwValue` `SCC_OPT_SCO_YES` プラグインのみがファイルのチェックアウトを許可され、ソース管理システムの UI を呼び出すことはできません。 これは、ide に "擬似ファイル" が含まれている可能性があります。この場合、IDE でのみチェックアウトするのが理にかなっています。

## <a name="scc_opt_sharesubproj"></a>SCC_OPT_SHARESUBPROJ
 `nOption`がに設定されている場合 `SCC_OPT_SHARESUBPROJ` 、IDE はソース管理プラグインがソース管理からファイルを追加するときに、指定したローカルフォルダーを使用できるかどうかをテストします。 この場合、パラメーターの値は `dwVal` 問題になりません。 プラグインで、 [Sccaddfromscc](../extensibility/sccaddfromscc-function.md) が呼び出されたときにソース管理からファイルが追加されるローカルの保存先フォルダーを IDE で指定できる場合、プラグインは `SCC_I_SHARESUBPROJOK` 関数が呼び出されたときにを返す必要があり `SccSetOption` ます。 次に、IDE は関数のパラメーターを使用して、 `lplpFileNames` `SccAddFromScc` 出力先フォルダーを渡します。 プラグインは、このコピー先フォルダーを使用して、ソース管理から追加されたファイルを配置します。 オプションを設定したときにプラグインが戻らない場合、IDE では、 `SCC_I_SHARESUBPROJOK` `SCC_OPT_SHARESUBPROJ` プラグインが現在のローカルフォルダーにのみファイルを追加できることを前提としています。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccAddFromScc](../extensibility/sccaddfromscc-function.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
