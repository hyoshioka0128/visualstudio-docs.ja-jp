---
title: 関数を取得する Sccbackground |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b1c07076b6e257bd5519d19f841797fbc652f0c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701231"
---
# <a name="sccbackgroundget-function"></a>関数を取得します。
この関数は、指定された各ファイルをソース管理から取得します。

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

[in]ソース管理プラグイン のコンテキスト ポインター。

 nファイル

[in]配列に指定されたファイルの`lpFileNames`数。

 ファイル名

[イン、アウト]取得するファイルの名前の配列。

> [!NOTE]
> 名前は、ローカルファイル名を完全修飾する必要があります。

 dwFlags

[in]コマンド フラグ`SCC_GET_ALL` `SCC_GET_RECURSIVE`( , )

 を実行します。

[in]この操作に関連付けられている一意の値。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|操作は正常に完了しました。|
|SCC_E_BACKGROUNDGETINPROGRESS|バックグラウンド検索は既に進行中です (ソース管理プラグインは、同時バッチ操作をサポートしていない場合にのみ、これを返す必要があります)。|
|SCC_I_OPERATIONCANCELED|操作は完了する前にキャンセルされました。|

## <a name="remarks"></a>Remarks
 この関数は、ソース管理プラグインを読み込んだスレッドとは異なるスレッドで常に呼び出されます。 この関数は、実行されるまで戻りません。ただし、複数のファイルリストを同時に複数回呼び出すことができます。

 引数の`dwFlags`使用は[、 SccGet](../extensibility/sccget-function.md)と同じです。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGet](../extensibility/sccget-function.md)
