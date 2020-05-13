---
title: '方法: ターゲットとタスクを構成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
ms.assetid: 92814100-392a-471d-96fd-e26f637d6cc2
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c8ef52638858160822fcc271a53513b130afc3f4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440052"
---
# <a name="how-to-configure-targets-and-tasks"></a>方法 : ターゲットとタスクを構成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

一部の MSBuild タスクは、開発コンピューターの環境に関係なく、それがターゲットとする環境で実行されるように設定できます。 たとえば、64 ビット コンピューターを使用し、32 ビット アーキテクチャをターゲットとするアプリケーションを構築するとき、一部のタスクが 32 ビット プロセスで実行されます。  
  
> [!NOTE]
> ビルド タスクが Visual C# や Visual Basic のような .NET 言語で記述されており、ネイティブのリソースまたはツールを使用しない場合、調整なしで、あらゆるターゲット コンテンツで実行されます。  
  
## <a name="usingtask-attributes-and-task-parameters"></a>UsingTask 属性とタスク パラメーター  
 次の `UsingTask` 属性は、特定のビルド プロセスで、あるタスクのすべての操作に影響を与えます。  
  
- `Runtime` 属性は、それが存在する場合、共通言語ランタイム (CLR) バージョンを設定し、値として `CLR2`、`CLR4`、`CurrentRuntime`、`*` (任意のランタイム) のいずれかを取得します。  
  
- `Architecture` 属性は、それが存在する場合、プラットフォームとビット数を設定し、値として `x86`、`x64`、`CurrentArchitecture`、`*` (任意のアーキテクチャ) のいずれかを取得します。  
  
- `TaskFactory` 属性は、それが存在する場合、タスク インスタンスを作成して実行するタスク ファクトリを設定し、値として `TaskHostFactory` のみを取得します。 詳細については、このドキュメントで後述する「タスク ファクトリ」を参照してください。  
  
```  
<UsingTask TaskName="SimpleTask"   
   Runtime="CLR2"  
   Architecture="x86"  
   AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v3.5.dll" />  
```  
  
 `MSBuildRuntime` パラメーターと `MSBuildArchitecture` パラメーターを利用し、個々のタスクのターゲット コンテキストを設定することもできます。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <Target Name="MyTarget">  
      <SimpleTask MSBuildRuntime="CLR2" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
```  
  
 MSBuild はタスクを実行する前に、一致する (ターゲット コンテキストが同じ) `UsingTask` を探します。  `UsingTask` で指定されているが、該当するタスクにないパラメーターは一致すると見なされます。  タスクで指定されているが、該当する `UsingTask` にないパラメーターも一致すると見なされます。 パラメーター値が `UsingTask` にもタスクにも指定されていない場合、値は既定として `*` (任意のパラメーター) になります。  
  
> [!WARNING]
> 複数の `UsingTask` が存在し、すべてに一致する `TaskName`、`Runtime`、`Architecture` 属性がある場合、最後に評価されたものが他に取って代わります。  
  
 パラメーターがタスクに設定されていると、MSBuild は、それらのパラメーターに一致するか、少なくともそれらと競合しない `UsingTask` を探します。  複数の `UsingTask` が同じタスクのターゲット コンテキストを指定できます。  たとえば、異なるターゲット環境のために異なる実行可能ファイルが与えられているタスクは次のようになります。  
  
```  
<UsingTask TaskName="MyTool"   
   Runtime="CLR2"  
   Architecture="x86"  
   AssemblyFile="$(MyToolsPath)\MyTool.v2.0.dll" />  
  
<UsingTask TaskName="MyTool"   
   Runtime="CLR4"  
   Architecture="x86"  
   AssemblyFile="$(MyToolsPath)\MyTool.4.0.dll" />  
  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <Target Name="MyTarget">  
      <MyTool MSBuildRuntime="CLR2" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
  
```  
  
## <a name="task-factories"></a>タスク ファクトリ  
 MSBuild はタスクを実行する前に、現在のソフトウェア コンテキストで実行するように指定されているかどうかを確認します。  タスクがそのように指定されている場合、MSBuild は AssemblyTaskFactory にタスクを渡します。AssemblyTaskFactory はタスクを現在のプロセスで実行します。現在のプロセスで実行するように指定されていない場合、MSBuild は TaskHostFactory にタスクを渡します。TaskHostFactory は、ターゲット コンテキストに一致するプロセスでタスクを実行します。 現在のコンテキストとターゲット コンテキストが一致する場合でも、`TaskFactory` を `TaskHostFactory` に設定することで、プロセスの外でタスクを実行するように強制できます (隔離、セキュリティ、またはその他の理由から)。  
  
```  
<UsingTask TaskName="MisbehavingTask"   
   TaskFactory="TaskHostFactory"  
   AssemblyFile="$(MSBuildToolsPath)\MyTasks.dll">  
</UsingTask>  
```  
  
## <a name="phantom-task-parameters"></a>ファントム タスク パラメーター  
 他のタスク パラメーターと同様に、`MSBuildRuntime` と `MSBuildArchitecture` はビルド プロパティから設定できます。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <PropertyGroup>  
      <FrameworkVersion>3.0</FrameworkVersion>  
   </PropertyGroup>  
   <Target Name="MyTarget">  
      <SimpleTask MSBuildRuntime="$(FrameworkVerion)" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
```  
  
 他のタスク パラメーターとは異なり、`MSBuildRuntime` と `MSBuildArchitecture` はタスク自体に対しては明白ではありません。  実行しているコンテキストを認識するタスクを作成するには、.NET Framework を呼び出してコンテキストをテストするか、またはビルド プロパティを使って他のタスク パラメーターからコンテキスト情報を渡す必要があります。  
  
> [!NOTE]
> `UsingTask` 属性は、ツールセットと環境のプロパティから設定できます。  
  
 `MSBuildRuntime` および `MSBuildArchitecture` パラメーターは、ターゲット コンテキストを設定する最も柔軟な方法を提供しますが、範囲も最も制限されています。  柔軟性の点では、これらはタスク インスタンス自体で設定され、タスクの実行直前まで評価されないため、評価時とビルド時の両方で使用できるプロパティの完全なスコープからその値を派生できます。  制限については、これらのパラメーターは、特定のターゲットのタスクの特定のインスタンスにのみ適用されます。  
  
> [!NOTE]
> タスク パラメーターは、タスク ホストのコンテキストではなく、親ノードのコンテキストで評価されます。ランタイムまたはアーキテクチャに依存する環境変数は (プログラム ファイルの場所など)、親ノードに一致する値として評価されます。  一方、同じ環境変数がタスクによって直接読み取られた場合は、タスク ホストのコンテキストで正しく評価されます。  
  
## <a name="see-also"></a>関連項目
 [ターゲットとタスクの構成](../msbuild/configuring-targets-and-tasks.md)
