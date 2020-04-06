---
title: ソース管理の設計に関する決定 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], design decisions
ms.assetid: 5f60ec1a-5a74-4362-8293-817a4dd73872
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c36bb2b50a72a52aeaeb7712f4ed711845b5e6d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705254"
---
# <a name="source-control-design-decisions"></a>ソース管理のデザインの方針
ソース管理を実装する場合は、プロジェクトに対して次の設計上の決定事項を考慮する必要があります。

## <a name="will-information-be-shared-or-private"></a>情報は共有されるか、プライベートになるのか?
 あなたが行うことができる最も重要な設計上の決定は、どのような情報が共有可能で、何がプライベートであるかです。 たとえば、プロジェクトのファイルの一覧は共有されますが、このファイルの一覧内では、一部のユーザーはプライベート ファイルを使用できます。 コンパイラ設定は共有されますが、スタートアップ プロジェクトは一般的にプライベートです。 設定は純粋に共有されるか、オーバーライドで共有されるか、純粋にプライベートです。 設計上、ソリューション ユーザー オプション (.suo) ファイルなどのプライベートアイテムは に[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]チェックインされません。 .suo ファイルなどのプライベート ファイルや、作成する特定のプライベート ファイル (Visual C# 用の .csproj.user ファイルや Visual Basic の .vbproj.user ファイルなど) には、プライベートな情報を必ず格納してください。

 この決定は包括的なものではなく、品目ごとに行うことができます。

## <a name="will-the-project-include-special-files"></a>プロジェクトに特別なファイルが含まれるか。
 もう 1 つの重要な設計決定は、プロジェクト構造で特殊なファイルを使用するかどうかです。 特殊ファイルは、ソリューション エクスプローラーおよびチェックイン ダイアログ ボックスおよびチェックアウト ダイアログ ボックスに表示されるファイルの基となる隠しファイルです。 特殊ファイルを使用する場合は、次のガイドラインに従ってください。

1. 特殊ファイルをプロジェクトのルート ノードに関連付けないでください。 プロジェクト ファイルは 1 つのファイルである必要があります。

2. プロジェクトで特殊ファイルを追加、削除、または名前変更する場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>ファイルが特殊ファイルであることを示すフラグセットを使用して、適切なイベントを発生する必要があります。 これらのイベントは、適切な<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>メソッドを呼び出すプロジェクトに応答して、環境によって呼び出されます。

3. プロジェクトまたはエディターがファイルを<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>呼び出すとき、そのファイルに関連付けられている特殊ファイルは自動的にチェックアウトされません。親ファイルと共に特殊ファイルを渡します。 環境は渡されるすべてのファイル間の関係を検出し、チェックアウト UI で特殊なファイルを適切に隠します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
