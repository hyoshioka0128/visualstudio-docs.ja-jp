---
title: '方法 : ビルドをクリーンする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- Exec task [MSBuild]
- MSBuild, cleaning a build
- directories [.NET Framework], for output items
- output, removing items
ms.assetid: 999ba473-b0c4-45c7-930a-63ea7a510509
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f8c64bb19d65540f8c72be9acb1c5f59deb3c8f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156649"
---
# <a name="how-to-clean-a-build"></a>方法 : ビルドをクリーンする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ビルドをクリーンするとき、すべての中間ファイルと出力ファイルが削除され、プロジェクト ファイルとコンポーネント ファイルが残ります。 プロジェクト ファイルとコンポーネント ファイルから、中間ファイルと出力ファイルの新しいインスタンスをビルドできます。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] とともに提供されている一般的なタスクのライブラリには、システム コマンドの実行に利用できる [Exec](../msbuild/exec-task.md) タスクが含まれています。 タスクのライブラリに関する情報については、「[タスク リファレンス](../msbuild/msbuild-task-reference.md)」を参照してください。  
  
## <a name="creating-a-directory-for-output-items"></a>出力項目のディレクトリを作成する  
 既定では、プロジェクトのコンパイル時に作成される .exe ファイルは、プロジェクトおよびソース ファイルと同じディレクトリに置かされます。 ただし、一般的には、出力項目は別個のディレクトリに作成されます。  
  
#### <a name="to-create-a-directory-for-output-items"></a>出力項目のディレクトリを作成するには  
  
1. `Property` 要素を利用し、ディレクトリの場所と名前を定義します。 たとえば、プロジェクトおよびソースファイルを含むディレクトリに `BuiltApp` という名前のディレクトリを作成します。  
  
     `<builtdir>BuiltApp</builtdir>`  
  
2. ディレクトリが存在しない場合、[MakeDir](../msbuild/makedir-task.md) タスクを理使用してディレクトリを作成します。 次に例を示します。  
  
     `<MakeDir Directories = "$(builtdir)"`  
  
     `Condition = "!Exists('$(builtdir)')" />`  
  
## <a name="removing-the-output-items"></a>出力項目を削除する  
 中間ファイルと出力ファイルの新しいインスタンスを作成する前に、以前のインスタンスをすべて消去しておくことをお勧めします。 [RemoveDir](../msbuild/removedir-task.md) タスクを利用し、ディレクトリとそれに含まれるすべてのファイルとディレクトリをディスクから削除します。  
  
#### <a name="to-remove-a-directory-and-all-files-contained-in-the-directory"></a>ディレクトリとそのディレクトリに含まれるすべてのファイルを削除するには  
  
- `RemoveDir` タスクを利用してディレクトリを削除します。 次に例を示します。  
  
     `<RemoveDir Directories="$(builtdir)" />`  
  
## <a name="example"></a>例  
 次のコード例プロジェクトには、新しいターゲット、`Clean` が含まれています。このターゲットは `RemoveDir` タスクを使用し、ディレクトリとそのディレクトリに含まれるすべてのファイルを削除します。 この例ではまた、`Compile` ターゲットは、ビルドのクリーン時に削除される出力項目に対して別個のディレクトリを作成します。  
  
 `Compile` は既定のターゲットとして定義されます。そのため、別のターゲットを指定しない限り、自動的に使用されます。 コマンド ライン スイッチ **/target** を使用し、別のターゲットを指定します。 次に例を示します。  
  
 `msbuild <file name>.proj /target:Clean`  
  
 **/target** スイッチは **/t** に短縮できます。また、複数のターゲットを指定できます。 たとえば、ターゲット `Clean` を使用し、次にターゲット `Compile` を使用するには、次のように入力します。  
  
 `msbuild <file name>.proj /t:Clean;Compile`  
  
```  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <PropertyGroup>  
        <!-- Set the application name as a property -->  
        <name>HelloWorldCS</name>  
  
        <!-- Set the output folder as a property -->  
        <builtdir>BuiltApp</builtdir>  
    </PropertyGroup>  
  
    <ItemGroup>  
        <!-- Specify the inputs by type and file name -->  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">  
        <!-- Check whether an output folder exists and create  
        one if necessary -->  
        <MakeDir Directories = "$(builtdir)"   
            Condition = "!Exists('$(builtdir)')" />  
  
        <!-- Run the Visual C# compiler -->  
        <CSC Sources = "@(CSFile)"   
            OutputAssembly = "$(BuiltDir)\$(appname).exe">  
            <Output TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
  
    <Target Name = "Clean">  
        <RemoveDir Directories="$(builtdir)" />  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>関連項目
 [Exec タスク](../msbuild/exec-task.md)   
 [MakeDir タスク](../msbuild/makedir-task.md)   
 [RemoveDir タスク](../msbuild/removedir-task.md)   
 [Csc タスク](../msbuild/csc-task.md)   
 [ターゲット](../msbuild/msbuild-targets.md)
