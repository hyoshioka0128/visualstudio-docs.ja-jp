---
title: '方法: 同じソース ファイルを異なるオプションでビルドする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- source files, building with different options
- MSBuild, properties
- project properties, modifying
- Hello World example [Visual Studio]
ms.assetid: d14f1212-ddd9-434f-b138-f840011b0fb2
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8bf76967363f4c0d97d93c895fbeb6209c8503f0
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821684"
---
# <a name="how-to-build-the-same-source-files-with-different-options"></a>方法: 同じソース ファイルを異なるオプションでビルドする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクトをビルドする場合、同じコンポーネントを異なるビルド オプションでコンパイルすることがよくあります。 たとえば、シンボル情報を付ければデバッグ ビルドを作成でき、シンボル情報なしで最適化を有効にすればリリース ビルドを作成できます。 あるいは、x86 や [!INCLUDE[vcprx64](../includes/vcprx64-md.md)] などのように、特定のプラットフォーム上で実行するようにプロジェクトをビルドできます。 これらのいずれの場合も、ほとんどのビルド オプションは同じままで、ビルド構成を制御するためにいくつかのオプションが変更されるだけです。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、異なるビルド構成を作成するためにプロパティと条件を使用します。  
  
## <a name="using-properties-to-modify-projects"></a>プロパティを使用してプロジェクトを変更  
 `Property` 要素は、一時ディレクトリの場所など、1 つのプロジェクト ファイル内で何回も参照されるような変数を定義したり、デバッグ ビルドとリリース ビルドなど、複数の構成で使用されるプロパティに値を設定したりします。 プロパティの詳細については、「[MSBuild プロパティ](msbuild-properties1.md)」を参照してください。  
  
 プロパティは、プロジェクト ファイルを変更せずにビルドの構成を変更するために使用することができます。 `Property` 要素と `PropertyGroup` 要素の `Condition` 属性により、プロパティの値を変更することができます。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 条件の詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。  
  
#### <a name="to-set-a-group-of-properties-based-on-another-property"></a>プロパティのグループを別のプロパティに基づいて設定するには  
  
- `PropertyGroup` 要素で以下のような `Condition` 属性を使用します。  
  
    ```  
    <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">  
        <DebugType>full</DebugType>  
        <Optimize>no</Optimize>  
    </PropertyGroup>  
    ```  
  
#### <a name="to-define-a-property-based-on-another-property"></a>プロパティを別のプロパティに基づいて定義するには  
  
- `Property` 要素で以下のような `Condition` 属性を使用します。  
  
    ```  
    <DebugType Condition="'$(Flavor)'=='DEBUG'">full</DebugType>  
    ```  
  
## <a name="specifying-properties-on-the-command-line"></a>コマンド ラインでのプロパティの指定  
 複数の構成を受け入れるようにプロジェクト ファイルを作成したら、プロジェクトをビルドするときに構成を変更できなければなりません。 それができるよう、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] ではコマンド ラインで **/property** または **/p** スイッチを使用してプロパティを指定できるようになっています。  
  
#### <a name="to-set-a-project-property-at-the-command-line"></a>コマンド ライン上でプロジェクト プロパティを設定するには  
  
- **/property** スイッチをプロパティおよびプロパティ値と共に使用します。 例えば:  
  
    ```  
    msbuild file.proj /property:Flavor=Debug  
    ```  
  
     \- または -  
  
    ```  
    Msbuild file.proj /p:Flavor=Debug  
    ```  
  
#### <a name="to-specify-more-than-one-project-property-at-the-command-line"></a>コマンド ライン上で 2 つ以上のプロジェクト プロパティを指定するには  
  
