---
title: SccEnd バッチ関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccEndBatch
helpviewer_keywords:
- SccEndBatch function
ms.assetid: 100e7833-fe0a-45c0-9fca-3e61fd1165b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 51fe7e0bc0d417ffa182fbc68fd2779ed0b625d9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700920"
---
# <a name="sccendbatch-function"></a>関数
この関数は、ソース管理操作のバッチを終了します。 これらのバッチは入れ子にできません。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccEndBatch(void);
```

## <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|操作のバッチが正常に終了しました。|
|SCC_E_UNKNOWNERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 ソース管理バッチは、複数のプロジェクトまたは複数のコンテキストで同じソース管理操作を実行するために使用されます。 バッチ処理を使用すると、バッチ操作中のユーザー エクスペリエンスから冗長なダイアログ ボックスを削除できます。 [SccBeginBatch](../extensibility/sccbeginbatch-function.md)と`SccEndBatch`関数は、操作の開始と終了を示すペアとして使用されます。 ネストすることはできません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccBeginBatch](../extensibility/sccbeginbatch-function.md)
