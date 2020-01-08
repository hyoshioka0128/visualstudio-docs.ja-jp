---
title: OnError 要素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b2ddf970225d96291f76935838a743ba358eff0f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594878"
---
# <a name="onerror-element-msbuild"></a>OnError 要素 (MSBuild)
失敗したタスクの `ContinueOnError` 属性が `false` の場合、1 つ以上のターゲットが実行されます。

 \<Project> \<Target> \<OnError>

## <a name="syntax"></a>構文

```xml
<OnError ExecuteTargets="TargetName"
    Condition="'String A'=='String B'" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、[条件](../msbuild/msbuild-conditions.md)をご覧ください。|
|`ExecuteTargets`|必須の属性です。<br /><br /> タスクが失敗した場合に実行するターゲットです。 ターゲットが複数の場合はセミコロンで区切ります。 複数のターゲットは指定した順序で実行されます。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [Target](../msbuild/target-element-msbuild.md) | [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] タスクのコンテナー要素。 |

## <a name="remarks"></a>Remarks
 `Target` 要素のタスクの 1 つが失敗し、`ContinueOnError` 属性が `ErrorAndStop` (または `false`) に設定されている場合、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] は `OnError` 要素を実行します。 タスクが失敗すると、`ExecuteTargets` 属性で指定されているターゲットが実行されます。 ターゲットに複数の `OnError` 要素がある場合、タスクが失敗すると `OnError` 要素は順番に実行されます。

 `ContinueOnError` 属性の詳細は、「[Task 要素 (MSBuild)](../msbuild/task-element-msbuild.md)」を参照してください。 ターゲットについては、「[MSBuild ターゲット](../msbuild/msbuild-targets.md)」をご覧ください。

## <a name="example"></a>例
 次のコードは、`TaskOne` タスクと `TaskTwo` タスクを実行します。 `TaskOne` が失敗した場合、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] は `OnError` 要素を評価し、`OtherTarget` ターゲットを実行します。

```xml
<Target Name="ThisTarget">
    <TaskOne ContinueOnError="ErrorAndStop">
    </TaskOne>
    <TaskTwo>
    </TaskTwo>
    <OnError ExecuteTargets="OtherTarget" />
</Target>
```

## <a name="see-also"></a>関連項目
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
- [ターゲット](../msbuild/msbuild-targets.md)
