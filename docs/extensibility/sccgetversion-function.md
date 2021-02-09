---
title: SccGetVersion 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 91daeca1df76f6b624d0eddf9d28222369b2cc4a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844542"
---
# <a name="sccgetversion-function"></a>SccGetVersion 関数
この関数は、ソース管理プラグインによってサポートされているソース管理プラグイン API のバージョン番号を取得します。

## <a name="syntax"></a>構文

```cpp
LONG SccGetVersion(void);
```

#### <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 `LONG`サポートされているソース管理プラグイン API のバージョン番号を含むデータ型。

|WORD|Description|
|----------|-----------------|
|HIWORD|メジャー バージョン|
|LOWORD|マイナー バージョン|

## <a name="remarks"></a>解説
 たとえば、ソース管理プラグインがソース管理プラグイン API のバージョン1.3 をサポートしている場合、この関数は0x0103 を返します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
