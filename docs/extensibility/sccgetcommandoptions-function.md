---
description: この関数は、指定されたコマンドの詳細オプションをユーザーに要求します。
title: SccGetCommandOptions 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 400b778cf5e26b0cabad0fb19c548b2faa0a803f
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220808"
---
# <a name="sccgetcommandoptions-function"></a>SccGetCommandOptions 関数
この関数は、指定されたコマンドの詳細オプションをユーザーに要求します。

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
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 iCommand

から詳細オプションが要求されるコマンド (使用可能な値については、 [コマンドコード](../extensibility/command-code-enumerator.md) を参照してください)。

 ppvOptions

からオプションの構造体 (を指定することもでき `NULL` ます)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|正常終了しました。|
|SCC_I_ADV_SUPPORT|ソース管理プラグインは、コマンドの高度なオプションをサポートしています。|
|SCC_I_OPERATIONCANCELED|ユーザーがソース管理プラグインの [ **オプション** ] ダイアログボックスをキャンセルしました。|
|SCC_E_OPTNOTSUPPORTED|ソース管理プラグインでは、この操作はサポートされていません。|
|SCC_E_ISCHECKEDOUT|現在チェックアウトされているファイルに対してこの操作を実行することはできません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 IDE は、を使用してこの関数を初めて呼び出し、 `ppvOptions` = `NULL` ソース管理プラグインが指定されたコマンドの詳細オプション機能をサポートしているかどうかを判断します。 プラグインがそのコマンドの機能をサポートしている場合、IDE は、ユーザーが詳細オプション (通常はダイアログボックスの **[詳細設定** ] ボタンとして実装されている) を要求し、ポインターをポイントするための NULL 以外のポインターを提供すると、この関数を再度呼び出し `ppvOptions` `NULL` ます。 プラグインには、ユーザーが指定した詳細設定オプションがプライベート構造で格納され、その構造体へのポインターが返され `ppvOptions` ます。 その後、この構造体は、その後の関数の呼び出しを含め、そのことを把握しておく必要がある他のすべてのソース管理プラグイン API 関数に渡され `SccGetCommandOptions` ます。

 例を使用すると、この状況を明確にすることができます。

 ユーザーが **get** コマンドを選択すると、IDE に [ **取得** ] ダイアログボックスが表示されます。 IDE は、 `SccGetCommandOptions` `iCommand` をに設定し、 `SCC_COMMAND_GET` `ppvOptions` をに設定して、関数を呼び出し `NULL` ます。 これはソース管理プラグインによって解釈されます。 "このコマンドの詳細オプションはありますか?" という質問があります。 プラグインがを返した場合 `SCC_I_ADV_SUPPORT` 、IDE の [**取得**] ダイアログボックスに **[詳細設定**] ボタンが表示されます。

 ユーザーが初めて **[詳細設定** ] ボタンをクリックすると、IDE は再び関数を呼び出し `SccGetCommandOptions` ます。今回はポインターを指す以外のを使用し `NULL``ppvOptions` `NULL` ます。 プラグインには、独自の [ **オプションの取得** ] ダイアログボックスが表示され、ユーザーに情報の入力を求め、その情報を独自の構造に配置し、の構造体へのポインターを返し `ppvOptions` ます。

 同じダイアログボックスでユーザーが **[詳細** ] をもう一度クリックすると、IDE は `SccGetCommandOptions` 変更せずに関数を再度呼び出し、 `ppvOptions` 構造体がプラグインに戻されるようにします。 これにより、プラグインは、ダイアログボックスをユーザーが以前に設定した値に再初期化できるようになります。 プラグインは、を返す前に、その場所にある構造を変更します。

 最後に、ユーザーが IDE の [**取得**] ダイアログボックスで **[OK]** をクリックすると、Ide は [sccget](../extensibility/sccget-function.md)を呼び出し、詳細オプションを含むで返された構造体を渡し `ppvOptions` ます。

> [!NOTE]
> コマンドは、 `SCC_COMMAND_OPTIONS` IDE に [ **オプション** ] ダイアログボックスが表示され、ユーザーが統合の動作を制御するための設定を設定できるようにするときに使用されます。 ソース管理プラグインが独自の設定ダイアログボックスを提供する必要がある場合は、IDE の [基本設定] ダイアログボックスの **[詳細設定** ] ボタンから表示できます。 このプラグインは、この情報を取得して保持するだけの役割を担います。IDE では、このファイルを使用したり、変更したりすることはありません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [コマンドコード](../extensibility/command-code-enumerator.md)
