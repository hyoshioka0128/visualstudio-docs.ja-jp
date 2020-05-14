---
title: カスタムドキュメントを保存する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f04d588b4becfa778407269849032ea8ec56fb3f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705609"
---
# <a name="saving-a-custom-document"></a>カスタム ドキュメントの保存
環境では、[**保存]、[名前**を**付けて保存**]、[**すべて保存]** の各コマンドを処理します。 ユーザーが [**ファイル**] メニューの **[上書き保存**]、[**名前を付けて**保存] **、または [すべて保存]** をクリックするか、またはソリューションを閉じて [すべて保存] をクリックすると、次の処理が実行されます。

 ![カスタマーエディター保存](../../extensibility/internals/media/private.gif "Private")カスタム エディターの [保存]、[名前を付けて保存]、および [すべて保存] コマンド処理

 このプロセスの詳細は、次の手順で説明します。

1. **[保存]** コマンドと **[名前を付けて保存]** コマンドの場合、環境はサービスを<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>使用してアクティブなドキュメント ウィンドウを決定し、保存する必要がある項目を決定します。 アクティブなドキュメント ウィンドウが判明すると、環境は、実行中のドキュメント テーブルで、ドキュメントの階層ポインターとアイテム識別子 (itemID) を検索します。 詳細については、「[ドキュメント テーブルの実行](../../extensibility/internals/running-document-table.md)」を参照してください。

     [すべて保存] コマンドの場合、環境は、実行中のドキュメント テーブルの情報を使用して、保存するすべてのアイテムのリストをコンパイルします。

2. ソリューションは、呼び出<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>しを受け取ると、選択された項目のセット (つまり、<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>サービスによって公開される複数の選択項目) を反復処理します。

3. 選択した各項目で、ソリューションは階層ポインターを使用してメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A>呼び出し、[保存] メニュー コマンドを有効にするかどうかを判断します。 1 つまたは複数のアイテムがダーティである場合は、[保存] コマンドが有効になります。 階層が標準エディターを使用している場合、メソッドを呼び出すことによって、階層はダーティ ステータスの<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A>クエリをエディターに委任します。

4. 選択した各項目がダーティである場合、ソリューションは階層ポインターを使用して<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>、適切な階層でメソッドを呼び出します。

     カスタム エディターの場合、ドキュメント データ オブジェクトとプロジェクト間の通信はプライベートです。 したがって、これらの 2 つのオブジェクト間で、特別な永続性の問題が処理されます。

    > [!NOTE]
    > 独自の永続性を実装する場合は、時間を<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>節約するために、必ずメソッドを呼び出してください。 このメソッドは、ファイルを安全に保存する (たとえば、ファイルが読み取り専用でない) かどうかを確認します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)
