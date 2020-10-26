---
title: ResolveNonMSBuildProjectOutput タスク | Microsoft Docs
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
- MSBuild, ResolveNonMSBuildProjectOutput task
- ResolveNonMSBuildProjectOutput task [MSBuild]
ms.assetid: a0b8fcec-8c8d-4867-85ac-5304c5108e5e
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: aaf99affe9c29762aa8b47ea76419da429089b7c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156155"
---
# <a name="resolvenonmsbuildprojectoutput-task"></a>ResolveNonMSBuildProjectOutput タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild 以外のプロジェクト参照に対する出力ファイルを確認します。  
  
## <a name="parameters"></a>パラメーター  
 `ResolveNonMSBuildProjectOutput` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|`PreresolvedProjectOutputs`|省略可能な `String` 型のパラメーターです。<br /><br /> 解決済みのプロジェクト出力を含む XML 文字列を指定します。|  
|`ProjectReferences`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> プロジェクト参照を指定します。|  
|`ResolvedOutputPaths`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 解決済みの参照パスの一覧が含まれます (また、元のプロジェクト参照属性を保持します)。|  
|`UnresolvedProjectReferences`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 出力の事前解決リストを使用して解決できなかったプロジェクト参照項目のリストが含まれます。<br /><br /> Visual Studio は非 MSBuild プロジェクトのみを事前解決するためです。つまり、この一覧のプロジェクト参照は MSBuild 形式です。|  
  
## <a name="remarks"></a>解説  
 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加パラメーターとその説明の一覧については、「 [Taskextension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)
