---
title: SccUn初期化関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c4706ddf28949af4fe1bba01c32b2c64c9156d51
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700227"
---
# <a name="sccuninitialize-function"></a>SccUninitialize 関数
この関数は、ソース管理プラグインをシャットダウンする準備として[、SccInitialize](../extensibility/sccinitialize-function.md)の以前の呼び出しによって作成された割り当てまたは開いている接続をクリーンアップします。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>パラメーター
 を行う

[in][SccInitialize](../extensibility/sccinitialize-function.md)で作成されたソース管理プラグイン コンテキスト構造体へのポインター。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|クリーンアップが正常に完了しました。|

## <a name="remarks"></a>Remarks
 ソース管理プラグインは、シャットダウンの準備と、プラグインがコンテキスト構造に割り当てたメモリを解放する役割を担います。 この関数は、プラグインのインスタンスごとに 1 回呼び出されます。 この呼び出しの前に[、SccInitialize](../extensibility/sccinitialize-function.md)の呼び出しが行ないます。 の呼び出し時に開くプロジェクトは存在`SccUninitialize`しません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
