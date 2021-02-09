---
title: ソース管理の構成の詳細 |Microsoft Docs
description: Visual Studio でプロジェクトの種類のソース管理を実装する方法について説明します。これには、アクセス許可を要求するようにプロジェクトシステムまたはエディターを構成する作業が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b9a3a2f33fcbb94d1e863daf69b8561f7bad4f2a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99846505"
---
# <a name="source-control-configuration-details"></a>ソース管理構成の詳細
ソース管理を実装するには、次の操作を行うためにプロジェクトシステムまたはエディターを適切に構成する必要があります。

- 変更された状態に移行するためのアクセス許可を要求する

- ファイルを保存するためのアクセス許可を要求する

- プロジェクト内のファイルを追加、削除、または名前変更するためのアクセス許可を要求する

## <a name="request-permission-to-transition-to-changed-state"></a>変更された状態に移行するためのアクセス許可を要求する
 プロジェクトまたはエディターは、を呼び出すことによって変更された (ダーティ) 状態に遷移するためのアクセス許可を要求する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> ます。 を返す前に、を実装する各エディター <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> は、を呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> て、環境からドキュメントを変更する承認を受け取る必要があり `True` <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> ます。 プロジェクトは基本的にはプロジェクトファイルのエディターであり、そのため、ファイルのテキストエディターと同じように、プロジェクトファイルに対して変更された状態の追跡を実装する責任があります。 環境は、変更されたソリューションの状態を処理しますが、プロジェクトファイルやその項目など、ソリューションが参照しているオブジェクトの変更された状態を処理する必要があります。 一般に、プロジェクトまたはエディターが項目の永続化を管理する必要がある場合は、変更された状態の追跡を実装する必要があります。

 呼び出しへの応答として、 `IVsQueryEditQuerySave2::QueryEditFiles` 環境は次のことを実行できます。

- 変更への呼び出しを拒否します。その場合、エディターまたはプロジェクトは変更なし (クリーン) 状態のままにしておく必要があります。

- ドキュメントデータを再度読み込む必要があることを示します。 プロジェクトの場合、環境によってプロジェクトのデータが再読み込みされます。 エディターは、その実装を通じてディスクからデータを再読み込みする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> ます。 どちらの場合も、データが再読み込みされると、プロジェクトまたはエディターのコンテキストが変更される可能性があります。

  これは、既存のコードベースに対する適切な呼び出しをカルチャだけする複雑で困難なタスクです `IVsQueryEditQuerySave2::QueryEditFiles` 。 そのため、これらの呼び出しは、プロジェクトまたはエディターの作成中に統合する必要があります。

## <a name="request-permission-to-save-a-file"></a>ファイルを保存するためのアクセス許可を要求する
 プロジェクトまたはエディターがファイルを保存する前に、またはを呼び出す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> ます。 プロジェクトファイルの場合、これらの呼び出しは、プロジェクトファイルを保存するタイミングを認識するソリューションによって自動的に完了します。 のエディター実装でヘルパー関数が使用されていない限り、エディターはこれらの呼び出しを行い `IVsPersistDocData2` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> ます。 エディターがこのようにを実装している場合 `IVsPersistDocData2` `IVsQueryEditQuerySave2::QuerySaveFile` は、または `IVsQueryEditQuerySave2::QuerySaveFiles` の呼び出しが行われます。

> [!NOTE]
> 常にこれらの呼び出しを事前ににします。つまり、エディターがキャンセルを受け取ることができるようになります。

## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>プロジェクト内のファイルを追加、削除、または名前変更するためのアクセス許可を要求する
 プロジェクトがファイルまたはディレクトリを追加、名前変更、または削除できるようにするには、 `IVsTrackProjectDocuments2::OnQuery*` 環境からアクセス許可を要求する適切なメソッドを呼び出す必要があります。 アクセス許可が付与されている場合は、プロジェクトが操作を完了し、適切なメソッドを呼び出して、 `IVsTrackProjectDocuments2::OnAfter*` 操作が完了したことを環境に通知する必要があります。 プロジェクトは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 親ファイルだけでなく、すべてのファイル (たとえば、特殊ファイル) に対してインターフェイスのメソッドを呼び出す必要があります。 ファイル呼び出しは必須ですが、ディレクトリ呼び出しは省略可能です。 プロジェクトにディレクトリ情報が含まれている場合は、適切なメソッドを呼び出す必要 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> がありますが、この情報がない場合は、環境によってディレクトリ情報が推測されます。

 プロジェクトは、 `IVsTrackProjectDocuments2` project open または close でのメソッドを呼び出すことはできません。 起動時にこの情報を必要とするリスナーは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> イベントを待機し、ソリューションを反復処理して必要な情報を見つけることができます。 シャットダウン時に、この情報は必要ありません。 `IVsTrackProjectDocuments2` は、から提供され <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> ます。

 [追加]、[名前の変更]、および [削除] の各アクションには、 `OnQuery*` メソッドとメソッドがあり `OnAfter*` ます。 メソッドを呼び出して、 `OnQuery*` ファイルまたはディレクトリを追加、名前変更、または削除するアクセス許可を要求します。 `OnAfter*`ファイルまたはディレクトリが追加、名前変更、または削除され、プロジェクトの状態が新しい状態を反映した後に、メソッドを呼び出します。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
