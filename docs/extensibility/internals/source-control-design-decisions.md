---
title: ソース管理の設計上の決定 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], design decisions
ms.assetid: 5f60ec1a-5a74-4362-8293-817a4dd73872
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3a7c8a902520323f548a7dd77a84b07a56bfc9a0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723609"
---
# <a name="source-control-design-decisions"></a>ソース管理のデザインの方針
ソース管理を実装する場合は、次の設計上の決定事項をプロジェクトで考慮する必要があります。

## <a name="will-information-be-shared-or-private"></a>情報は共有または非公開になりますか。
 作成できる最も重要な設計上の決定は、どの情報が共有可能であり、どのようなものがプライベートであるかということです。 たとえば、プロジェクトのファイルの一覧は共有されますが、このファイルの一覧内では、ユーザーによってはプライベートファイルが必要になる場合があります。 コンパイラ設定は共有されますが、スタートアッププロジェクトは一般にプライベートです。 設定は、純粋に共有するか、上書きと共有するか、純粋にプライベートにします。 設計上、ソリューションユーザーオプション (.suo) ファイルなどのプライベート項目は [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] にチェックインされません。 個人情報は、.suo ファイルなどのプライベートファイル、または作成した特定のプライベートファイル (たとえば、Visual C#の場合は .csproj ファイル、Visual Basic の場合は .vbproj ファイル) に保存してください。

 この決定は、すべてを網羅するものではなく、項目ごとに行うことができます。

## <a name="will-the-project-include-special-files"></a>プロジェクトには特殊なファイルが含まれますか。
 もう1つの重要な設計上の決定は、プロジェクト構造で特別なファイルを使用するかどうかです。 特別なファイルは、ソリューションエクスプローラーおよびチェックインとチェックアウトのダイアログボックスに表示されるファイルの基になる隠しファイルです。 特別なファイルを使用する場合は、次のガイドラインに従ってください。

1. 特別なファイルは、プロジェクトのルートノード (つまり、プロジェクトファイル自体) に関連付けないでください。 プロジェクトファイルは1つのファイルである必要があります。

2. プロジェクトで特別なファイルを追加、削除、または名前変更する場合は、ファイルが特別なファイルであることを示すフラグを設定して、適切な <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> イベントを発生させる必要があります。 これらのイベントは、適切な <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> メソッドを呼び出しているプロジェクトに応答して環境によって呼び出されます。

3. プロジェクトまたはエディターがファイルの <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> を呼び出すと、そのファイルに関連付けられている特殊なファイルは自動的にはチェックアウトされません。で、特別なファイルを親ファイルと共に渡します。 環境によって、渡されたすべてのファイルの関係が検出され、チェックアウト UI の特殊ファイルが適切に非表示になります。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
