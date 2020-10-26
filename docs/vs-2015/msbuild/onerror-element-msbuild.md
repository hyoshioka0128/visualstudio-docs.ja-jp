---
title: OnError 要素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#OnError
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- OnError Element [MSBuild]
- <OnError Element [MSBuild]
ms.assetid: 765767d3-ecb7-4cd9-ba1e-d9468964dddc
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 46f6907bea5954cffae92b41398717a8247350e0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195660"
---
# <a name="onerror-element-msbuild"></a>OnError 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

失敗したタスクの `ContinueOnError` 属性が `false` の場合、1 つ以上のターゲットが実行されます。  
  
 \<Project>  
 \<Target>  
 \<OnError>  
  
## <a name="syntax"></a>構文  
  
```  
<OnError ExecuteTargets="TargetName"  
    Condition="'String A'=='String B'" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|  
|`ExecuteTargets`|必須の属性です。<br /><br /> タスクが失敗した場合に実行するターゲットです。 ターゲットが複数の場合はセミコロンで区切ります。 複数のターゲットは指定した順序で実行されます。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[移行先](../msbuild/target-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクのコンテナー要素。|  
  
## <a name="remarks"></a>注釈  
 `Target` 要素のタスクの 1 つが失敗し、`ContinueOnError` 属性が `ErrorAndStop` (または `false`) に設定されている場合、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は `OnError` 要素を実行します。 タスクが失敗すると、`ExecuteTargets` 属性で指定されているターゲットが実行されます。 ターゲットに複数の `OnError` 要素がある場合、タスクが失敗すると `OnError` 要素は順番に実行されます。  
  
 属性の詳細については `ContinueOnError` 、「 [Task 要素 (MSBuild)](../msbuild/task-element-msbuild.md)」を参照してください。 ターゲットについては、「[MSBuild ターゲット](../msbuild/msbuild-targets.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次のコードは、`TaskOne` タスクと `TaskTwo` タスクを実行します。 `TaskOne` が失敗した場合、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は `OnError` 要素を評価し、`OtherTarget` ターゲットを実行します。  
  
```  
<Target Name="ThisTarget">  
    <TaskOne ContinueOnError="ErrorAndStop">  
    </TaskOne>  
    <TaskTwo>  
    </TaskTwo>  
    <OnError ExecuteTargets="OtherTarget" />  
</Target>  
```  
  
## <a name="see-also"></a>参照  
 [プロジェクトファイルスキーマリファレンス](../msbuild/msbuild-project-file-schema-reference.md)   
 [ターゲット](../msbuild/msbuild-targets.md)
