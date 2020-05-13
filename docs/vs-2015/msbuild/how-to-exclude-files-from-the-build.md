---
title: '方法: ビルドからファイルを除外する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, wildcards
- MSBuild, excluding files
- wildcards, MSBuild
ms.assetid: 1be36e45-01da-451c-972d-f9fc0e7d663c
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d7aac21e1ee4d77453808090fc37a3fccaf77e1d
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821611"
---
# <a name="how-to-exclude-files-from-the-build"></a>方法: ビルドからファイルを除外する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクト ファイルでは、ワイルドカードを使用して、1 つのディレクトリ内のすべてのファイル、または入れ子にされたディレクトリのセットをビルドの入力として使用することができます。 しかし、ディレクトリ内の 1 つのファイル、または入れ子にされたディレクトリのセット内の 1 つのディレクトリをビルドの入力に含めたくない場合もあります。 そのファイルまたはディレクトリは、入力の一覧から明示的に除外できます。 また、特定の条件のもとでのみ含めることを望むファイルがプロジェクトに存在することもあります。 ファイルをビルドに含める条件を明示的に宣言できます。  
  
## <a name="excluding-a-file-or-directory-from-the-inputs-for-a-build"></a>ビルドの入力からファイルまたはディレクトリを除外する  
 項目リストは、ビルドの入力ファイルです。 `Include` 属性を使用して、含める項目を個別にまたはグループとして宣言します。 例えば:  
  
```  
<CSFile Include="Form1.cs"/>  
<CSFile Include ="File1.cs;File2.cs"/>  
<CSFile Include="*.cs"/>  
<JPGFile Include="Images\**\*.jpg"/>  
```  
  
 ビルドの入力として 1 つのディレクトリのすべてのファイルまたは入れ子にされたディレクトリのセットを含めるためにワイルドカードを使用した場合に、ディレクトリ内の 1 つ以上のファイル、または入れ子にされたディレクトリのセット内の 1 つのディレクトリを含めたくないと思う可能性があります。 項目リストから項目を除外するには、`Exclude` 属性を使用します。  
  
#### <a name="to-include-all-cs-or-vb-files-except-form2"></a>Form2 を除くすべての .cs ファイルまたは .vb ファイルを含める場合  
  
- 次の `Include` および `Exclude` 属性のうち、いずれかを使用します。  
  
    ```  
    <CSFile Include="*.cs" Exclude="Form2.cs"/>  
    ```  
  
     \- または -  
  
    ```  
    <VBFile Include="*.vb" Exclude="Form2.vb"/>  
    ```  
  
#### <a name="to-include-all-cs-or-vb-files-except-form2-and-form3"></a>Form2 と Form3 を除くすべての .cs ファイルまたは .vb ファイルを含める場合  
  
- 次の `Include` および `Exclude` 属性のうち、いずれかを使用します。  
  
    ```  
    <CSFile Include="*.cs" Exclude="Form2.cs;Form3.cs"/>  
    ```  
  
     \- または -  
  
    ```  
    <VBFile Include="*.vb" Exclude="Form2.vb;Form3.vb"/>  
    ```  
  
#### <a name="to-include-all-jpg-files-in-subdirectories-of-the-images-directory-except-those-in-the-version2-directory"></a>Images ディレクトリのサブディレクトリにあるすべての .jpg ファイルを含めるものの、Version2 ディレクトリのファイルは除外する場合  
  
- 次の `Include` 属性と `Exclude` 属性を使用します。  
  
    ```  
    <JPGFile  
        Include="Images\**\*.jpg"  
        Exclude = "Images\**\Version2\*.jpg"/>  
    ```  
  
    > [!NOTE]
    > 両方の属性にパスを指定する必要があります。 ファイルの場所を指定するのに `Include` 属性で絶対パスを使用する場合、`Exclude` 属性においても絶対パスを使用する必要があります。`Include` 属性で相対パスを使用する場合は、`Exclude` 属性においても相対パスを使用する必要があります。  
  
## <a name="using-conditions-to-exclude-a-file-or-directory-from-the-inputs-for-a-build"></a>条件を使ってビルドの入力からファイルまたはディレクトリを除外する  
 たとえば、デバッグ ビルドには含めるものの、リリース ビルドには含めない項目がある場合には、`Condition` 属性を使用して項目を含める条件を指定できます。  
  
#### <a name="to-include-the-file-formulavb-only-in-release-builds"></a>リリース ビルドにのみファイル Formula.vb を含める場合  
  
- 以下のような `Condition` 属性を使用します。  
  
    ```  
    <Compile  
        Include="Formula.vb"  
        Condition=" '$(Configuration)' == 'Release' " />  
    ```  
  
## <a name="example"></a>例  
 次のコードの例では、Form2.cs を除くディレクトリ内のすべての .cs ファイルを使用してプロジェクトをビルドします。  
  
```  
<Project DefaultTargets="Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <PropertyGroup>  
        <builtdir>built</builtdir>  
    </PropertyGroup>  
  
    <ItemGroup>  
        <CSFile Include="*.cs Exclude="Form2.cs"/>  
  
        <Reference Include="System.dll"/>  
        <Reference Include="System.Data.dll"/>  
        <Reference Include="System.Drawing.dll"/>  
        <Reference Include="System.Windows.Forms.dll"/>  
        <Reference Include="System.XML.dll"/>  
    </ItemGroup>  
  
    <Target Name="PreBuild">  
        <Exec Command="if not exist $(builtdir) md $(builtdir)"/>  
    </Target>  
  
    <Target Name="Compile" DependsOnTargets="PreBuild">  
        <Csc Sources="@(CSFile)"  
            References="@(Reference)"  
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).exe"  
            TargetType="exe" />  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>関連項目
 [項目](../msbuild/msbuild-items.md)   
 [MSBuild](msbuild.md) [方法。ビルドするファイルを選択する](../msbuild/how-to-select-the-files-to-build.md)
