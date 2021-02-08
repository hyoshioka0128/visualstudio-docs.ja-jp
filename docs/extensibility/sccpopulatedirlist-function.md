---
title: SccPopulateDirList 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: eac3973bf28a14340b720a51fc291b914822f3d1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99836918"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 関数
この関数は、確認するディレクトリのリストを指定して、ソース管理に格納するディレクトリと (必要に応じて) ファイルを決定します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccPopulateDirList(
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

からソース管理プラグインのコンテキストポインター。

 nDirs

から配列内のディレクトリパスの数 `lpDirPaths` 。

 lpDirPaths

から確認するディレクトリパスの配列。

 pfnPopulate

からディレクトリパスと (必要に応じて) のファイル名を呼び出すためのコールバック関数 `lpDirPaths` (詳細については、「 [Popdirlistfunc](../extensibility/popdirlistfunc.md) 」を参照してください)。

 pvCallerData

から変更せずにコールバック関数に渡される値。

 限ら

からディレクトリの処理方法を制御する値の組み合わせ (有効な値については、 [特定のコマンドで使用される Bitflags](../extensibility/bitflags-used-by-specific-commands.md) の "PopulateDirList flags" セクションを参照してください)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|操作は正常に完了しました。|
|SCC_E_UNKNOWNERROR|エラーが発生しました。|

## <a name="remarks"></a>解説
 コールバック関数に渡されるのは、ソース管理リポジトリ内のディレクトリと (必要に応じて) ファイル名だけです。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [エラー コード](../extensibility/error-codes.md)
