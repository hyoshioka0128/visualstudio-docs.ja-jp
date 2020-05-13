---
title: GenerateTemporaryTargetAssembly タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- build process [WPF MSBuild], XAML page refers to a locally declared type
- GenerateTemporaryTargetAssembly task [WPF MSBuild]
- GenerateTemporaryTargetAssembly task [WPF MSBuild], parameters
- creating an assembly [WPF MSBuild], XAML page refers to a locally declared type
ms.assetid: 92b6539c-6897-45e0-8989-0c234bbfe782
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 69333b87720513244e90c131f052d11099b62e35
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634046"
---
# <a name="generatetemporarytargetassembly-task"></a>GenerateTemporaryTargetAssembly タスク

<xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly> タスクを実行すると、プロジェクト内の少なくとも 1 つの XAML ページが、そのプロジェクトでローカルに宣言されている型を参照している場合に、アセンブリが生成されます。 生成されたアセンブリは、ビルド処理が完了した後、またはビルド処理が失敗した場合に削除されます。

## <a name="task-parameters"></a>タスク パラメーター

| パラメーター | 説明 |
|--------------------------| - |
| `AssemblyName` | 必須の **String** 型のパラメーターです。<br /><br /> プロジェクトのために生成されるアセンブリの短い名前を指定します。この名前は、一時的に生成されるターゲット アセンブリの名前にもなります。 たとえば、プロジェクトが *WinExeAssembly.exe* という名前の Windows 実行可能ファイルを生成する場合、**AssemblyName** パラメーターの値は **WinExeAssembly** になります。 |
| `CompileTargetName` | 必須の **String** 型のパラメーターです。<br /><br /> ソース コード ファイルからアセンブリを生成するために使用される MSBuild ターゲットの名前を指定します。 **CompileTargetName** の一般的な値は、**CoreCompile** です。 |
| `CompileTypeName` | 必須の **String** 型のパラメーターです。<br /><br /> **CompileTargetName** パラメーターで指定したターゲットによって実行されるコンパイルの種類を指定します。 **CoreCompile** ターゲットでは、この値は **Compile** です。 |
| `CurrentProject` | 必須の **String** 型のパラメーターです。<br /><br /> 一時ターゲット アセンブリを必要とするプロジェクトの、MSBuild プロジェクト ファイルの完全なパスを指定します。 |
| `GeneratedCodeFiles` | 省略可能な **ITaskItem[]** パラメーターです。<br /><br /> [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md) タスクによって生成された言語固有のマネージド コード ファイルの一覧を指定します。 |
| `IntermediateOutputPath` | 必須の **String** 型のパラメーターです。<br /><br /> 生成される一時ターゲット アセンブリが格納されるディレクトリを指定します。 |
| `MSBuildBinPath` | 必須の **String** 型のパラメーターです。<br /><br /> 一時ターゲット アセンブリをコンパイルするために必要な *MSBuild.exe* の場所を指定します。 |
| `ReferencePath` | 省略可能な **ITaskItem[]** パラメーターです。<br /><br /> 一時ターゲット アセンブリにコンパイルされる型によって参照されるアセンブリの一覧を、パスおよびファイル名を使用して指定します。 |
| `ReferencePathTypeName` | 必須の **String** 型のパラメーターです。<br /><br /> コンパイル ターゲット (**CompileTargetName**) パラメーターによって使用される、アセンブリ参照の一覧 (**ReferencePath**) を指定するパラメーターを指定します。 適切な値は、**ReferencePath** です。 |

## <a name="remarks"></a>Remarks

[MarkupCompilePass1](../msbuild/markupcompilepass1-task.md) によって実行される最初のマークアップ コンパイル パスでは、XAML ファイルがバイナリ形式にコンパイルされます。 したがって、コンパイラでは、XAML ファイルで使用される型を含んでいる参照アセンブリの一覧が必要になります。 ただし、同じプロジェクト内で定義されている型が XAML ファイルで使用されていると、そのプロジェクトの対応するアセンブリは、プロジェクトがビルドされるまで作成されません。 このため、最初のマークアップ コンパイル パスの間にアセンブリ参照を用意することができません。

代わりに、**MarkupCompilePass1** は、同じプロジェクト内の型への参照を含む XAML ファイルの変換を、[MarkupCompilePass2](../msbuild/markupcompilepass2-task.md) によって実行される 2 番目のマークアップ コンパイル パスまで延期します。 **MarkupCompilePass2** が実行される前に、一時アセンブリが生成されます。 このアセンブリには、マークアップ コンパイル パスが延期された XAML ファイルによって使用される型が含まれます。 **MarkupCompilePass2** の実行時には、生成されたアセンブリへの参照が指定されます。これにより、コンパイルが延期された XAML ファイルをバイナリ形式に変換できるようになります。

## <a name="example"></a>例

次の例では、*Page1.xaml* が同じプロジェクト内の型への参照を含んでいるため、一時アセンブリが作成されます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="GenerateTemporaryTargetAssemblyTask">
    <GenerateTemporaryTargetAssembly
      AssemblyName="WPFMSBuildSample"
      CompileTargetName="CoreCompile"
      CompileTypeName="Compile"
      CurrentProject="FullBuild.proj"
      GeneratedCodeFiles="obj\debug\app.g.cs;obj\debug\Page1.g.cs;obj\debug\Page2.g.cs"
      ReferencePath="c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll"
      IntermediateOutputPath=".\obj\debug\"
      MSBuildBinPath="$(MSBuildBinPath)"
      ReferencePathTypeName="ReferencePath"/>
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [WPF MSBuild のリファレンス](../msbuild/wpf-msbuild-reference.md)
- [タスク リファレンス](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
- [WPF XAML ブラウザー アプリケーションの概要](/dotnet/framework/wpf/app-development/wpf-xaml-browser-applications-overview)
