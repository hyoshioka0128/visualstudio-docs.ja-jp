---
description: この関数は、ソース管理操作のバッチシーケンスを開始します。
title: SccBeginBatch 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b52b82919b10e58772343aee42cb8723b10d6ca3
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221653"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 関数
この関数は、ソース管理操作のバッチシーケンスを開始します。 バッチを終了するために [Sccendbatch](../extensibility/sccendbatch-function.md) が呼び出されます。 これらのバッチを入れ子にすることはできません。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|操作のバッチが正常に開始しました。|
|SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 ソース管理バッチは、複数のプロジェクトまたは複数のコンテキストで同じ操作を実行するために使用されます。 バッチ処理を使用すると、バッチ操作中のユーザーエクスペリエンスから、プロジェクトごとの冗長なダイアログボックスを削除できます。 `SccBeginBatch`関数と[Sccendbatch](../extensibility/sccendbatch-function.md)は、操作の開始と終了を示すために関数のペアとして使用されます。 入れ子にすることはできません。 `SccBeginBatch` バッチ操作が進行中であることを示すフラグを設定します。

 バッチ操作が有効になっている間、ソース管理プラグインは、すべての質問に対して1つのダイアログボックスを表示し、後続のすべての操作にそのダイアログボックスから応答を適用する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)
