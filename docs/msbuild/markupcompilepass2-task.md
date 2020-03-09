---
title: MarkupCompilePass2 タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- performing second-pass markup [WPF MSBuild], MarkupCompilePass2 task
- MarkupCompilePass2 task [WPF MSBuild]
- MarkupCompilePass2 task [WPF MSBuild], parameters
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d18bc3638454e2a6b034cd2e35c3a158361a033e
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633526"
---
# <a name="markupcompilepass2-task"></a>MarkupCompilePass2 タスク

<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> タスクでは、同じプロジェクト内で型を参照する XAML ファイルの 2 回目のマークアップのコンパイルが実行されます。

## <a name="task-parameters"></a>タスク パラメーター

| パラメーター | 説明 |
| - | - |
| `AlwaysCompileMarkupFilesInSeparateDomain` | 省略可能な **Boolean** 型のパラメーターです。<br /><br /> 別の <xref:System.AppDomain> でタスクを実行するかどうかを指定します。 このパラメーターが **false** を返す場合、タスクは MSBuild と同じ <xref:System.AppDomain> 内で、より高速に実行されます。 このパラメーターが **true** を返す場合、タスクは MSBuild から分離された 2 番目の <xref:System.AppDomain> 内で実行され、動作はより低速になります。 |
| `AssembliesGeneratedDuringBuild` | 省略可能な **String[]** 型のパラメーターです。<br /><br /> ビルド処理時に変更されるアセンブリへの参照を指定します。 たとえば、Visual Studio ソリューションには、別のプロジェクトのコンパイル済み出力を参照するプロジェクトが含まれていることがあります。 この場合、別のプロジェクトのコンパイル済み出力を **AssembliesGeneratedDuringBuild** に追加できます。<br /><br /> メモ:**AssembliesGeneratedDuringBuild** は、ビルド ソリューションによって生成されるアセンブリの完全なセットへの参照を含んでいる必要があります。 |
| `AssemblyName` | 必須の **String** 型のパラメーターです。<br /><br /> プロジェクトのために生成されるアセンブリの短い名前を指定します。 たとえば、プロジェクトが *WinExeAssembly.exe* という名前の実行可能ファイルを生成する場合、**AssemblyName** パラメーターの値は **WinExeAssembly** になります。 |
| `GeneratedBaml` | 省略可能な **ITaskItem[]** 型の出力パラメーターです。<br /><br /> XAML バイナリ形式で生成されたファイルの一覧を含みます。 |
| `KnownReferencePaths` | 省略可能な **String[]** 型のパラメーターです。<br /><br /> ビルド処理時に変更されないアセンブリへの参照を指定します。 グローバル アセンブリ キャッシュ (GAC)、.NET インストール ディレクトリなどにあるアセンブリが含まれます。 |
| `Language` | 必須の **String** 型のパラメーターです。<br /><br /> コンパイラがサポートするマネージド言語を指定します。 有効なオプションは **C#** 、**VB**、**JScript**、**C++** です。 |
| `LocalizationDirectivesToLocFile` | 省略可能な **String** 型のパラメーターです。<br /><br /> 各ソース XAML ファイルのローカリゼーション情報を生成する方法を指定します。 有効なオプションは、**None**、**CommentsOnly**、および **All** です。 |
| `OutputPath` | 必須の **String** 型のパラメーターです。<br /><br /> XAML バイナリ形式ファイルが生成されるディレクトリを指定します。 |
| `OutputType` | 必須の **String** 型のパラメーターです。<br /><br /> プロジェクトで生成されるアセンブリの型を指定します。 有効なオプションは、**winexe**、**exe**、**library**、および **netmodule** です。 |
| `References` | 省略可能な **ITaskItem[]** パラメーターです。<br /><br /> XAML ファイル内で使用される型を含む、ファイルからアセンブリへの参照の一覧を指定します。 そのうちの 1 つは、<xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly> タスクによって生成されたアセンブリへの参照です。このタスクは、<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> タスクの前に実行しておく必要があります。 |
| `RootNamespace` | 省略可能な **String** 型のパラメーターです。<br /><br /> プロジェクト内部にあるクラスのルート名前空間を指定します。 **RootNamespace** は、対応する XAML ファイルが `x:Class` 属性を含まない場合に、生成されるマネージド コード ファイルの既定の名前空間としても使用されます。 |
| `XAMLDebuggingInformation` | 省略可能な **Boolean** 型のパラメーターです。<br /><br /> **true** の場合、デバッグを支援するために、診断情報が生成され、コンパイルされた XAML 内に追加されます。 |

## <a name="remarks"></a>Remarks

**MarkupCompilePass2** を実行する前に、マークアップ コンパイル パスが延期された XAML ファイルによって使用される型を含む、一時アセンブリを生成する必要があります。 一時アセンブリを生成するには、**GenerateTemporaryTargetAssembly** タスクを実行します。

<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> の実行時には、生成された一時アセンブリへの参照を指定します。これにより、最初のマークアップ コンパイル パスでコンパイルが延期された XAML ファイルをバイナリ形式にコンパイルできるようになります。

## <a name="example"></a>例

<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> タスクを使用して 2 番目のコンパイル パスを実行する方法を次の例に示します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.MarkupCompilePass2"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="MarkupCompilePass2Task">
    <MarkupCompilePass2
      AssemblyName="WPFMSBuildSample"
      Language="C#"
      OutputType="WinExe"
      OutputPath="obj\Debug\"
      References=".\obj\debug\WPFMSBuildSample.exe;c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll" />
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [WPF MSBuild のリファレンス](../msbuild/wpf-msbuild-reference.md)
- [WPF MSBuild タスク リファレンス](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [MSBuild タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
- [WPF XAML ブラウザー アプリケーションの概要](/dotnet/framework/wpf/app-development/wpf-xaml-browser-applications-overview)
