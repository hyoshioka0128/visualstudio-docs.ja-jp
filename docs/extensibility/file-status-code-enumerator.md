---
title: ファイルステータスコード列挙子 |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 184c8686ea184aea2cbd0a64873718cbe72f7615
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711454"
---
# <a name="file-status-code-enumerator"></a>ファイル状態コード列挙子
列挙`SccStatus`子には、ソース管理システム内のファイルの状態を指定する名前付き定数値が含まれています。 この列挙体は[、SccQueryInfo](../extensibility/sccqueryinfo-function.md)と`POPLISTFUNC`コールバック関数 (詳細については[、POPLISTFUNC](../extensibility/poplistfunc.md)を参照してください) によって使用されます。

## <a name="syntax"></a>構文

```
enum SccStatus {
   SCC_STATUS_INVALID          = -1L,
   SCC_STATUS_NOTCONTROLLED    = 0x0000L,
   SCC_STATUS_CONTROLLED       = 0x0001L,
   SCC_STATUS_CHECKEDOUT       = 0x0002L,
   SCC_STATUS_OUTOTHER         = 0x0004L,
   SCC_STATUS_OUTEXCLUSIVE     = 0x0008L,
   SCC_STATUS_OUTMULTIPLE      = 0x0010L,
   SCC_STATUS_OUTOFDATE        = 0x0020L,
   SCC_STATUS_DELETED          = 0x0040L,
   SCC_STATUS_LOCKED           = 0x0080L,
   SCC_STATUS_MERGED           = 0x0100L,
   SCC_STATUS_SHARED           = 0x0200L,
   SCC_STATUS_PINNED           = 0x0400L,
   SCC_STATUS_MODIFIED         = 0x0800L,
   SCC_STATUS_OUTBYUSER        = 0x1000L
   SCC_STATUS_NOMERGE          = 0x2000L
   SCC_STATUS_RESERVED_1       = 0x4000L
   SCC_STATUS_RESERVED_2       = 0x8000L
};
```

## <a name="members"></a>メンバー
 SCC_STATUS_INVALID ステータスを取得できませんでした。それに頼らないでください。

 SCC_STATUS_NOTCONTROLLED ファイルがソース管理下にありません。

 SCC_STATUS_CONTROLLED ファイルはソース管理下にあります。

 SCC_STATUS_CHECKEDOUTローカル ディスク上の現在のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTOTHER ファイルが別のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTEXCLUSIVE ファイルは排他的にチェックアウトされています。

 SCC_STATUS_OUTMULTIPLE ファイルが複数のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTOFDATE ファイルが最新ではありません。

 SCC_STATUS_DELETEDファイルはプロジェクトから削除されました。

 SCC_STATUS_LOCKEDファイルはロックされています。これ以上のバージョンは許可されません。

 SCC_STATUS_MERGEDファイルはマージされましたが、まだ修正/検証されていません。

 SCC_STATUS_SHARED ファイルはプロジェクト間で共有されます。

 SCC_STATUS_PINNEDファイルは明示的なバージョンで共有されます。

 SCC_STATUS_MODIFIEDファイルが変更/破損/違反されました。

 SCC_STATUS_OUTBYUSER ファイルは現在のユーザーによってチェックアウトされています。

 SCC_STATUS_NOMERGEファイルはマージされず、GETの前に保存する必要はありません。

 SCC_STATUS_RESERVED_1 内部使用のために予約されています。

 SCC_STATUS_RESERVED_2 内部使用のために予約されています。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccQueryInfo](../extensibility/sccqueryinfo-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
