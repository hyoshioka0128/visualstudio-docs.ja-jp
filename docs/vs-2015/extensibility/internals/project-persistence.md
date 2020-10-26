---
title: プロジェクトの永続化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: abbcc1fc1048866ef790a4b6779ed15ef80a9be1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62429523"
---
# <a name="project-persistence"></a>プロジェクトの永続化
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

永続化は、プロジェクトの主要な設計上の考慮事項です。 ほとんどのプロジェクトでは、ファイルを表すプロジェクト項目を使用します。で [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、ファイルベースではないデータを持つプロジェクトもサポートされています。 プロジェクトとプロジェクトファイルの両方によって所有されているファイルを永続化する必要があります。 IDE により、プロジェクト自体またはプロジェクト項目を保存するように指示されます。  
  
 プロジェクトのテンプレートは、プロジェクトファクトリに渡されます。 テンプレートは、特定のプロジェクトの種類の要件に従って、すべてのプロジェクト項目の初期化をサポートする必要があります。 これらのテンプレートは、後でプロジェクトファイルとして保存し、IDE によってソリューションを通じて管理できます。 詳細については、「プロジェクトファクトリと[ソリューション](../../extensibility/internals/solutions-overview.md)[を使用したプロジェクトインスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)」を参照してください。  
  
 プロジェクト項目は、ファイルベースまたはファイルベースではない場合があります。  
  
- ファイルベースのアイテムは、ローカルまたはリモートにすることができます。 たとえば、C# の Web プロジェクトでは、リモートシステム上のファイルへの接続はローカルに保持されますが、ファイル自体はリモートシステムで保持されます。  
  
- ファイルベース以外のアイテムでは、アイテムをデータベースまたはリポジトリに保存できます。  
  
## <a name="commit-models"></a>モデルのコミット  
 プロジェクト項目が配置されている場所を決定したら、適切なコミットモデルを選択する必要があります。 たとえば、ローカルファイルを使用したファイルベースのモデルでは、各プロジェクトを自律的に保存できます。 リポジトリモデルでは、1つのトランザクションに複数のアイテムを保存できます。 詳細については、「 [プロジェクトの種類の設計](../../extensibility/internals/project-type-design-decisions.md)上の決定」を参照してください。  
  
 ファイル名拡張子を決定するために、プロジェクトはインターフェイスを実装します <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 。これにより、オブジェクトのクライアントが [ **名前を** 付けて保存] ダイアログボックスを実装するための情報を提供します。つまり、[名前を **付けて保存** ] ドロップダウンリストに入力し、初期ファイル名拡張子を管理します。  
  
 IDE はプロジェクトのインターフェイスを呼び出し、プロジェクトがプロジェクト項目を必要に応じて永続化する必要がある `IPersistFileFormat` ことを示します。 そのため、オブジェクトは、そのファイルと形式のすべての要素を所有します。 これには、オブジェクトの形式の名前が含まれます。  
  
 項目がファイルでない場合でも、 `IPersistFileFormat` はファイルベースではない項目が永続化される方法になります。 プロジェクトファイル (プロジェクトの場合は .vbp ファイル、 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] プロジェクトの場合は .vcproj ファイルなど) [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] も保存する必要があります。  
  
 保存操作の場合、IDE は実行中のドキュメントテーブル (RDT) を調べ、階層はおよびインターフェイスにコマンドを渡し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> ます。 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A> 項目が変更されているかどうかを判断するために実装されます。 項目にがある場合、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A> メソッドは、変更された項目を保存するために実装されます。  
  
 インターフェイスのメソッドを使用して、 `IVsPersistHierarchyItem2` 項目を再度読み込むことができるかどうかを判断し、項目を再読み込みすることができるかどうかを判断します。 また、メソッドを実装して、変更された <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A> 項目が保存されずに破棄されるようにすることもできます。  
  
## <a name="see-also"></a>参照  
 [チェックリスト: 新しいプロジェクトの種類の作成](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
