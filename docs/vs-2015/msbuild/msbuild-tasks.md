---
title: MSBuild タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- tasks
- MSBuild, tasks
ms.assetid: 5d3cc4a7-e5db-4f73-b707-8b6882fddcf8
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 756c19da1aeb8878c2d045f4ee471d8449d2a954
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154810"
---
# <a name="msbuild-tasks"></a>MSBuild タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ビルド プラットフォームでは、ビルドの処理中に、いくつかのアクションを実行する権限が必要です。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は*タスク*を使用して、これらのアクションを実行します。 タスクとは、分割不可能なビルド操作を実行するために [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] で使用される実行可能コードの単位です。  
  
## <a name="task-logic"></a>タスクのロジック  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] XML プロジェクト ファイル形式はそれ自体でビルド操作を完全に実行することができないため、プロジェクト ファイルの外部でタスクのロジックを実装する必要があります。  
  
 タスクの実行ロジックは、<xref:Microsoft.Build.Framework> 名前空間で定義されている <xref:Microsoft.Build.Framework.ITask> インターフェイスを実装する .NET クラスとして実装されます。  
  
 タスク クラスは、プロジェクト ファイル内のタスクで使用可能な入力パラメーターと出力パラメーターも定義します。 タスク クラスによって公開されている、パブリックに設定可能な非静的かつ非抽象のプロパティはどれも、プロジェクト ファイル内でアクセスできます。そのためには、同じ名前を持つ、対応する属性を [Task](../msbuild/task-element-msbuild.md) 要素に指定します。  
  
 <xref:Microsoft.Build.Framework.ITask> インターフェイスを実装するマネージド クラスを記述することにより、独自のタスクを作成できます。 詳細については、「[タスクの作成](../msbuild/task-writing.md)」を参照してください。  
  
## <a name="executing-a-task-from-a-project-file"></a>プロジェクト ファイルからのタスクの実行  
 プロジェクト ファイルでタスクを実行する前に、まずタスクを実装するアセンブリ内の型を、[UsingTask](../msbuild/usingtask-element-msbuild.md) 要素でタスク名にマップする必要があります。 これにより、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は、プロジェクト ファイルでタスクを見つけたら、どこでその実行ロジックを探すかが把握できます。  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルのタスクを実行するには、`Target` 要素の子として、そのタスクの名前を持つ要素を作成します。 タスクがパラメーターを受け取る場合、パラメーターは要素の属性として渡されます。  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] の項目一覧とプロパティはパラメーターとして使用できます。 たとえば、次のコードは `MakeDir` タスクを呼び出し、`MakeDir` オブジェクトの `Directories` プロパティの値を、前の例で宣言された `BuildDir` プロパティの値に等しくなるよう設定します。  
  
```  
<Target Name="MakeBuildDirectory">  
    <MakeDir  
        Directories="$(BuildDir)" />  
</Target>  
```  
  
 また、タスクはプロジェクト ファイルに情報を返すこともできます。この情報は、後で使用するために項目またはプロパティに格納できます。 たとえば、次のコードは `Copy` タスクを呼び出して、`SuccessfullyCopiedFiles` 項目一覧に `CopiedFiles` 出力プロパティからの情報を格納します。  
  
```  
<Target Name="CopyFiles">  
    <Copy  
        SourceFiles="@(MySourceFiles)"  
        DestinationFolder="@(MyDestFolder)">  
        <Output  
            TaskParameter="CopiedFiles"  
            ItemName="SuccessfullyCopiedFiles"/>  
     </Copy>  
</Target>  
```  
  
## <a name="included-tasks"></a>含まれているタスク  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] には、ファイルをコピーする [Copy](../msbuild/copy-task.md)、ディレクトリを作成する [MakeDir](../msbuild/makedir-task.md)、[!INCLUDE[csprcs](../includes/csprcs-md.md)] ソース コード ファイルをコンパイルする [Csc](../msbuild/csc-task.md) など、多数のタスクが装備されています。 使用可能なすべてのタスクと使用法については、「[Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)」を参照してください。  
  
## <a name="overridden-tasks"></a>オーバーライドされたタスク  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は、複数の場所でタスクを検索します。 最初の検索場所は、.NET Framework ディレクトリに格納されている拡張子が .OverrideTasks であるファイル内です。 これらのファイル内のタスクは、プロジェクト ファイル内のタスクも含め、同じ名前を持つ他のタスクをオーバーライドします。 2 番目の検索場所は、.NET Framework ディレクトリ内の拡張子が .Tasks であるファイル内です。 タスクがこれらの場所のいずれにも見つからない場合は、プロジェクト ファイル内のタスクが使用されます。  
  
## <a name="see-also"></a>関連項目
 [MSBuild の概念](../msbuild/msbuild-concepts.md)   
 [MSBuild](msbuild.md)   
 [タスクの作成](../msbuild/task-writing.md)   
 [インライン タスク](../msbuild/msbuild-inline-tasks.md)
