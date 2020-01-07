---
title: CreateItem タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#CreateItem
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CreateItem task [MSBuild]
- MSBuild, CreateItem task
ms.assetid: c4311f38-979e-4324-b524-9e8c1cbdc41a
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 758491a068fe2c2c7318717f5481b41839c49a3f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63419773"
---
# <a name="createitem-task"></a>CreateItem タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

項目コレクションに入力項目を設定します。 これにより、リスト間で項目をコピーできるようになります。  
  
> [!NOTE]
> このタスクは非推奨とされます。 .NET Framework 3.5 以降、項目グループは [Target](../msbuild/target-element-msbuild.md) 要素内に配置できます。 詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。  
  
## <a name="attributes"></a>属性  
 `CreateItem` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AdditionalMetadata`|省略可能な `String` 型の配列パラメーターです。<br /><br /> 出力項目にアタッチする追加のメタデータを指定します。  項目のメタデータの名前と値を次の構文で指定します。<br /><br /> *MetadataName* `=` *MetadataValue*<br /><br /> メタデータの名前と値のペアを複数指定する場合は、セミコロンで区切る必要があります。 名前または値にセミコロンまたは他の特殊文字が含まれる場合は、エスケープする必要があります。 詳細については、「[方法 :MSBuild で特殊文字をエスケープ](../msbuild/how-to-escape-special-characters-in-msbuild.md)します。|  
|`Exclude`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 出力項目コレクションから除外する項目を指定します。 このパラメーターには、ワイルドカードの指定を含めることができます。 詳細については、「[項目](../msbuild/msbuild-items.md)」と「[方法: ビルドからファイルを除外する](../msbuild/how-to-exclude-files-from-the-build.md)します。|  
|`Include`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` パラメーター。<br /><br /> 出力項目のコレクションに含める項目を指定します。 このパラメーターには、ワイルドカードの指定を含めることができます。|  
|`PreserveExistingMetadata`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `True` の場合は、まだ存在しない場合にのみ追加メタデータを適用します。|  
  
## <a name="remarks"></a>Remarks  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例では、項目コレクション `MySourceItems` から、`MySourceItemsWithMetadata` という名前の新しい項目コレクションを作成します。 `CreateItem` タスクは、`MySourceItems` 項目コレクションの項目を新しい項目コレクションに設定します。 その後、名前が `MyMetadata` で値が `Hello` の追加メタデータ エントリを、新しいコレクションの各項目に追加します。  
  
 タスクを実行した後、`MySourceItemsWithMetadata` 項目コレクションには項目 `file1.resx` と `file2.resx` が含まれ、どちらにも `MyMetadata` のメタデータ エントリが追加されています。 `MySourceItems` 項目コレクションは変更されません。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <MySourceItems Include="file1.resx;file2.resx" />  
    </ItemGroup>  
  
    <Target Name="NewItems">  
        <CreateItem  
            Include="@(MySourceItems)"  
            AdditionalMetadata="MyMetadata=Hello">  
           <Output  
               TaskParameter="Include"  
               ItemName="MySourceItemsWithMetadata"/>  
        </CreateItem>  
  
    </Target>  
  
</Project>  
```  
  
 次の表では、タスク実行後の出力項目の値について説明します。 項目のメタデータは、項目の後にかっこで囲まれて示されます。  
  
|項目コレクション|目次|  
|---------------------|--------------|  
|`MySourceItemsWithMetadata`|`file1.resx` (`MyMetadata="Hello"`)<br /><br /> `file2.resx` (`MyMetadata="Hello"`)|  
  
## <a name="see-also"></a>関連項目
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [タスク](../msbuild/msbuild-tasks.md)
