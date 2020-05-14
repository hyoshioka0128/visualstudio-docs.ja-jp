---
title: 永続性と実行中のドキュメントテーブル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ba698f20b83d1a7af42aeca046aa2a8c943838ef
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706719"
---
# <a name="persistence-and-the-running-document-table"></a>ドキュメント テーブルの保存と実行
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE では、プロジェクトは、サービス<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>を使用して実行するプロジェクト項目の永続性を完全に管理する必要があります。 ドキュメントは、Visual Studio 環境での永続化の基本単位です。 プロジェクトは、開いているすべてのドキュメントの状態を追跡するリソースである、実行中のドキュメント テーブル (RDT) を使用してドキュメントの開く、保存、および名前の変更を調整します。

## <a name="managing-persistence"></a>永続性の管理
 プロジェクトは、インターフェイスを実装することで、環境の永続化<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem>サービスを制御します。 環境は、ドキュメント自体を永続化するように直接要求することはありませんが、所有しているプロジェクト (または階層) にドキュメントの保存を要求します。 これにより、プロジェクトはプロジェクト項目データをローカルファイル、リモートファイル、データベース、リポジトリ、またはその他のメディアに保存できます。

 グローバル環境は、RDT を維持します。 環境では、開いているすべてのウィンドウとドキュメントのエントリを RDT で保持し、ソリューションを閉じたときに、特別な通知を受け取ることができます。 さらに、RDT を使用すると、**ソリューション エクスプローラー**で対応するノードを追跡できます。 RDT は、プロジェクト ファイルとプロジェクト項目ドキュメントの両方を含む、開いている永続化可能なオブジェクトごとに 1 つのレコードを保持します。

## <a name="see-also"></a>関連項目
- [ドキュメント テーブルの実行](../../extensibility/internals/running-document-table.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
