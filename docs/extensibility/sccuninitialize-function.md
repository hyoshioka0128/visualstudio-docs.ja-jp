---
description: この関数は、ソース管理プラグインをシャットダウンする準備として、SccInitialize の前回の呼び出しで作成された割り当てまたは開いている接続をクリーンアップします。
title: SccUninitialize 解除関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 187451aba5151c95d8947bd4f5a1419894cc65e7
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221328"
---
# <a name="sccuninitialize-function"></a>SccUninitialize 関数
この関数は、ソース管理プラグインをシャットダウンする準備として、 [Sccinitialize](../extensibility/sccinitialize-function.md) の前回の呼び出しで作成された割り当てまたは開いている接続をクリーンアップします。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

から [Sccinitialize](../extensibility/sccinitialize-function.md)で作成されたソース管理プラグインコンテキスト構造へのポインター。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|クリーンアップが正常に完了しました。|

## <a name="remarks"></a>解説
 ソース管理プラグインは、シャットダウンの準備を行い、プラグインによってコンテキスト構造に割り当てられたメモリを解放します。 関数は、プラグインの特定のインスタンスごとに1回呼び出されます。 [Sccinitialize](../extensibility/sccinitialize-function.md)の呼び出しは、この呼び出しの前になります。 を呼び出した時点でまだ開いているプロジェクトはありません `SccUninitialize` 。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
