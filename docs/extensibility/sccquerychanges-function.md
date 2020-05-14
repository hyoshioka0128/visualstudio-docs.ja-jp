---
title: 関数の変更 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ec335d808c287decb75bf759d5a3795d98962579
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700498"
---
# <a name="sccquerychanges-function"></a>SccQueryChanges 関数
この関数は、特定のファイルのリストを列挙し、コールバック関数を通じて各ファイルの名前変更に関する情報を提供します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccQueryChanges(
   LPVOID           pContext,
   LONG             nFiles,
   LPCSTR*          lpFileNames,
   QUERYCHANGESFUNC pfnCallback,
   LPVOID           pvCallerData
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグイン のコンテキスト ポインター。

 nファイル

[in]配列内のファイル`lpFileNames`数。

 ファイル名

[in]情報を取得するファイル名の配列。

 コールバック

[in]リスト内の各ファイル名を呼び出すコールバック関数 (詳細については[、QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)を参照してください)。

 呼び出し元データ

[in]コールバック関数に変更されずに渡される値。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|クエリ プロセスが正常に完了しました。|
|SCC_E_PROJNOTOPEN|プロジェクトはソース管理で開かれていない。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。|
|SCC_E_NONSPECIFICERROR|未指定または一般的なエラーが発生しました。|

## <a name="remarks"></a>Remarks
 照会される変更は、名前空間に対するものです。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)
- [エラー コード](../extensibility/error-codes.md)
