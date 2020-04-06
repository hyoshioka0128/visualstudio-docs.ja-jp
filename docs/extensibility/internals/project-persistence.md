---
title: プロジェクトの永続性 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 10a9cde91c0181fbfefbaa353c7c3702f4b36819
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706456"
---
# <a name="project-persistence"></a>プロジェクトの永続化
永続性は、プロジェクトの設計上の重要な考慮事項です。 ほとんどのプロジェクトでは、ファイルを表すプロジェクト項目を使用します。[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]また、データがファイルベース以外のプロジェクトもサポートします。 プロジェクトが所有するファイルとプロジェクト ファイルの両方を永続化する必要があります。 IDE は、プロジェクト自体またはプロジェクト項目を保存するように指示します。

 プロジェクトのテンプレートは、プロジェクト ファクトリに渡されます。 テンプレートは、特定のプロジェクトタイプの要件に従って、すべてのプロジェクト項目の初期化をサポートする必要があります。 これらのテンプレートは、後でプロジェクト ファイルとして保存し、ソリューションを通じて IDE によって管理できます。 詳細については、「 プロジェクト ファクトリとソリューション[を使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)」を参照[してください](../../extensibility/internals/solutions-overview.md)。

 プロジェクト項目は、ファイルベースまたは非ファイルベースです。

- ファイルベースの項目は、ローカルまたはリモートにすることができます。 たとえば、C# の Web プロジェクトでは、リモート システム上のファイルへの接続はローカルで保持されますが、ファイル自体はリモート システム上で保持されます。

- ファイルベース以外のアイテムは、データベースまたはリポジトリにアイテムを保存できます。

## <a name="commit-models"></a>コミット モデル
 プロジェクト項目の場所を決定したら、適切なコミット モデルを選択する必要があります。 たとえば、ローカル ファイルを含むファイル ベースのモデルでは、各プロジェクトを自律的に保存できます。 リポジトリ モデルでは、1 つのトランザクションで複数のアイテムを保存できます。 詳細については、「[プロジェクトの種類の設計に関する決定](../../extensibility/internals/project-type-design-decisions.md)」を参照してください。

 ファイル名拡張子を決定するために、プロジェクトは<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>インターフェイスを実装し、オブジェクトのクライアントが [**名前を付けて保存**] ダイアログ ボックスを実装できるようにする情報を**Save As Type**提供します。

 IDE は、`IPersistFileFormat`プロジェクトのインターフェイスを呼び出して、プロジェクトがプロジェクト項目を適切に永続化する必要があることを示します。 したがって、オブジェクトは、そのファイルとフォーマットのすべての側面を所有します。 これには、オブジェクトのフォーマットの名前が含まれます。

 項目がファイルではない場合`IPersistFileFormat`、ファイルベース以外のアイテムがどのように保持されているかはそのままです。 プロジェクトファイル(プロジェクトの .vbp[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]ファイルやプロジェクトの[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)].vcproj ファイルなど)も永続化する必要があります。

 保存操作の場合、IDE は実行中のドキュメント テーブル (RDT) を調べ、階層によって<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem>コマンドが<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>および インターフェイスに渡されます。 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A>メソッドは、項目が変更されたかどうかを判断するために実装されます。 アイテムが含まれた場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A>メソッドは、変更されたアイテムを保存するために実装されます。

 インターフェイスの`IVsPersistHierarchyItem2`メソッドは、項目を再読み込みできるかどうかを判断し、項目が再ロードできるかどうかを判断するために使用されます。 さらに、このメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A>を実装すると、変更されたアイテムを保存せずに破棄できます。

## <a name="see-also"></a>関連項目
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