- **/property** または **/p** スイッチをプロパティおよびプロパティ値と共に複数回使用するか、 **/property** または **/p** スイッチを 1 回使用し、複数のプロパティをセミコロン (;) で分けます。 例えば:  
  
  ```  
  msbuild file.proj /p:Flavor=Debug;Platform=x86  
  ```  
  
   \- または  
  
  ```  
  msbuild file.proj /p:Flavor=Debug /p:Platform=x86  
  ```  
  
  環境変数はプロパティとしても扱われ、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] によって自動的に組み込まれます。 環境変数の使用方法の詳細については、「[方法: ビルドで環境変数を使用して](../msbuild/how-to-use-environment-variables-in-a-build.md)します。  
  
  コマンド ラインで指定されたプロパティ値は、同じプロパティに対してプロジェクト ファイル内で設定されているどの値よりも優先され、プロジェクト ファイル内の値は環境変数の値よりも優先されます。  
  
  この動作は、プロジェクト タグの `TreatAsLocalProperty` 属性を使用して変更できます。 その属性と共に記載されたプロパティ名については、コマンド ラインで指定されたプロパティ値がプロジェクト ファイル内の値よりも優先されることはありません。 このトピックの後の部分でその例を示します。  
  
## <a name="example"></a>例  
 以下の "Hello World" プロジェクトのコード例には、デバッグ ビルドとリリース ビルドを作成するために使用できる 2 つの新しいプロパティ グループが含まれています。  
  
 このプロジェクトのデバッグ バージョンをビルドするには、以下のように入力します。  
  
```  
msbuild consolehwcs1.proj /p:flavor=debug  
```  
  
 このプロジェクトのリテール バージョンをビルドするには、以下のように入力します。  
  
```  
msbuild consolehwcs1.proj /p:flavor=retail  
```  
  
```  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <!-- Sets the default flavor of an environment variable called   
    Flavor is not set or specified on the command line -->  
    <PropertyGroup>  
        <Flavor Condition="'$(Flavor)'==''">DEBUG</Flavor>  
    </PropertyGroup>  
  
    <!-- Define the DEBUG settings -->  
    <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">  
        <DebugType>full</DebugType>  
        <Optimize>no</Optimize>  
    </PropertyGroup>  
  
    <!-- Define the RETAIL settings -->  
    <PropertyGroup Condition="'$(Flavor)'=='RETAIL'">  
        <DebugType>pdbonly</DebugType>  
        <Optimize>yes</Optimize>  
    </PropertyGroup>  
  
    <!-- Set the application name as a property -->  
    <PropertyGroup>  
        <appname>HelloWorldCS</appname>  
    </PropertyGroup>  
  
    <!-- Specify the inputs by type and file name -->  
    <ItemGroup>  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">  
        <!-- Run the Visual C# compilation using input files  
        of type CSFile -->  
        <CSC  Sources = "@(CSFile)"  
            DebugType="$(DebugType)"  
            Optimize="$(Optimize)"  
            OutputAssembly="$(appname).exe" >  
  
            <!-- Set the OutputAssembly attribute of the CSC  
            task to the name of the executable file that is   
            created -->  
            <Output TaskParameter="OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
## <a name="example"></a>例  
 次の例は、`TreatAsLocalProperty` 属性を使用する方法を示しています。 `Color` プロパティはプロジェクト ファイル内では値 `Blue` であり、コマンド ライン上では値 `Green` です。 プロジェクト タグ内に `TreatAsLocalProperty="Color"` がある場合、コマンド ライン上のプロパティ (`Green`) はプロジェクト ファイル内で定義されているプロパティ (`Blue`) をオーバーライドしません。  
  
 プロジェクトをビルドするには、次のコマンドを入力します。  
  
```  
msbuild colortest.proj /t:go /property:Color=Green  
```  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
ToolsVersion="4.0" TreatAsLocalProperty="Color">  
  
    <PropertyGroup>  
        <Color>Blue</Color>  
    </PropertyGroup>  
  
    <Target Name="go">  
        <Message Text="Color: $(Color)" />  
    </Target>  
</Project>  
  
<!--  
  Output with TreatAsLocalProperty="Color" in project tag:  
     Color: Blue  
  
  Output without TreatAsLocalProperty="Color" in project tag:  
     Color: Green  
-->  
```  
  
## <a name="see-also"></a>関連項目
[MSBuild](msbuild.md)  
 [MSBuild の概念](../msbuild/msbuild-concepts.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [Project 要素 (MSBuild)](../msbuild/project-element-msbuild.md)
