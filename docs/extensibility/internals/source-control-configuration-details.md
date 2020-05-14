---
title: ソース管理の構成の詳細 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7cf4a5c55e8093e5dcd6406cde1c60f642188495
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705295"
---
# <a name="source-control-configuration-details"></a>ソース管理構成の詳細
ソース管理を実装するには、プロジェクト システムまたはエディターを適切に構成して、次の操作を行う必要があります。

- 変更された状態に移行するためのアクセス許可を要求する

- ファイルを保存する権限を要求する

- プロジェクト内のファイルの追加、削除、または名前変更を行うアクセス許可を要求する

## <a name="request-permission-to-transition-to-changed-state"></a>変更された状態に遷移するためのアクセス許可の要求
 プロジェクトまたはエディターは、 を呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>して変更された (ダーティ) 状態に遷移するアクセス許可を要求する必要があります。 実装する各エディターは<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>に戻る`True`前に、環境からドキュメントを変更するために、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A>呼び出しを行い、承認を受ける必要があります。 プロジェクトは基本的にプロジェクト ファイルのエディターであり、その結果、プロジェクト ファイルの変更状態の追跡を実装する場合と、テキスト エディターがそのファイルに対して行うのと同じ役割があります。 環境は、ソリューションの変更された状態を処理しますが、プロジェクト ファイルやその項目のように、ソリューションが参照するが格納されないオブジェクトの変更された状態を処理する必要があります。 一般に、プロジェクトまたはエディターが項目の永続性を管理する責任がある場合、変更状態の追跡を実装する必要があります。

 この呼び出`IVsQueryEditQuerySave2::QueryEditFiles`しに応答して、環境は次の操作を実行できます。

- 変更の呼び出しを拒否し、その場合、エディターまたはプロジェクトは変更されていない (クリーン) 状態のままである必要があります。

- ドキュメント データを再読み込みする必要があることを示します。 プロジェクトの場合、環境はプロジェクトのデータを再ロードします。 エディターは、その実装を通じてディスクから<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>データを再ロードする必要があります。 どちらの場合も、データが再読み込みされたときに、プロジェクトまたはエディターのコンテキストが変更される可能性があります。

  既存のコード ベースに適切な`IVsQueryEditQuerySave2::QueryEditFiles`呼び出しを再設定するのは複雑で困難な作業です。 そのため、これらの呼び出しは、プロジェクトまたはエディターの作成中に統合する必要があります。

## <a name="request-permission-to-save-a-file"></a>ファイルを保存するアクセス許可を要求する
 プロジェクトまたはエディターがファイルを保存する前に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>または<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>を呼び出す必要があります。 プロジェクト ファイルの場合、これらの呼び出しは、プロジェクト ファイルを保存するタイミングを知っているソリューションによって自動的に完了します。 エディターの実装がヘルパー関数`IVsPersistDocData2`<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>を使用しない限り、これらの呼び出しを行う必要があります。 エディターがこの方法で実装`IVsPersistDocData2`する場合は、呼び出し`IVsQueryEditQuerySave2::QuerySaveFile`が`IVsQueryEditQuerySave2::QuerySaveFiles`行われるか、またはあなたのために行われます。

> [!NOTE]
> これらの呼び出しは常にプリエンプティブに行います。

## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>プロジェクト内のファイルの追加、削除、または名前変更のアクセス許可を要求する
 プロジェクトがファイルまたはディレクトリを追加、名前変更、または削除するには、その前に適切な`IVsTrackProjectDocuments2::OnQuery*`メソッドを呼び出して環境にアクセス許可を要求する必要があります。 アクセス許可が付与されている場合、プロジェクトは操作を完了し、適切な`IVsTrackProjectDocuments2::OnAfter*`メソッドを呼び出して、操作が完了したことを環境に通知する必要があります。 プロジェクトは、親ファイルだけでなく、すべての<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>ファイル (たとえば、特殊ファイル) のインターフェイスのメソッドを呼び出す必要があります。 ファイル呼び出しは必須ですが、ディレクトリ呼び出しはオプションです。 プロジェクトにディレクトリ情報がある場合は、適切な<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>メソッドを呼び出す必要がありますが、この情報がない場合は、ディレクトリ情報が推測されます。

 プロジェクトは、プロジェクトの開いている時`IVsTrackProjectDocuments2`または閉じる時のメソッドを呼び出してはいけません。 起動時にこの情報を必要とするリスナーは、イベントを<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A>待機し、ソリューションを反復処理して必要な情報を見つけることができます。 シャットダウン時には、この情報は必要ありません。 `IVsTrackProjectDocuments2`は から提供<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>されます。

 追加、名前変更、および削除の各アクションには、`OnQuery*`メソッドと`OnAfter*`メソッドがあります。 このメソッド`OnQuery*`を呼び出して、ファイルまたはディレクトリの追加、名前変更、または削除を行うアクセス許可を要求します。 ファイルまたは`OnAfter*`ディレクトリが追加、名前変更、または削除された後にメソッドを呼び出し、プロジェクトの状態が新しい状態を反映します。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
