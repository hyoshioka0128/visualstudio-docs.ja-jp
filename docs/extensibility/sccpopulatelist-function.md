---
description: この関数は、特定のソース管理コマンドのファイルの一覧を更新し、指定されたすべてのファイルに対してソース管理の状態を提供します。
title: SccPopulateList 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateList
helpviewer_keywords:
- SccPopulateList function
ms.assetid: 7416e781-c571-4a7f-8af3-a089ce8be662
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 24ed033d05711e4c6815945796595897e926ba74
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220548"
---
# <a name="sccpopulatelist-function"></a>SccPopulateList 関数
この関数は、特定のソース管理コマンドのファイルの一覧を更新し、指定されたすべてのファイルに対してソース管理の状態を提供します。

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
 pvContext

からソース管理プラグインのコンテキスト構造。

 N コマンド

から配列内のすべてのファイルに適用されるソース管理コマンド `lpFileNames` (使用可能なコマンドの一覧については、 [コマンドコード](../extensibility/command-code-enumerator.md) を参照してください)。

 nFiles

から配列内のファイルの数 `lpFileNames` 。

 lpFileNames 名

からIDE で認識されているファイル名の配列。

 pfnPopulate

からファイルの追加と削除を行うために呼び出す IDE コールバック関数 (詳細については、 [POPLISTFUNC](../extensibility/poplistfunc.md) を参照してください)。

 pvCallerData

から変更せずにコールバック関数に渡される値。

 lpStatus

[入力、出力]各ファイルの状態フラグを返すソース管理プラグインの配列。

 限ら

からコマンドフラグ (詳細については、特定の [コマンドで使用される Bitflags](../extensibility/bitflags-used-by-specific-commands.md) の "PopulateList フラグ" セクションを参照してください)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|正常終了しました。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 この関数は、現在の状態についてファイルの一覧を調べます。 また、コールバック関数を使用して `pfnPopulate` 、ファイルがの条件に一致しない場合に呼び出し元に通知し `nCommand` ます。 たとえば、コマンドがで、 `SCC_COMMAND_CHECKIN` リスト内のファイルがチェックアウトされていない場合は、コールバックを使用して呼び出し元に通知します。 場合によっては、ソース管理プラグインがコマンドの一部として他のファイルを検出して追加することがあります。 これにより、たとえば Visual Basic ユーザーは自分のプロジェクトで使用されている .bmp ファイルをチェックアウトできますが、Visual Basic プロジェクトファイルには表示されません。 ユーザーが IDE で **Get** コマンドを選択します。 IDE には、ユーザーが取得できると思われるすべてのファイルの一覧が表示されますが、リストが表示される前に、 `SccPopulateList` 表示されるリストが最新の状態であることを確認するために関数が呼び出されます。

## <a name="example"></a>例
 IDE によって、ユーザーが取得できると思われるファイルの一覧が作成されます。 このリストを表示する前に、関数を呼び出して、 `SccPopulateList` ソース管理プラグインがリストからファイルを追加および削除できるようにします。 プラグインは、指定されたコールバック関数を呼び出すことによってリストを変更します (詳細については、 [POPLISTFUNC](../extensibility/poplistfunc.md) を参照してください)。

 プラグインは、処理 `pfnPopulate` が完了するまでファイルを追加および削除する関数の呼び出しを続け、関数から制御を戻し `SccPopulateList` ます。 IDE でそのリストを表示できます。 配列は、 `lpStatus` IDE によって渡された元のリスト内のすべてのファイルを表します。 このプラグインは、コールバック関数を使用するだけでなく、これらすべてのファイルの状態を格納します。

> [!NOTE]
> ソース管理プラグインには、常にこの関数からすぐに制御を戻すオプションがあり、そのままにしておきます。 プラグインがこの関数を実装する場合、 `SCC_CAP_POPULATELIST` [Sccinitialize](../extensibility/sccinitialize-function.md)の最初の呼び出しで機能ビットフラグを設定することによって、この関数を示すことができます。 既定では、プラグインは、渡されるすべての項目がファイルであると常に想定する必要があります。 ただし、IDE でパラメーターにフラグを設定した場合は、 `SCC_PL_DIR` `fOptions` 渡されるすべての項目がディレクトリと見なされます。 プラグインは、ディレクトリに属するすべてのファイルを追加する必要があります。 IDE では、ファイルとディレクトリが混在することはありません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
- [コマンド コード](../extensibility/command-code-enumerator.md)
