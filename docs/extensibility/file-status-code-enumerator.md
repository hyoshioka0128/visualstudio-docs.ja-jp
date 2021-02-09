---
title: ファイル状態コード列挙子 |Microsoft Docs
description: SccStatus 列挙子には、ソース管理システム内のファイルの状態を示す定数値が含まれ、SccQueryInfo および POPLISTFUNC によって使用されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- named constants, SccStatus enumerator
- source control plug-ins, file status enumeration
- SccStatus enumerator
- file status code enumerator
ms.assetid: 5c37876b-c83c-4ca1-837b-57cd465a879a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 981e4e4561db7bc7fb8a9f0ce92522d34e4b34fa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99874049"
---
# <a name="file-status-code-enumerator"></a>ファイル状態コード列挙子
列挙子には、 `SccStatus` ソース管理システム内のファイルの状態を指定する名前付き定数値が含まれます。 この列挙体は、 [Sccqueryinfo](../extensibility/sccqueryinfo-function.md) およびコールバック関数によって使用され `POPLISTFUNC` ます (詳細については、 [POPLISTFUNC](../extensibility/poplistfunc.md) を参照してください)。

## <a name="syntax"></a>構文

```
enum SccStatus {
   SCC_STATUS_INVALID          = -1L,
   SCC_STATUS_NOTCONTROLLED    = 0x0000L,
   SCC_STATUS_CONTROLLED       = 0x0001L,
   SCC_STATUS_CHECKEDOUT       = 0x0002L,
   SCC_STATUS_OUTOTHER         = 0x0004L,
   SCC_STATUS_OUTEXCLUSIVE     = 0x0008L,
   SCC_STATUS_OUTMULTIPLE      = 0x0010L,
   SCC_STATUS_OUTOFDATE        = 0x0020L,
   SCC_STATUS_DELETED          = 0x0040L,
   SCC_STATUS_LOCKED           = 0x0080L,
   SCC_STATUS_MERGED           = 0x0100L,
   SCC_STATUS_SHARED           = 0x0200L,
   SCC_STATUS_PINNED           = 0x0400L,
   SCC_STATUS_MODIFIED         = 0x0800L,
   SCC_STATUS_OUTBYUSER        = 0x1000L
   SCC_STATUS_NOMERGE          = 0x2000L
   SCC_STATUS_RESERVED_1       = 0x4000L
   SCC_STATUS_RESERVED_2       = 0x8000L
};
```

## <a name="members"></a>メンバー
 SCC_STATUS_INVALID の状態を取得できませんでした。それに依存しないでください。

 SCC_STATUS_NOTCONTROLLED ファイルがソース管理下にありません。

 SCC_STATUS_CONTROLLED ファイルがソース管理下にあります。

 SCC_STATUS_CHECKEDOUT ローカルディスクの現在のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTOTHER ファイルが別のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTEXCLUSIVE ファイルは排他的にチェックアウトされています。

 SCC_STATUS_OUTMULTIPLE ファイルが複数のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTOFDATE ファイルが最新ではありません。

 SCC_STATUS_DELETED ファイルがプロジェクトから削除されました。

 SCC_STATUS_LOCKED ファイルがロックされています。これ以上のバージョンは使用できません。

 SCC_STATUS_MERGED ファイルはマージされましたが、まだ修正または検証されていません。

 SCC_STATUS_SHARED ファイルは、プロジェクト間で共有されます。

 SCC_STATUS_PINNED ファイルは、明示的なバージョンに共有されます。

 SCC_STATUS_MODIFIED ファイルが変更されたか、壊れているか、違反になっています。

 SCC_STATUS_OUTBYUSER ファイルが現在のユーザーによってチェックアウトされています。

 SCC_STATUS_NOMERGE ファイルをにマージすることはできません。また、GET の前に保存する必要もありません。

 SCC_STATUS_RESERVED_1 内部使用のために予約されています。

 SCC_STATUS_RESERVED_2 内部使用のために予約されています。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccQueryInfo](../extensibility/sccqueryinfo-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
