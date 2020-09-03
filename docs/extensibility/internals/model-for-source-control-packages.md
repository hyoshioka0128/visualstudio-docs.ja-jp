---
title: ソース管理パッケージのモデル |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707071"
---
# <a name="model-for-source-control-packages"></a>ソース管理パッケージのモデル
次のモデルは、ソース管理の実装例を表しています。 モデルには、実装する必要があるインターフェイスと、呼び出す必要がある環境サービスが表示されます。 すべてのサービスと同様に、実際には、サービスを通じて取得する特定のインターフェイスのメソッドを呼び出します。 クラスの名前は、ソース管理がどのように実行されているかを簡単に確認できるように識別されます。

 ![SCC&#95;TUP の例](../../extensibility/internals/media/scc_tup.gif "SCC_TUP") ソース管理プロジェクトの例

## <a name="interfaces"></a>インターフェイス
 次の表に示すインターフェイスの一覧を使用して、Visual Studio で新しいプロジェクトの種類のソース管理を実装できます。

|インターフェイス|用途|
|---------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|プロジェクトおよびエディターによって呼び出され、ファイルを保存または変更 (ダーティ) します。 このインターフェイスには、サービスを使用してアクセスし <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> ます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|ファイルまたはディレクトリの追加、削除、または名前変更を行うためのアクセス許可を要求するために、プロジェクトによって呼び出されます。 このインターフェイスは、承認された add、remove、または rename アクションが完了したことを環境に通知するために、プロジェクトによっても呼び出されます。 サービスを使用してアクセスし <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> ます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|プロジェクトがファイルまたはディレクトリを追加、名前変更、または削除したときに通知を受け取るように登録する任意のエンティティによって実装されます。 イベント通知に登録するには、を呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A> ます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|ソース管理パッケージに登録し、ソース管理の状態に関する情報を取得するために、プロジェクトによって呼び出されます。 このインターフェイスには、サービスを使用してアクセスし <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> ます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|ファイルに関する情報のソース管理要求に応答し、プロジェクトファイルに必要なソース管理設定を取得するために、プロジェクトによって実装されます。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
