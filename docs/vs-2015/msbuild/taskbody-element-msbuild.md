---
title: TaskBody 要素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- TaskBody element [MSBuild]
- <TaskBody> element [MSBuild]
ms.assetid: 49d8741b-f1ea-4470-94fd-a1ac27341a6a
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7918844915d32893491f69b4e7f58a5867c3613c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68144334"
---
# <a name="taskbody-element-msbuild"></a>TaskBody 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`UsingTask``TaskFactory` に渡されるデータを含みます。 詳細については、「[UsingTask Element (MSBuild)](../msbuild/usingtask-element-msbuild.md)」(UsingTask 要素 (MSBuild)) を参照してください。  
  
 \<Project>  
 \<UsingTask>  
 \<TaskBody>  
  
## <a name="syntax"></a>構文  
  
```  
<TaskBody Evaluate="true/false" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`Evaluate`|省略可能な Boolean 属性です。<br /><br /> `true` の場合、MSBuild は内部要素をすべて評価し、タスクがインスタンス化されるときに項目とプロパティを展開してから情報を `TaskFactory` に渡します。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|Data|`TaskBody` タグ間のテキストは `TaskFactory` にそのまま送信されます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[UsingTask](../msbuild/usingtask-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] にタスクを登録する方法を提供します。 1 つのプロジェクトに 0 個以上の `UsingTask` 要素を含めることができます。|  
  
## <a name="example"></a>例  
 次の例では、`Evaluate` 属性で `TaskBody` 要素を使用する方法を示します。  
  
```  
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">  
       <ParameterGroup>  
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>  
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>  
              ...  
</ParameterGroup>  
       <TaskBody Evaluate="true">  
      ... Task factory-specific data ...  
       </TaskBody>  
</UsingTask>  
```  
  
## <a name="see-also"></a>参照  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)   
 [プロジェクトファイルスキーマリファレンス](../msbuild/msbuild-project-file-schema-reference.md)
