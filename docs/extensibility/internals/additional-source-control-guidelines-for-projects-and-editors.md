---
title: プロジェクトとエディターのソース管理のガイドライン
description: ソース管理をサポートするためにプロジェクトとエディターが従う必要があるガイドラインについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2509f2f6f9da91c3df60d6b041d5ebb6bdd367b6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079008"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>プロジェクトとエディターの追加ソース管理ガイドライン
ソース管理をサポートするためにプロジェクトとエディターが従う必要があるガイドラインがいくつかあります。

## <a name="guidelines"></a>ガイドライン
 また、プロジェクトまたはエディターは、ソース管理をサポートするために次の操作を行う必要があります。

|領域|Project|エディター|詳細|
|----------|-------------|------------|-------------|
|ファイルのプライベートコピー|X||この環境では、ファイルのプライベートコピーがサポートされています。 つまり、プロジェクトに参加している各ユーザーには、そのプロジェクト内のファイルの独自のプライベートコピーが含まれています。|
|ANSI/Unicode の永続性|X|X|永続化コードを記述する場合は、ほとんどのソース管理プログラムが Unicode をサポートしていないため、ANSI 形式のファイルを保持します。|
|ファイルの列挙|X||プロジェクトには、その中にあるすべてのファイルの特定のリストが含まれている必要があり、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (VSH_PROPID_First_Child/Next_Sibling) を使用してファイルの一覧を列挙できる必要があります。 また、プロジェクトでは、実装を通じて項目名 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A> を公開し、実装によって名前参照 (特殊ファイルを含む) をサポートする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> ます。|
|テキスト形式|X|X|可能であれば、異なるバージョンのマージをサポートするために、ファイルはテキスト形式である必要があります。 テキスト形式ではないファイルは、後で他のバージョンのファイルとマージすることはできません。 推奨されるテキスト形式は XML です。|
|参照ベース|X||参照ベースのプロジェクトは、ソース管理で簡単にサポートされています。 ただし、ファイルがディスク上に存在するかどうかに関係なく、プロジェクトが必要に応じてファイルの一覧を作成できる限り、ディレクトリベースのプロジェクトもソース管理でサポートされます。 ソース管理からプロジェクトを開くと、そのファイルの前にプロジェクトファイルが先に停止します。|
|オブジェクトとプロパティを予測可能な順序で永続化する|X|X|マージを容易にするために、ファイルをアルファベット順などの予測可能な順序で保存します。|
|再読み込み|X|X|ディスク上のファイルが変更された場合、エディターは再読み込みできなければなりません。 ソース管理に参加すると、環境はの実装を呼び出すことによって、データを再読み込みし <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> ます。 再読み込みが最も困難なケースは、IVsQueryEditQuerySave:: を呼び出し、情報を処理しているときにチェックアウトが発生した場合です <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 。 ただし、このような状況では、再読み込みコードを実行できる必要があります。<br /><br /> 環境では、プロジェクトファイルが自動的に再読み込みされます。 ただし、入れ子になった <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> プロジェクトファイルの再読み込みをサポートするために、入れ子になった階層がある場合は、プロジェクトを実装する必要があります。|

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
