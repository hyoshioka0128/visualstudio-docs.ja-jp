---
title: '[新しい項目の追加] ダイアログボックスに貢献する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d288f2d007fd0f923021847179326069959d3698
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197017"
---
# <a name="contributing-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスへの投稿
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトのサブタイプでは、[ **新しい項目の追加** ] ダイアログボックスに項目の完全な新しいディレクトリを指定できます。そのためには、レジストリサブキーの下に項目テンプレートを **追加** し `Projects` ます。  
  
## <a name="registering-add-new-item-templates"></a>新しい項目の追加テンプレートを登録しています  
 このセクションは、レジストリの **HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0\projects** にあります。 以下のレジストリエントリは、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] プロジェクトが仮定のプロジェクトサブタイプによって集計されていることを前提としています。 プロジェクトのエントリを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 以下に示します。  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}]  
@="#2143"  
"DefaultProjectExtension"="vbproj"  
"PossibleProjectExtensions"="vbproj;vbp"  
"ProjectTemplatesDir"="visualStudioInstallPath\\Vb\\.\\VBProjects"  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}\AddItemTemplates\TemplateDirs\{12345678-1234-1234-1122334455667788}\/1]  
@="#100"  
"TemplatesDir"="projectSubTypeTemplatesDir\\VBProjectItems"  
```  
  
 `AddItemTemplates\TemplateDirs`サブキーには、[**新しい項目の追加**] ダイアログボックスで使用できるようになった項目が配置されるディレクトリへのパスを含むレジストリエントリが格納されます。  
  
 環境では、レジストリサブキーの下にあるすべてのデータが自動的に読み込まれ `AddItemTemplates` `Projects` ます。 これには、基本プロジェクトの実装のデータだけでなく、特定の種類のプロジェクトのサブタイプのデータも含まれます。 各プロジェクトのサブタイプは、プロジェクトの種類によって識別され `GUID` ます。 プロジェクトのサブタイプでは、 `Add Item` 実装内のから列挙をサポートして `VSHPROPID_ AddItemTemplatesGuid` プロジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> サブタイプの GUID 値を返すことによって、特定の flavored プロジェクトインスタンスに対して別のテンプレートのセットを使用するように指定できます。 `VSHPROPID_AddItemTemplatesGuid`プロパティが指定されていない場合は、基本プロジェクト GUID が使用されます。  
  
 [ **新しい項目の追加** ] ダイアログボックスで項目をフィルター処理するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> プロジェクトのサブタイプアグリゲーターオブジェクトにインターフェイスを実装します。 たとえば、プロジェクトを集計することによってデータベースプロジェクトを実装するプロジェクトのサブタイプでは、フィルター処理を実装することで、[ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **新しい項目の追加** ] ダイアログボックスから特定の項目をフィルター処理できます。また、でをサポートすることによって、データベースプロジェクト固有の項目を追加することもでき `VSHPROPID_ AddItemTemplatesGuid` <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> ます。 [ **新しい項目の追加** ] ダイアログボックスにフィルターを適用して項目を追加する方法の詳細については、「 [[新しい項目の追加] ダイアログボックスへの項目](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)の追加」を参照してください。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
