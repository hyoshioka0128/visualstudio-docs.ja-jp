---
title: 関数を実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6c7982d8c8c0d71f8c79e9b808be5453d384882d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701192"
---
# <a name="sccbeginbatch-function"></a>関数
この関数は、ソース管理操作のバッチ シーケンスを開始します。 バッチを終了するために[SccEndBatch](../extensibility/sccendbatch-function.md)が呼び出されます。 これらのバッチは入れ子にできません。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|操作のバッチが正常に開始されました。|
|SCC_E_UNKNOWNERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 ソース管理バッチは、複数のプロジェクトまたは複数のコンテキストで同じ操作を実行するために使用されます。 バッチを使用すると、バッチ操作中のユーザー エクスペリエンスからプロジェクトごとの冗長ダイアログ ボックスを削除できます。 関数`SccBeginBatch`と[SccEndBatch](../extensibility/sccendbatch-function.md)は、操作の開始と終了を示す関数ペアとして使用されます。 ネストすることはできません。 `SccBeginBatch`バッチ操作が進行中であることを示すフラグを設定します。

 バッチ操作が有効な間、ソース管理プラグインは、ユーザーに対して 1 つのダイアログ ボックスを表示し、そのダイアログ ボックスからの応答を後続のすべての操作に適用する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)
