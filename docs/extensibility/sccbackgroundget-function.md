---
title: SccBackgroundGet 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6d081389124b8703958f82cb97fc877f9f812290
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952123"
---
# <a name="sccbackgroundget-function"></a>SccBackgroundGet 関数
この関数は、指定された各ファイルを、ユーザー操作なしでソース管理から取得します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccBackgroundGet(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LONG    dwFlags,
   LONG    dwBackgroundOperationID
);
```

### <a name="parameters"></a>パラメーター
 pContext

からソース管理プラグインのコンテキストポインター。

 nFiles

から配列に指定されたファイルの数 `lpFileNames` 。

 lpFileNames 名

[入力、出力]取得するファイルの名前の配列。

> [!NOTE]
> 名前は、完全修飾されたローカルファイル名である必要があります。

 dwFlags

からコマンドフラグ ( `SCC_GET_ALL` 、 `SCC_GET_RECURSIVE` )。

 dwBackgroundOperationID

からこの操作に関連付けられている一意の値。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|操作は正常に完了しました。|
|SCC_E_BACKGROUNDGETINPROGRESS|バックグラウンドでの取得が既に進行中である (ソース管理プラグインは、同時バッチ操作をサポートしていない場合にのみ、これを返す必要があります)。|
|SCC_I_OPERATIONCANCELED|操作が完了する前に取り消されました。|

## <a name="remarks"></a>解説
 この関数は、ソース管理プラグインが読み込まれたスレッドとは異なるスレッド上で常に呼び出されます。 この関数は、完了するまでを返すことは想定されていません。ただし、ファイルの複数のリストを使用して複数回呼び出すことができます。

 引数の使用 `dwFlags` は [Sccget](../extensibility/sccget-function.md)と同じです。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGet](../extensibility/sccget-function.md)
