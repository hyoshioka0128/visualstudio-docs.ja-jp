---
title: 関数を一覧表示する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateList
helpviewer_keywords:
- SccPopulateList function
ms.assetid: 7416e781-c571-4a7f-8af3-a089ce8be662
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f518413adba1546bcff4f7cf2e62b4563cf1bcc7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700532"
---
# <a name="sccpopulatelist-function"></a>SccPopulateList 関数
この関数は、特定のソース管理コマンドのファイルの一覧を更新し、指定されたすべてのファイルのソース管理ステータスを提供します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccPopulateList (
   LPVOID          pvContext,
   enum SCCCOMMAND nCommand,
   LONG            nFiles,
   LPCSTR*         lpFileNames,
   POPLISTFUNC     pfnPopulate,
   LPVOID          pvCallerData,
   LPLONG          lpStatus,
   LONG            fOptions
);
```

#### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 nコマンド

[in]`lpFileNames`配列内のすべてのファイルに適用されるソース管理コマンド (使用可能なコマンドの一覧については[、「コマンド コード](../extensibility/command-code-enumerator.md)」を参照してください)。

 nファイル

[in]配列内のファイル数`lpFileNames`。

 ファイル名

[in]IDE で認識されているファイル名の配列。

 を設定する

[in]ファイルを追加および削除するために呼び出す IDE コールバック関数 (詳細については[、POPLISTFUNC](../extensibility/poplistfunc.md)を参照してください)。

 呼び出し元データ

[in]コールバック関数に変更されずに渡される値。

 lp2

[イン、アウト]ソース管理プラグインが各ファイルのステータス フラグを返す配列。

 f オプション

[in]コマンド フラグ (詳細については、[特定のコマンドで使用されるビット フラグ](../extensibility/bitflags-used-by-specific-commands.md)の「PopulateList フラグ」セクションを参照してください)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|正常終了しました。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 この関数は、ファイルのリストの現在のステータスを調べます。 このメソッドは`pfnPopulate`、コールバック関数を使用して、ファイルが の条件に一致しない`nCommand`場合に呼び出し元に通知します。 たとえば、コマンドが`SCC_COMMAND_CHECKIN`チェックアウトされ、リスト内のファイルがチェックアウトされていない場合、コールバックを使用して呼び出し元に通知します。 ソース管理プラグインは、コマンドの一部である可能性がある他のファイルを見つけて追加することがあります。 これにより、たとえば、Visual Basic ユーザーは、プロジェクトで使用されているが、Visual Basic プロジェクト ファイルには表示されない .bmp ファイルをチェックアウトできます。 ユーザーが IDE で **[取得**] コマンドを選択します。 IDE には、ユーザーが取得できると思われるすべてのファイルの一覧が表示されますが、リストが表示される前に`SccPopulateList`、表示するリストが最新であることを確認する関数が呼び出されます。

## <a name="example"></a>例
 IDE は、ユーザーが取得できると思うファイルのリストを作成します。 このリストを表示する前に、この`SccPopulateList`関数を呼び出して、ソース管理プラグインにリストからファイルを追加したり、リストからファイルを削除したりできます。 プラグインは、指定されたコールバック関数を呼び出すことによってリストを変更します (詳細については[、POPLISTFUNC](../extensibility/poplistfunc.md)を参照してください)。

 プラグインは、処理が完了するまで、`pfnPopulate`ファイルを追加および削除する関数を`SccPopulateList`呼び出し続け、その後関数から戻ります。 IDE はそのリストを表示できます。 配列`lpStatus`は、IDE によって渡された元のリスト内のすべてのファイルを表します。 プラグインは、コールバック関数を使用するだけでなく、これらすべてのファイルのステータスを入力します。

> [!NOTE]
> ソース管理プラグインには、この関数からすぐに戻るオプションが常にあり、リストはそのままにします。 プラグインがこの関数を実装する場合`SCC_CAP_POPULATELIST`[、SccInitialize](../extensibility/sccinitialize-function.md)への最初の呼び出しで機能ビットフラグを設定することで、これを示すことができます。 既定では、プラグインは常に渡されるすべての項目がファイルであると想定する必要があります。 ただし、IDE がパラメータに`SCC_PL_DIR`フラグを`fOptions`設定した場合、渡されるすべての項目はディレクトリと見なされます。 プラグインは、ディレクトリに属するすべてのファイルを追加する必要があります。 IDE は、ファイルとディレクトリの混在を渡すことはありません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
- [コマンド コード](../extensibility/command-code-enumerator.md)
