---
title: FindUnderPath タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#FindUnderPath
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, FindUnderPath task
- FindUnderPath task [MSBuild]
ms.assetid: 3c6d58b0-36e8-47aa-bfca-b73dd2045d91
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1c679352fb8db81379ab93e800efa9f631773c36
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149743"
---
# <a name="findunderpath-task"></a>FindUnderPath タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定した項目コレクションの中で、指定したフォルダーの中にあるか、下にあるパスが含まれる項目を判断します。  
  
## <a name="parameters"></a>パラメーター  
 `FindUnderPath` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`Files`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> `Path` パラメーターで指定したパスと比較する必要のあるパスのファイルを指定します。|  
|`InPath`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 指定したパスの下で見つかった項目が含まれます。|  
|`OutOfPath`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 指定したパスの下で見つからなかった項目が含まれます。|  
|`Path`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> 参照として使用するフォルダー パスを指定します。|  
|`UpdateToAbsolutePaths`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> true の場合、出力項目のパスが絶対パスになります。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`FindUnderPath` タスクを利用し、`MyFiles` 項目に含まれるファイルに、`SearchPath` プロパティによって指定されるパスの下に存在するパスがあるか判断します。 タスク完了後、`FilesNotFoundInPath` 項目に `File1.txt` ファイルが含まれ、`FilesFoundInPath` 項目に `File2.txt` ファイルが含まれます。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <MyFiles Include="C:\File1.txt" />  
        <MyFiles Include="C:\Projects\MyProject\File2.txt" />  
    </ItemGroup>  
  
    <PropertyGroup>  
        <SearchPath>C:\Projects\MyProject</SearchPath>  
    </PropertyGroup>  
  
    <Target Name="FindFiles">  
        <FindUnderPath  
            Files="@(MyFiles)"  
            Path="$(SearchPath)">  
            <Output  
                TaskParameter="InPath"  
                ItemName="FilesFoundInPath" />  
            <Output  
                TaskParameter="OutOfPath"  
                ItemName="FilesNotFoundInPath" />  
        </FindUnderPath>  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>関連項目
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [タスク](../msbuild/msbuild-tasks.md)   
 [MSBuild の概念](../msbuild/msbuild-concepts.md)
