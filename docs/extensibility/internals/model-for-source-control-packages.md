---
title: ソース管理パッケージのモデル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], model
ms.assetid: 6164b2d3-a622-4de8-bef3-a6de985e9ebd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 46845be1bc22a67d6703af12933945bdfcfa7f4b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707071"
---
# <a name="model-for-source-control-packages"></a>ソース管理パッケージのモデル
次のモデルは、ソース管理の実装例を示しています。 モデルには、実装する必要があるインターフェイスと呼び出す必要がある環境サービスが表示されます。 すべてのサービスと同様に、実際には、サービスを介して取得した特定のインターフェイスのメソッドを呼び出します。 クラスの名前は、ソース管理の実行方法を簡単に確認できるように識別されます。

 ![SCC&#95;TUP の例](../../extensibility/internals/media/scc_tup.gif "SCC_TUP")ソース管理プロジェクトの例

## <a name="interfaces"></a>インターフェイス
 次の表に示すインターフェイスの一覧を使用して、Visual Studio で新しいプロジェクトの種類のソース管理を実装できます。

|インターフェイス|用途|
|---------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|プロジェクトおよび編集者がファイルを保存または変更する前に呼び出されます。 このインターフェイスは、サービスを<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>使用してアクセスされます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|ファイルまたはディレクトリの追加、削除、または名前変更のアクセス許可を要求するために、プロジェクトによって呼び出されます。 このインターフェイスは、承認された追加、削除、または名前変更操作が完了したときに環境に通知するためにプロジェクトによって呼び出されます。 サービスを使用してアクセス<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|プロジェクトがファイルまたはディレクトリを追加、名前変更、または削除するときに通知を受け取るように登録する任意のエンティティによって実装されます。 イベント通知を登録するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>を呼び出します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|ソース管理パッケージに登録し、ソース管理の状態に関する情報を取得するために、プロジェクトによって呼び出されます。 このインターフェイスは、サービスを<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>使用してアクセスされます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|ファイルに関する情報のソース管理要求に応答し、プロジェクト ファイルに必要なソース管理設定を取得するために、プロジェクトによって実装されます。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
