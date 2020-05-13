---
title: プロジェクトおよび編集者に関する追加のソース管理ガイドライン |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 181f6c10ff7ce95cd3a37151f117353d1bb47d41
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710115"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>プロジェクトおよびエディターの追加ソース管理ガイドライン
ソース管理をサポートするために、プロジェクトや編集者が遵守すべきガイドラインは数多くあります。

## <a name="guidelines"></a>ガイドライン
 ソース管理をサポートするには、プロジェクトまたはエディターで次の操作も行う必要があります。

|領域|Project|エディター|詳細|
|----------|-------------|------------|-------------|
|ファイルのプライベート コピー|X||この環境では、ファイルのプライベート コピーがサポートされています。 つまり、プロジェクトに参加している各ユーザーは、そのプロジェクト内のファイルの独自のプライベート コピーを持っています。|
|ANSI/ユニコードの永続性|X|X|永続性コードを記述する場合は、ほとんどのソース管理プログラムは現在 Unicode をサポートしていないため、ANSI 形式でファイルを永続化します。|
|ファイルの列挙|X||プロジェクトには、その中のすべてのファイルの特定のリストが含まれている必要があり、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>または<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>(VSH_PROPID_First_Child/Next_Sibling) を使用してファイルの一覧を列挙できる必要があります。 プロジェクトは、その実装を通じて項目<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A>名を公開し、その実装を通じて名前の<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A>検索 (特殊なファイルを含む) をサポートする必要があります。|
|テキスト形式|X|X|可能な場合、ファイルは、異なるバージョンのマージをサポートするためにテキスト形式である必要があります。 テキスト形式でないファイルは、後で他のバージョンのファイルとマージすることはできません。 推奨されるテキスト形式は XML です。|
|リファレンスベース|X||参照ベースのプロジェクトは、ソース管理で容易にサポートされます。 ただし、ディレクトリ ベースのプロジェクトは、ディスク上に存在するかどうかに関係なく、プロジェクトが必要に応じてファイルの一覧を生成できる限り、ソース管理でもサポートされます。 ソース管理からプロジェクトを開くと、プロジェクト ファイルは、そのファイルの前に最初にダウンします。|
|予測可能な順序でオブジェクトとプロパティを永続化する|X|X|ファイルをアルファベット順など、予測可能な順序で保存して、マージを容易にします。|
|再読み込み|X|X|ディスク上のファイルが変更された場合、エディタは再読み込みできる必要があります。 ソース管理に参加すると、環境は実装を呼び出すことによってデータを再<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>ロードします。 最も困難な再読み込みケースは、チェックアウトが発生したときに IVsQueryEditQuerySave::<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>を呼び出し、情報を処理している場合です。 ただし、このような状況では、リロード コードを実行できる必要があります。<br /><br /> 環境は、プロジェクト ファイルを自動的に再ロードします。 ただし、入れ子になった<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>プロジェクト ファイルの再読み込みをサポートするために、入れ子になった階層がある場合は、プロジェクトを実装する必要があります。|

## <a name="see-also"></a>関連項目
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
