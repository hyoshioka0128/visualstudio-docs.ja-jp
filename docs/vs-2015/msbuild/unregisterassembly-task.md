---
title: UnregisterAssembly タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#UnregisterAssembly
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, UnregisterAssembly task
- UnregisterAssembly task [MSBuild]
ms.assetid: 04f549dd-3591-4dda-9c3a-cf6ede9df2c3
caps.latest.revision: 24
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2ef7ef7f4ec930b8aa338a8be33c4009b3009b20
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193237"
---
# <a name="unregisterassembly-task"></a>UnregisterAssembly タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

COM 相互運用のために、指定されたアセンブリの登録を解除します。 [RegisterAssembly タスク](../msbuild/registerassembly-task.md)とは逆の処理になります。  
  
## <a name="parameters"></a>パラメーター  
 `UnregisterAssembly` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|`Assemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 登録解除するアセンブリを指定します。|  
|`AssemblyListFile`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> `RegisterAssembly` タスクと `UnregisterAssembly` タスクの間の状態に関する情報が含まれます。 これにより、`RegisterAssembly` タスクで登録に失敗したアセンブリの登録をタスクが解除しないようにできます。<br /><br /> このパラメーターが指定されている場合、`Assemblies` と `TypeLibFiles` のパラメーターは無視されます。|  
|`TypeLibFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 指定したアセンブリから指定したタイプ アセンブリを登録解除します。 **注:** このパラメーターは、タイプ ライブラリのファイル名がアセンブリ名と異なる場合にのみ必要です。|  
  
## <a name="remarks"></a>解説  
 アセンブリが存在していなくても、このタスクは正常に終了します。 存在しないアセンブリの登録を解除しようとした場合、タスクは警告を発行して正常終了します。 これは、アセンブリ登録をレジストリから削除することが、このタスクのジョブであるためです。 アセンブリが存在しない場合、アセンブリはレジストリに登録されていないため、タスクは正常に終了します。  
  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.AppDomainIsolatedTaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:System.MarshalByRefObject> クラスから継承されます。 `MarshalByRefObject` クラスは <xref:Microsoft.Build.Utilities.Task> クラスと同じ機能を提供しますが、独自のアプリケーション ドメインでインスタンス化できます。  
  
## <a name="example"></a>例  
 次の例では `UnregisterAssembly` タスクを使用して、`OutputPath` と `FileName` のプロパティで指定されたパスにあるアセンブリ (存在する場合) を登録解除します。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <PropertyGroup>  
        <OutputPath>\Output\</OutputPath>  
        <FileName>MyFile.dll</FileName>  
    </PropertyGroup>  
    <Target Name="UnregisterAssemblies">  
        <UnregisterAssembly  
            Condition="Exists('$(OutputPath)$(FileName)')"  
            Assemblies="$(OutputPath)$(FileName)" />  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>参照  
 [RegisterAssembly タスク](../msbuild/registerassembly-task.md)   
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)
