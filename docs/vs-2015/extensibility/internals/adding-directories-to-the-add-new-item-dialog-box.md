---
title: '[新しい項目の追加] ダイアログボックスにディレクトリを追加する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f370d208cb8f7aad88f806983983ccee9f584625
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203925"
---
# <a name="adding-directories-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスへの新しいディレクトリの追加
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次のコード例は、[ **新しい項目の追加** ] ダイアログボックスのディレクトリの新しいセットを登録する方法を示しています。 [ **新しい項目の追加** ] ダイアログボックスのディレクトリは、プロジェクトごとに異なります。 そのため、ディレクトリは、次のように Projects サブキーの下に登録され \<HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects> ます。  
  
## <a name="the-registry-script"></a>レジストリスクリプト  
  
```  
NoRemove Projects  
{  
  NoRemove %GUID_Project%  
  {  
    NoRemove AddItemTemplates  
    {  
      NoRemove TemplateDirs  
      {  
        ForceRemove %CLSID_Package%  
        {  
      ForceRemove /1 = s '#%Folder_Label_ResID%'  
          {  
            val TemplatesDir = s '%Template_Path%'     
            val SortPriority = d 2000  
          }  
        }  
      }  
    }  
  }  
}  
```  
  
 Template_Path 値は、プロジェクトテンプレートを含むディレクトリの完全パスを指定します。 これらのテンプレートには、.vsz ファイルまたは複製する典型的なテンプレートファイルを指定できます。  
  
 SortPriority 値は、並べ替えの優先順位を指定します。  
  
## <a name="adding-items-to-an-existing-project"></a>既存のプロジェクトへの項目の追加  
 既存のプロジェクトに項目を追加することもできます。 たとえば、プロジェクトの場合は、" [!INCLUDE[csprcs](../../includes/csprcs-md.md)] \CSharpProjectItems\LocalProjectItems" フォルダーに項目を追加でき \<root> ます。 この場合、 `%GUID_Project%` は C# プロジェクト ({FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}) の GUID です。  
  
 また、プロジェクトのサブタイプをプログラミングすることによって、既存のプロジェクトを拡張することもできます。 プロジェクトのサブタイプを使用すると、新しいプロジェクトの種類を記述せずにプロジェクトを拡張できます。 プロジェクトのサブタイプの詳細については、「 [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [プロジェクトテンプレートと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)   
 [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [[新しいプロジェクト] ダイアログ ボックスへの新しいディレクトリの追加](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
