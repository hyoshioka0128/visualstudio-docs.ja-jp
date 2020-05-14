---
title: 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 91b3debf0e686ceece3048cf3d92b629e3359edd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700819"
---
# <a name="sccgetevents-function"></a>関数
この関数は、キューに入っている状態イベントを取得します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetEvents (
   LPVOID pvContext,
   LPSTR  lpFileName,
   LPLONG lpStatus,
   LPLONG pnEventsRemaining
);
```

### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 ファイル名

[イン、アウト]ソース管理プラグインが返されたファイル名 (最大_MAX_PATH文字) を格納するバッファー。

 lp2

[イン、アウト]ステータスコードを返します(可能な値については[ファイルステータスコード](../extensibility/file-status-code-enumerator.md)を参照)。

 残り

[イン、アウト]この呼び出しの後にキューに残されたエントリの数を返します。 この数値が大きい場合、呼び出し元は[SccQueryInfo](../extensibility/sccqueryinfo-function.md)を呼び出して、すべての情報を一度に取得することを決定できます。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|取得イベントが成功しました。|
|SCC_E_OPNOTSUPPORTED|この関数はサポートされません。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 この関数は、ソース管理下のファイルのステータス更新が行われていないかどうかを確認するために、アイドル処理中に呼び出されます。 ソース管理プラグインは、認識しているすべてのファイルのステータスを保持し、プラグインによってステータスの変更が示されるたびに、ステータスと関連ファイルがキューに格納されます。 呼`SccGetEvents`び出されると、キューの最上位の要素が取得されて返されます。 この関数は、以前にキャッシュされた情報のみを返すように制約されており、非常に迅速なターンアラウンド(つまり、ディスクの読み取りやソース管理システムの状態の問い合わせください)を持っている必要があります。そうしないと、IDE のパフォーマンスが低下し始める可能性があります。

 レポートするステータスの更新がない場合、ソース管理プラグインは、 が`lpFileName`指すバッファに空の文字列を格納します。 それ以外の場合、プラグインはステータス情報が変更されたファイルのフルパス名を格納し、適切なステータスコード ([ファイルステータスコード](../extensibility/file-status-code-enumerator.md)で詳述されている値の 1 つ) を返します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [ファイルステータスコード](../extensibility/file-status-code-enumerator.md)
