---
title: AssignCulture タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#AssignCulture
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, AssignCulture task
- AssignCulture task [MSBuild]
ms.assetid: 8f8314cc-82a6-4f16-a62d-b9f0d1d5e274
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 23b991efaa32e2c1886e6e0cd64bb9d6181190d0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187047"
---
# <a name="assignculture-task"></a>AssignCulture タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このタスクは、有効な .NET カルチャ ID 文字列をファイル名の一部として含む可能性がある項目の一覧を受け取り、対応するカルチャ ID を含む `Culture` という名前のメタデータを持つ項目を生成します。 たとえば、ファイル名 Form1.fr-fr.resx には、"fr-fr" というカルチャ ID が埋め込まれています。したがって、このタスクでは、`fr-fr` と等しい値の `Culture` メタデータを持つ同じファイル名の項目が生成されます。 また、このタスクでは、ファイル名からカルチャを削除したファイル名の一覧も生成されます。  
  
## <a name="task-parameters"></a>タスク パラメーター  
 `AssignCulture` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AssignedFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> `Files` パラメーターで受信した項目の一覧が含まれています。各項目には `Culture` メタデータ エントリが追加されています。<br /><br /> `Files` パラメーターから受信した項目に既に `Culture` メタデータ エントリが含まれている場合は、この元のメタデータ エントリが使用されます。<br /><br /> このタスクでは、ファイル名に有効なカルチャ ID が含まれている場合にのみ、`Culture` メタデータ エントリが割り当てられます。 カルチャ ID は、ファイル名の最後の 2 つのドットの間にある必要があります。|  
|`AssignedFilesWithCulture`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> `AssignedFiles` パラメーターの項目のうち、`Culture` メタデータ エントリを持つ項目のサブセットが含まれています。|  
|`AssignedFilesWithNoCulture`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> `AssignedFiles` パラメーターの項目のうち、`Culture` メタデータ エントリを持たない項目のサブセットが含まれています。|  
|`CultureNeutralAssignedFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> `AssignedFiles` パラメーターに生成された項目の同じ一覧が含まれていますが、ファイル名からカルチャが削除されています。<br /><br /> このタスクでは、カルチャ ID が有効な場合にのみ、ファイル名からカルチャが削除されます。|  
|`Files`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> カルチャを割り当てるためのカルチャ名が埋め込まれたファイルの一覧を指定します。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 `ResourceFiles` 項目コレクションを指定して `AssignCulture` タスクを実行する例を以下に示します。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ResourceFiles Include="MyResource1.fr.resx"/>  
        <ResourceFiles Include="MyResource2.XX.resx"/>  
    </ItemGroup>  
  
    <Target Name="Culture">  
        <AssignCulture  
            Files="@(ResourceFiles)"  
            <Output TaskParameter="AssignedFiles"  
                ItemName="OutAssignedFiles"/>  
            <Output TaskParameter="AssignedFilesWithCulture"  
                ItemName="OutAssignedFilesWithCulture"/>  
            <Output TaskParameter="AssignedFilesWithNoCulture"  
                ItemName="OutAssignedFilesWithNoCulture"/>  
            <Output TaskParameter="CultureNeutralAssignedFiles"  
                ItemName="OutCultureNeutralAssignedFiles"/>  
        </AssignCulture>  
    </Target>  
</Project>  
```  
  
 次の表では、タスク実行後の出力項目の値について説明します。 項目のメタデータは、項目の後にかっこで囲まれて示されます。  
  
|項目コレクション|目次|  
|---------------------|--------------|  
|`OutAssignedFiles`|`MyResource1.fr.resx (Culture="fr")`<br /><br /> `MyResource2.XX.resx` (追加メタデータなし)|  
|`OutAssignedFilesWithCulture`|`MyResource1.fr.resx (Culture="fr")`|  
|`OutAssignedFilesWithNoCulture`|`MyResource2.XX.resx` (追加メタデータなし)|  
|`OutCultureNeutralAssignedFiles`|`MyResource1.resx (Culture="fr")`<br /><br /> `MyResource2.XX.resx (`追加メタデータなし)|  
  
## <a name="see-also"></a>関連項目
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
