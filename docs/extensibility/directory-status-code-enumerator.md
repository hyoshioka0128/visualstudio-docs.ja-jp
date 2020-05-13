---
title: ディレクトリ ステータス コード列挙子 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b5ebf61f2baa6e4277e27cd3c4d18a51e64f835
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712158"
---
# <a name="directory-status-code-enumerator"></a>ディレクトリ状態コード列挙子
列挙`SccDirStatus`子には、ソース管理システムのディレクトリの状態を指定する名前付き定数値が含まれています。 この列挙体は[、SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)によって使用されます。 これは、ソース管理プラグイン API のバージョン 1.2 で導入されました。

## <a name="syntax"></a>構文

```
enum SccDirStatus {
   SCC_DIRSTATUS_INVALID       = -1L,
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L
};
```

## <a name="members"></a>メンバー
 SCC_DIRSTATUS_INVALID ステータスを取得できませんでした。それに頼らないでください。

 SCC_DIRSTATUS_NOTCONTROLLED ディレクトリがソース管理下にありません。

 SCC_DIRSTATUS_CONTROLLEDディレクトリはソース管理下にあります。

 SCC_DIRSTATUS_EMPTYPROJこのディレクトリに対応するプロジェクトは空です。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
