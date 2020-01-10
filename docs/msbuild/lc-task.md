---
title: LC タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#LC
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, LC task
- LC task [MSBuild]
ms.assetid: d5a53472-6f2a-42b8-a6db-593ca99c9790
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 86525b2c4ddcf36ca85feee31f89f0003f1f9775
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590827"
---
# <a name="lc-task"></a>LC タスク
*LC.exe* をラップします。LC.exe は *.licx* ファイルから *.license* ファイルを生成します。 *LC.exe* の詳細については、「[Lc.exe (ライセンス コンパイラ)](/dotnet/framework/tools/lc-exe-license-compiler)」を参照してください。

## <a name="parameters"></a>パラメーター
`LC` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`LicenseTarget`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> *.licenses* ファイルを生成する実行可能ファイルを指定します。|
|`NoLogo`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> Microsoft 著作権情報を表示しません。|
|`OutputDirectory`|省略可能な `String` 型のパラメーターです。<br /><br /> 出力 *.licenses* ファイルを配置するディレクトリを指定します。|
|`OutputLicense`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> *.licenses* ファイルの名前を指定します。 名前を指定しなかった場合は、 *.licx* ファイルの名前が使用され、 *.licenses* ファイルは、 *.licx* ファイルが含まれているディレクトリに配置されます。|
|`ReferencedAssemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> *.license* ファイルの生成時に読み込む参照コンポーネントを指定します。|
|`SdkToolsPath`|省略可能な `String` 型のパラメーターです。<br /><br /> *resgen.exe* などの SDK ツールのパスを指定します。|
|`Sources`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> *.licenses* ファイルに組み込むライセンス付きコンポーネントを格納するアイテムを指定します。 詳細については、「[Lc.exe (ライセンス コンパイラ)](/dotnet/framework/tools/lc-exe-license-compiler)」にある `/complist` スイッチの説明を参照してください。|

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.ToolTaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.ToolTask> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[ToolTaskExtension Base Class](../msbuild/tooltaskextension-base-class.md)」を参照してください。

## <a name="example"></a>例
`LC` タスクを使用してライセンスをコンパイルする例を次に示します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
<!-- Item declarations, etc -->

    <Target Name="CompileLicenses">
        <LC
            Sources="@(LicxFile)"
            LicenseTarget="$(TargetFileName)"
            OutputDirectory="$(IntermediateOutputPath)"
            OutputLicenses="$(IntermediateOutputPath)$(TargetFileName).licenses"
            ReferencedAssemblies="@(ReferencePath);@(ReferenceDependencyPaths)">

            <Output
                TaskParameter="OutputLicenses"
                ItemName="CompiledLicenseFile"/>
        </LC>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
