---
title: 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDirQueryInfo
helpviewer_keywords:
- SccDirQueryInfo function
ms.assetid: 459e2d99-573d-47c4-b834-6d82c5e14162
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 222b5d15a1e2bcd9bd3f27a5cd0e9904642d9786
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700948"
---
# <a name="sccdirqueryinfo-function"></a>関数
この関数は、現在の状態に関する完全修飾ディレクトリのリストを調べます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccDirQueryInfo(
LPVOID  pContext,
LONG    nDirs,
LPCSTR* lpDirNames,
LPLONG  lpStatus
);
```

### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグインのコンテキスト構造。

 nディルス

[in]照会対象として選択されたディレクトリの数。

 名前

[in]照会するディレクトリの完全修飾パスの配列。

 lp2

[イン、アウト]ステータス フラグを返すソース管理プラグインの配列構造 (詳細については[、ディレクトリステータスコード](../extensibility/directory-status-code-enumerator.md)を参照)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|クエリは正常に実行されました。|
|SCC_E_OPNOTSUPPORTED|ソース コード管理システムでは、この操作はサポートされていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 この関数は、ファミリの`SCC_DIRSTATUS`ビットマスク ([ディレクトリステータスコード](../extensibility/directory-status-code-enumerator.md)を参照)で戻り配列を埋め、指定されたディレクトリごとに 1 つのエントリを指定します。 ステータス配列は、呼び出し元によって割り当てられます。

 IDE は、ディレクトリの名前を変更する前にこの関数を使用して、対応するプロジェクトがあるかどうかを照会して、ディレクトリがソース管理下にあるかどうかを確認します。 ディレクトリがソース管理下にない場合、IDE はユーザーに適切な警告を表示できます。

> [!NOTE]
> ソース管理プラグインが 1 つ以上の状態値を実装しない場合は、実装されていないビットを 0 に設定する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [ディレクトリステータスコード](../extensibility/directory-status-code-enumerator.md)
