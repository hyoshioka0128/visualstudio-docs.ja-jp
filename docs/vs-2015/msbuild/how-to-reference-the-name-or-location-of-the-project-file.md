---
title: '方法: プロジェクト ファイルの名前または場所を参照する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- locations, referencing
- locations
- MSBuildProjectName property
- MSBuild, referencing the project file
- names, referencing
- reserved properties
- project files, referencing
ms.assetid: c8fcc594-5d37-4e2e-b070-4d9c012043b5
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: eae8a32d4587b71f238c023d08a1328ce83ba37d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842001"
---
# <a name="how-to-reference-the-name-or-location-of-the-project-file"></a>方法 : プロジェクト ファイルの名前または場所を参照する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

独自のプロパティを作成することなく、プロジェクト ファイル自体のプロジェクトの名前または場所を使用できます。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は、プロジェクトのファイル名とプロジェクトに関連するその他のプロパティを参照する、予約済みのプロパティを提供します。 予約済みプロパティの詳細については、「 [MSBuild の予約済みプロパティと既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)」を参照してください。  
  
## <a name="using-the-msbuildprojectname-property"></a>MSBuildProjectName プロパティの使用  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は、毎回定義することなくプロジェクト ファイルで使用できる、いくつかの予約済みプロパティを提供します。 たとえば、予約済みプロパティ `MSBuildProjectName` はプロジェクト ファイル名への参照を提供します。  
  
#### <a name="to-use-the-msbuildprojectname-property"></a>MSBuildProjectName プロパティを使用するには  
  
- 他のすべてのプロパティの場合と同様に、$() 表記でプロジェクト ファイルのプロパティを参照します。 次に例を示します。  
  
  ```  
  <CSC Sources = "@(CSFile)"   
      OutputAssembly = "$(MSBuildProjectName).exe"/>  
  </CSC>  
  ```  
  
  予約済みのプロパティを使用する利点は、プロジェクト ファイル名への変更がすべて自動的に組み込まれることです。 次回プロジェクトをビルドするとき、出力ファイルに新しい名前が付けられ、追加の操作は必要ありません。  
  
> [!NOTE]
> 予約済みのプロパティは、プロジェクト ファイルで再定義できません。  
  
## <a name="example"></a>例  
 次の例では、プロジェクト ファイルは出力の名前を指定する予約済みのプロパティとして、プロジェクト名を参照します。  
  
```  
<Project xmlns="http://scheams.microsoft.com/developer/msbuild/2003"   
    DefaultTargets = "Compile">  
  
    <!-- Specify the inputs -->  
    <ItemGroup>  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
    <Target Name = "Compile">  
        <!-- Run the Visual C# compilation using  
        input files of type CSFile -->  
        <CSC Sources = "@(CSFile)"  
            OutputAssembly = "$(MSBuildProjectName).exe" >  
            <!-- Set the OutputAssembly attribute of the CSC task  
            to the name of the project -->  
            <Output  
                TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>参照  
[MSBuild](msbuild.md)  
 [MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)
