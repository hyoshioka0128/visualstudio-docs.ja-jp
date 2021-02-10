---
title: ディレクトリ状態コード列挙子 |Microsoft Docs
description: SccDirStatus 列挙子には、ソース管理システムのディレクトリの状態を指定し、SccDirQueryInfo によって使用される名前付き定数値が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c6d5eb64cf4883c2e977b41e77fc2243aca2ee34
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968256"
---
# <a name="directory-status-code-enumerator"></a>ディレクトリステータスコード列挙子
列挙子には、 `SccDirStatus` ソース管理システム内のディレクトリの状態を指定する名前付き定数値が含まれます。 この列挙体は、 [Sccdirqueryinfo](../extensibility/sccdirqueryinfo-function.md)によって使用されます。 これは、ソース管理プラグイン API のバージョン1.2 で導入されました。

## <a name="syntax"></a>構文

```
enum SccDirStatus {
   SCC_DIRSTATUS_INVALID       = -1L,
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L
};
```

## <a name="members"></a>メンバー
 SCC_DIRSTATUS_INVALID の状態を取得できませんでした。それに依存しないでください。

 SCC_DIRSTATUS_NOTCONTROLLED ディレクトリがソース管理下にありません。

 SCC_DIRSTATUS_CONTROLLED Directory がソース管理下にあります。

 このディレクトリに対応する SCC_DIRSTATUS_EMPTYPROJ プロジェクトは空です。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
