---
title: Task 要素 (MSBuild) | Microsoft Docs
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
- Task element [MSBuild]
- <Task> element [MSBuild]
ms.assetid: d82e2485-e5f0-4936-a357-745bacccc299
caps.latest.revision: 26
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6683aac3c5a4314df6fde3d72dd9085b6608d8a3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202265"
---
# <a name="task-element-msbuild"></a>Task 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクのインスタンスを作成し、実行します。 要素名は、作成されるタスクの名前によって決まります。  
  
 \<Project>  
 \<Target>  
  
## <a name="syntax"></a>構文  
  
```  
<Task Parameter1="Value1"... ParameterN="ValueN"  
    ContinueOnError="WarnAndContinue/true/ErrorAndContinue/ErrorAndStop/false"  
    Condition="'String A' == 'String B'" >  
    <Output... />  
</Task>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`Condition`|省略可能な属性です。 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|  
|`ContinueOnError`|省略可能な属性です。 次の値のいずれかを含めることができます。<br /><br /> -   **WarnAndContinue** または **true**。 タスクが失敗すると、 [ターゲット](../msbuild/target-element-msbuild.md) 要素とビルドの後続のタスクが実行され、タスクのすべてのエラーが警告として扱われます。<br />-   **Errorandcontinue**。 タスクが失敗すると、`Target` 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーがエラーとして扱われます。<br />-   **Errorandstop** または **false** (既定値) です。 タスクが失敗すると、`Target` 要素の残りのタスクとビルドは実行されず、`Target` 要素全体とビルドは失敗したと見なされます。<br /><br /> バージョン 4.5 より前の .NET Framework では、`true` 値と `false` 値のみがサポートされます。<br /><br /> 詳細については、「[方法: タスクで発生したエラーを無視する](../msbuild/how-to-ignore-errors-in-tasks.md)」を参照してください。|  
|`Parameter`|タスク クラスに `[Required]` 属性のラベルが付けられた 1 つ以上のプロパティが含まれる場合は必須です。<br /><br /> パラメーター値とその値を含むユーザー定義のタスク パラメーターです。 `Task` 要素には任意の数のパラメーターを指定でき、各属性はタスク クラスの .NET プロパティにマップされます。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[出力](../msbuild/output-element-msbuild.md)|タスクからの出力をプロジェクト ファイルに格納します。 1 つのタスクに 0 個以上の `Output` 要素を指定できます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[移行先](../msbuild/target-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクのコンテナー要素。|  
  
## <a name="remarks"></a>注釈  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイル内の `Task` 要素は、タスクのインスタンスを作成し、そこにプロパティを設定して実行します。 `Output` 要素は、プロジェクト ファイル内の別の場所で使用するプロパティまたは項目に出力パラメーターを格納します。  
  
 タスクの親 `Target` 要素に [OnError](../msbuild/onerror-element-msbuild.md) 要素がある場合は、タスクが失敗して `ContinueOnError` の値が `false` の場合も評価されます。 タスクについて詳しくは、「[MSBuild タスク](../msbuild/msbuild-tasks.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次のコード例は、[Csc タスク](../msbuild/csc-task.md) クラスのインスタンスを作成し、6 つのプロパティを設定し、タスクを実行します。 実行後に、オブジェクトの `OutputAssembly` プロパティの値は `FinalAssemblyName` という項目一覧に配置されます。  
  
```  
<Target Name="Compile" DependsOnTarget="Resources" >  
    <Csc Sources="@(CSFile)"  
          TargetType="library"  
          Resources="@(CompiledResources)"  
          EmitDebugInformation="$(includeDebugInformation)"  
          References="@(Reference)"  
          DebugType="$(debuggingType)" >  
        <Output TaskParameter="OutputAssembly"  
                  ItemName="FinalAssemblyName" />  
    </Csc>  
</Target>  
```  
  
## <a name="see-also"></a>参照  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)   
 [プロジェクトファイルスキーマリファレンス](../msbuild/msbuild-project-file-schema-reference.md)
