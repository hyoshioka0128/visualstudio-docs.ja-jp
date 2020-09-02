---
title: ResourcesGenerator タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- embedding resources into a .resources file [WPF MSBuild]
- ResourcesGenerator task [WPF MSBuild]
- ResourcesGenerator task [WPF MSBuild], parameters
ms.assetid: e782bbac-9ee6-472b-8171-3ee008c77b4e
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fa8b438727160bb5a752643f7ef9791ca5e09245
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682136"
---
# <a name="resourcesgenerator-task"></a>ResourcesGenerator タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:Microsoft.Build.Tasks.Windows.ResourcesGenerator> タスクは、1 つ以上のリソース (.jpg、.ico、.bmp、バイナリ形式の [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)]、その他の種類の拡張子) を .resources ファイルに埋め込みます。  
  
## <a name="task-parameters"></a>タスク パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`OutputPath`|必須の **String** 型のパラメーターです。<br /><br /> 出力ディレクトリのパスを指定します。 パスが絶対パスではない場合は、プロジェクトのルート ディレクトリに対する相対パスとして扱われます。|  
|`OutputResourcesFile`|必須の **ITaskItem[]** 型の出力パラメーターです。<br /><br /> 生成される .resources ファイルのパスと名前を指定します。 パスが絶対パスではない場合、.resources ファイルはプロジェクトのルート ディレクトリに対する相対パスに作成されます。|  
|`ResourcesFiles`|必須の **ITaskItem[]** 型のパラメーターです。<br /><br /> 生成される .resources ファイルに埋め込まれる 1 つ以上のリソースを指定します。|  
  
## <a name="example"></a>例  
 1 つの .bmp リソースを持つ .resources ファイルを作成する例を次に示します。 .bmp リソースは、プロジェクトのルート ディレクトリを基準にした相対ディレクトリに生成されます。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.ResourcesGenerator"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="ResourcesGeneratorTask">  
    <ResourcesGenerator  
      ResourceFiles="Resource1.bmp"  
      OutputPath="myresources"  
      OutputResourcesFile="myresources\my.resources" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>参照  
 [WPF MSBuild リファレンス](../msbuild/wpf-msbuild-reference.md)   
 [タスクリファレンス](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)   
 [WPF アプリケーションのビルド (WPF)](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)
