---
title: 関数を指定する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ac1c51ac694acadd2efb0cd7d1c5a3f1d66ebc1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700556"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 関数
この関数は、検査するディレクトリのリストを指定して、ソース管理に格納されるディレクトリと (オプションで) ファイルを決定します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccPopulateDirList(
   LPVOID        pContext,
   LONG          nDirs,
   LPCSTR*       lpDirPaths,
   POPDIRLISTFUNCpfnPopulate,
   LPVOID        pvCallerData,
   LONG          fOptions
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグイン のコンテキスト ポインター。

 nディルス

[in]配列内のディレクトリ パス`lpDirPaths`の数。

 パス

[in]検査するディレクトリ パスの配列。

 を設定する

[in]各ディレクトリ パスを呼び出すコールバック関数と (オプション`lpDirPaths`で) ファイル名 (詳細については[、POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)を参照してください)。

 呼び出し元データ

[in]コールバック関数に変更されずに渡される値。

 f オプション

[in]ディレクトリの処理方法を制御する値の組み合わせ (可能な値については、特定の[コマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)の「PopulateDirList フラグ」セクションを参照してください)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|操作は正常に完了しました。|
|SCC_E_UNKNOWNERROR|エラーが発生しました。|

## <a name="remarks"></a>Remarks
 実際にソース管理リポジトリにあるディレクトリと (オプションで) ファイル名だけが、コールバック関数に渡されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [エラー コード](../extensibility/error-codes.md)
