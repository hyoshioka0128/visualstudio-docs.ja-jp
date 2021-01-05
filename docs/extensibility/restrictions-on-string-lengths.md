---
title: 文字列の長さに関する制限 |Microsoft Docs
description: ソース管理プラグイン API によって適用されるさまざまな関数で使用される文字列の長さに関する制限について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, restrictions on string lengths
ms.assetid: 877173d2-ca27-43b3-b1f4-8379f7c5e268
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5412e930937d029f803f5c6c2b4ddc9d396d9485
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715523"
---
# <a name="restrictions-on-string-lengths"></a>文字列の長さに関する制限
ソース管理プラグイン API は、さまざまな関数で使用される文字列の長さを制限します。

## <a name="string-length-values"></a>文字列長の値

|定数|値|
|--------------|-----------|
|`SCC_NAME_LEN`|31|
|`SCC_AUXLABEL_LEN`|31|
|`SCC_USER_LEN`|31|
|`SCC_PRJPATH_LEN`|300|

> [!NOTE]
> 長さには、終了文字は含まれません `null` 。 "_LEN" ではなく "_SIZE" サフィックスを持つその他の定数には、終了のためのスペースが含ま `null` れます。

|定数|値|
|--------------|-----------|
|SCC_NAME_SIZE|32|
|SCC_AUXLABEL_SIZE|32|
|SCC_USER_SIZE|32|
|SCC_PRJPATH_SIZE|301|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
