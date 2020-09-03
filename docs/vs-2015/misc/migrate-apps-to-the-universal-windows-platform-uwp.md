---
title: アプリをユニバーサル Windows プラットフォームに移行する (UWP) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 5279ab9b-71d9-4be5-81f6-a1f24b06f5fb
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 60951091914474f07f19672799fb59c8b2d0aa56
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75919137"
---
# <a name="migrate-apps-to-the-universal-windows-platform-uwp"></a>アプリを Universal Windows Platform (UWP) へ移行する
Visual Studio 2015 RC で作成された Windows Store 8.1 アプリ、Windows Phone 8.1 アプリ、またはユニバーサル Windows アプリ用の既存のプロジェクト ファイルに必要な変更を手動で加え、Visual Studio 2015 RTM で使用できるようにします。 (Windows アプリのプロジェクトと Windows Phone プロジェクトの両方を備えた Windows 8.1 ユニバーサル アプリがある場合、各プロジェクトを移行するための手順に従う必要があります。)

 ユニバーサル Windows プラットフォームの場合は、今すぐにアプリのターゲットを 1 つ以上のデバイス ファミリにします。 ユニバーサル Windows アプリについて詳しくは、この「 [プラットフォーム ガイド](https://msdn.microsoft.com/library/windows/apps/dn894631.aspx)」を参照してください。

- [既存の C#/VB の Windows ストア 8.1 または Windows Phone 8.1 アプリを移行して](#MigrateCSharp) ユニバーサル Windows プラットフォームを使用するようにします。

- [既存の C++ の Windows ストア 8.1 または Windows Phone 8.1 アプリを移行して](#MigrateCPlusPlus) ユニバーサル Windows プラットフォームを使用するようにします。

- [Visual Studio 2015 RC で作成された既存のユニバーサル Windows アプリに必要な変更](#PreviousVersions)。

- [Visual Studio 2015 RC で作成されたユニバーサル Windows アプリの既存の単体テスト プロジェクトに必要な変更](#MigrateUnitTest)。

  これらのすべての変更を加えない場合は、新しいユニバーサル Windows プロジェクトに [既存のアプリを移植する方法](https://msdn.microsoft.com/library/windows/apps/xaml/mt238321.aspx) を参照してください。

## <a name="migrate-your-cvb-windows-store-81-or-windows-phone-81-apps-to-use-the-universal-windows-platform"></a><a name="MigrateCSharp"></a> C#/VB Windows ストア8.1 または Windows Phone 8.1 アプリを移行して、ユニバーサル Windows プラットフォームを使用する

#### <a name="migrate-your-cvb-project-files"></a>C#/VB プロジェクト ファイルを移行する

1. インストールされているユニバーサル Windows プラットフォームを見つけるには、次のフォルダーを開きます: **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 これには、インストールされているユニバーサル Windows プラットフォームごとのフォルダーの一覧が含まれています。 フォルダー名は、インストールされているユニバーサル Windows プラットフォームのバージョンです。 たとえば、この Windows 10 デバイスには、ユニバーサル Windows プラットフォームのバージョン 10.0.10240.0 がインストールされています。

     ![フォルダーを開いてインストールされているバージョンを表示する](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

     ユニバーサル Windows プラットフォームの複数のバージョンをインストールすることができます。 アプリに対応した最新バージョンを使用することをお勧めします。

2. ファイル エクスプローラーを使用して、UWP プロジェクトが保存されているフォルダーに移動します。 このフォルダー内に .json ファイルを作成します。 ファイルの名前を project.json にして、次の内容をこのファイルに追加します。

    ```json
    {
      "dependencies": {
        "Microsoft.ApplicationInsights": "1.0.0",
        "Microsoft.ApplicationInsights.PersistenceChannel": "1.0.0",
        "Microsoft.ApplicationInsights.WindowsApps": "1.0.0",
        "Microsoft.NETCore.UniversalWindowsPlatform": "5.0.0"
      },
      "frameworks": {
        "uap10.0": {}
      },
      "runtimes": {
        "win10-arm": {},
        "win10-arm-aot": {},
        "win10-x86": {},
        "win10-x86-aot": {},
        "win10-x64": {},
        "win10-x64-aot": {}
      }
    }

    ```

3. 以下の内容で、default.rd.xml という名前のファイルを作成します。 VB プロジェクトがある場合、このファイルをプロジェクトのマイ プロジェクト ディレクトリに追加します。 C# プロジェクトがある場合、このファイルをプロジェクトのプロパティ ディレクトリに追加します。

    ```xml
    <?xml version="1.0"?>
    <!-- This file contains Runtime Directives used by .NET Native. The defaults here are suitable for most developers. However, you can modify these parameters to modify the behavior of the .NET Native optimizer. Runtime Directives are documented at http://go.microsoft.com/fwlink/?LinkID=391919 To fully enable reflection for App1.MyClass and all of its public/private members <Type Name="App1.MyClass" Dynamic="Required All"/> To enable dynamic creation of the specific instantiation of AppClass<T> over System.Int32 <TypeInstantiation Name="App1.AppClass" Arguments="System.Int32" Activate="Required Public" /> Using the Namespace directive to apply reflection policy to all the types in a particular namespace <Namespace Name="DataClasses.ViewModels" Seralize="All" /> -->
    <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata"><Application>
    <!-- An Assembly element with Name="*Application*" applies to all assemblies in the application package. The asterisks are not wildcards. -->
    <Assembly Dynamic="Required All" Name="*Application*"/>
    <!-- Add your application specific runtime directives here. -->
    </Application></Directives>
    ```

4. Visual Studio で、既存の Windows Store 8.1 アプリまたは Windows Phone 8.1 アプリを含むソリューションを開きます。

5. ソリューション エクスプローラーで、アプリの既存のプロジェクトを右クリックし、 **[プロジェクトのアンロード]** を選択します。 プロジェクトをアンロードした後、プロジェクト ファイルを再度右クリックして、.csproj または .vbproj ファイルの編集を選択します。

     ![プロジェクトを右クリックし、[編集] をクリックします](../misc/media/uap-editproject.png "UAP_EditProject")

6. 値が \<PropertyGroup> 8.1 の要素を含む要素を探し \<TargetPlatformVersion> ます。 この要素に対して次の手順を実行し \<PropertyGroup> ます。

    1. 要素の値 \<Platform> を **x86**に設定します。

    2. 要素を追加 \<TargetPlatformIdentifier> し、その値を **UAP**に設定します。

    3. 要素の既存の値 \<TargetPlatformVersion> を、インストールしたユニバーサル Windows プラットフォームバージョンの値に変更します。 また、要素を追加 \<TargetPlatformMinVersion> し、同じ値を指定します。

    4. 要素の値 \<MinimumVisualStudioVersion> を **14**に変更します。

    5. 要素を \<ProjectTypeGuids> 次のように置き換えます。

         C# の場合 :

        ```xml
        <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
        ```

         VB の場合:

        ```xml
        <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{F184B08F-C81C-45F6-A57F-5ABD9991F28F}</ProjectTypeGuids>
        ```

    6. 要素を追加 \<EnableDotNetNativeCompatibleProfile> し、その値を **true**に設定します。

    7. ユニバーサル Windows アプリの既定のアセット スケールは 200 です。 200でスケーリングされていない資産がプロジェクトに含まれている場合は、 \<UapDefaultAssetScale> 資産のスケールの値を持つ要素をこの PropertyGroup に追加する必要があります。 詳細については、「 [資産とスケール](https://msdn.microsoft.com/library/jj679352.aspx)」を参照してください。

         ここで、 \<PropertyGroup> 要素は次の例のようになります。

        ```xml
        <PropertyGroup>
            …
             <Platform Condition=" '$(Platform)' == '' ">x86</Platform>
             <TargetPlatformVersion>10.0.10240.0</TargetPlatformVersion>
             <TargetPlatformMinVersion>10.0.10240.0</TargetPlatformMinVersion>
             <TargetPlatformIdentifier>UAP</TargetPlatformIdentifier>
             <MinimumVisualStudioVersion>14</MinimumVisualStudioVersion>
             <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
        <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>
             <UapDefaultAssetScale>100</UapDefaultAssetScale>
             …
        </PropertyGroup>
        ```

7. 現在使用している Visual Studio のバージョンを反映するように、12.0 のすべてのインスタンスを 14.0 に置き換えます。 たとえば、以下のインスタンスです。

    ```xml
    <Project Tools Version="14.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    ```

    ```
    <PropertyGroup Condition=" '$(VisualStudioVersion)' == '' or '$(VisualStudioVersion)' < '14.0' ">
        <VisualStudioVersion>14.0</VisualStudioVersion>
    ```

8. \<PropertyGroup>条件属性の一部として AnyCPU プラットフォームに対して構成されている要素を検索します。 これらの要素と、そのすべての子を削除します。 Visual Studio 2015 RC において、AnyCPU は Windows 10 アプリではサポートされていません。 たとえば、次のような要素を削除する必要があり \<PropertyGroup> ます。

    ```xml
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
        <PlatformTarget>AnyCPU</PlatformTarget>
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <Optimize>false</Optimize>
        <OutputPath>bin\Debug\</OutputPath>
        <DefineConstants>DEBUG;TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
        <PlatformTarget>AnyCPU</PlatformTarget>
        <DebugType>pdbonly</DebugType>
        <Optimize>true</Optimize>
        <OutputPath>bin\Release\</OutputPath>
        <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
      </PropertyGroup>
    ```

9. 残りの各要素について \<PropertyGroup> 、要素にリリース構成の Condition 属性があるかどうかを確認します。 含まれているが、要素が含まれていない場合は、それを \<UseDotNetNativeToolchain> 追加します。 次のように、要素の値を \<UseDotNetNativeToolchain> true に設定します。

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|x64'">
        <OutputPath>bin\x64\Release\</OutputPath>
        <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
        <Optimize>true</Optimize>
        <NoWarn>;2008</NoWarn>
        <DebugType>pdbonly</DebugType>
        <PlatformTarget>x64</PlatformTarget>
        <UseVSHostingProcess>false</UseVSHostingProcess>
        <ErrorReport>prompt</ErrorReport>
        <Prefer32Bit>true</Prefer32Bit>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>
    ```

10. Windows Phone プロジェクトの場合のみ、 \<PropertyGroup> WindowsPhoneApp という値を持つ要素を含む要素を削除し \<TargetPlatformIdentifier> ます。 また、この要素の子をすべて削除します。

    ```xml
    <PropertyGroup Condition=" '$(TargetPlatformIdentifier)' == '' ">
      <TargetPlatformIdentifier>WindowsPhoneApp</TargetPlatformIdentifier>
    </PropertyGroup>
    ```

11. 要素を \<ItemGroup> 含む要素を検索 \<AppxManifest> します。 次の \<None> 要素を要素の子として追加し \<ItemGroup> ます。

    ```xml
    <None Include="project.json" />
    ```

12. \<ItemGroup>プロジェクトに追加された他のアセット (logo .png ファイル () など) が含まれている要素を検索 \<Content Include="Assets\Logo.scale-100.png" /> します。 次の \<Content> 子要素をこの要素に追加し \<ItemGroup> ます。

     **C# の場合 :**

    ```xml
    <Content Include="Properties\default.rd.xml" />
    ```

     **VB の場合:**

    ```xml
    <Content Include="My Project\default.rd.xml" />
    ```

13. \<ItemGroup> \<Reference> NuGet パッケージの子要素を含む要素を検索します。 プロジェクトを再読み込みした後に、NuGet パッケージ マネージャーで NuGet パッケージをダウンロードする必要があるため、使用する NuGet パッケージに注意してください。 この \<ItemGroup> を子と共に削除します。 たとえば、ある UWP プロジェクトでは次の NuGet パッケージを削除する必要があるかもしれません。

    ```xml
    <ItemGroup>
        <Reference Include="Microsoft.ApplicationInsights, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
          <HintPath>..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.dll</HintPath>
          <Private>True</Private>
        </Reference>
        <Reference Include="Microsoft.ApplicationInsights.Extensibility.Windows, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
          <HintPath>..\packages\Microsoft.ApplicationInsights.WindowsApps.0.14.3-build00177\lib\win81\Microsoft.ApplicationInsights.Extensibility.Windows.dll</HintPath>
          <Private>True</Private>
        </Reference>
        <Reference Include="Microsoft.ApplicationInsights.PersistenceChannel, Version=0.14.3.186, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
          <HintPath>..\packages\Microsoft.ApplicationInsights.PersistenceChannel.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.PersistenceChannel.dll</HintPath>
          <Private>True</Private>
        </Reference>
        <Reference Include="System.Numerics.Vectors, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
          <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.dll</HintPath>
          <Private>True</Private>
        </Reference>
        <Reference Include="System.Numerics.Vectors.WindowsRuntime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
          <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.WindowsRuntime.dll</HintPath>
          <Private>True</Private>
        </Reference>
      </ItemGroup>
    ```

14. 変更を保存します。

15. .csproj または .vbproj ファイルを閉じます。

16. ソリューション エクスプローラーでプロジェクトを右クリックし、コンテキスト メニューの [プロジェクトの再読み込み] をクリックします。 これで、プロジェクト内のすべてのファイルがソリューション エクスプローラーに表示されます。

17. 前の手順で削除したパッケージを再度追加するには、NuGet マネージャーを使用します。

     次に、Windows ストア 8.1 または Windows Phone 8.1 プロジェクトの [パッケージ マニフェスト ファイルを更新する](#PackageManifest) 手順に従う必要があります。

## <a name="migrate-your-c-windows-store-81-or-windows-phone-81-apps-to-use-the-universal-windows-platform"></a><a name="MigrateCPlusPlus"></a> C++ Windows ストア8.1 または Windows Phone 8.1 アプリを移行して、ユニバーサル Windows プラットフォームを使用する

#### <a name="migrate-your-c-project-files"></a>C++ プロジェクト ファイルを移行する

1. インストールされているユニバーサル Windows プラットフォームを見つけるには、次のフォルダーを開きます: **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 これには、インストールされているユニバーサル Windows プラットフォームごとのフォルダーの一覧が含まれています。 フォルダー名は、インストールされているユニバーサル Windows プラットフォームのバージョンです。 たとえば、この Windows 10 デバイスには、ユニバーサル Windows プラットフォームのバージョン 10.0.10240.0 がインストールされています。

     ![フォルダーを開いてインストールされているバージョンを表示する](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

     ユニバーサル Windows プラットフォームの複数のバージョンをインストールすることができます。 アプリに対応した最新バージョンを使用することをお勧めします。

2. Visual Studio で、既存の C++ Windows Store 8.1 アプリまたは Windows Phone 8.1 アプリを含むソリューションを開きます。

     ソリューション エクスプローラーで、既存のプロジェクトを右クリックし、 **[プロジェクトのアンロード]** を選択します。 プロジェクトをアンロードした後、プロジェクト ファイルを再度右クリックして、.vcxproj ファイルの編集を選択します。

     ![右&#45;[プロジェクトファイル] をクリックし、[編集] を選択します。](../misc/media/uap-editcplusproject.png "UAP_EditCPlusProject")

3. 値が \<PropertyGroup> 8.1 の要素を含む要素を探し \<ApplicationTypeRevision> ます。 この要素に対して次の手順を実行し \<PropertyGroup> ます。

    1. \<WindowsTargetPlatformVersion>要素と要素を追加 \<WindowsTargetPlatformMinVersion> し、インストールしたユニバーサル Windows プラットフォームバージョンの値を指定します。

    2. ApplicationTypeRevision 要素の値を 8.1 から 10.0 に更新します。

    3. 要素の値 \<MinimumVisualStudioVersion> を14に変更します。

    4. 要素を追加 \<EnableDotNetNativeCompatibleProfile> し、その値を true に設定します。

    5. ユニバーサル Windows アプリの既定のアセット スケールは 200 です。 200でスケーリングされていない資産がプロジェクトに含まれている場合は、 \<UapDefaultAssetScale> 資産のスケールの値を持つ要素をこの PropertyGroup に追加する必要があります。 詳細については、「 [資産とスケール](https://msdn.microsoft.com/library/jj679352.aspx)」を参照してください。

    6. Windows Phone プロジェクトの場合のみ、の値を \<ApplicationType> Windows Phone から Windows ストアに変更します。

         ここで、 \<PropertyGroup> 要素は次の例のようになります。

        ```xml
        <PropertyGroup>
            …
                  <WindowsTargetPlatformVersion>10.0.10240.0</WindowsTargetPlatformVersion>
        <WindowsTargetPlatformMinVersion>10.0.10240.0</WindowsTargetPlatformMinVersion>
             <ApplicationType>Windows Store</ApplicationType>
             <ApplicationTypeRevision>10.0</ApplicationTypeRevision>
             <MinimumVisualStudioVersion>14</MinimumVisualStudioVersion>
             <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>
             <UapDefaultAssetScale>100</UapDefaultAssetScale>
             …
        </PropertyGroup>
        ```

4. 要素のすべてのインスタンスの \<PlatformToolset> 値を v140 に変更します。 次に例を示します。

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'" Label="Configuration">
        <ConfigurationType>Application</ConfigurationType>
        <UseDebugLibraries>false</UseDebugLibraries>
        <WholeProgramOptimization>true</WholeProgramOptimization>
        <PlatformToolset>v140</PlatformToolset>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>
    ```

5. 残りの各要素について \<PropertyGroup> 、要素にリリース構成の Condition 属性があるかどうかを確認します。 含まれているが、要素が含まれていない場合は、それを \<UseDotNetNativeToolchain> 追加します。 次のように、要素の値を \<UseDotNetNativeToolchain> true に設定します。

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|X64'" Label="Configuration">
        <ConfigurationType>Application</ConfigurationType>
        <UseDebugLibraries>false</UseDebugLibraries>
        <WholeProgramOptimization>true</WholeProgramOptimization>
        <PlatformToolset>v140</PlatformToolset>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>

    ```

6. 変更を保存します。 その後、プロジェクト ファイルを閉じます。

7. ソリューション エクスプローラーでプロジェクト ファイルを右クリックし、コンテキスト メニューの [プロジェクトの再読み込み] をクリックします。 これで、プロジェクト内のすべてのファイルがソリューション エクスプローラーに表示されます。

     次に、Windows ストア 8.1 または Windows Phone 8.1 プロジェクトの [パッケージ マニフェスト ファイルを更新する](#PackageManifest) 手順に従う必要があります。

## <a name="update-your-package-manifest-file-for-all-your-windows-store-81-or-windows-phone-81-projects"></a><a name="PackageManifest"></a> すべての Windows ストア8.1 または Windows Phone 8.1 プロジェクトのパッケージマニフェストファイルを更新する
 ソリューション内のプロジェクトごとに、パッケージのマニフェスト ファイルを更新する必要があります。

#### <a name="update-your-package-manifest-file"></a>パッケージ マニフェスト ファイルを更新する

1. プロジェクトの Package.appxmanifest ファイルを開きます。 Windows ストアと Windows Phone のプロジェクトごとに、Package.AppxManifest ファイルを編集する必要があります。

2. \<Package>既存のプロジェクトの種類に基づいて、新しいスキーマを使用して要素を更新する必要があります。 最初に、Windows ストアまたは Windows Phone プロジェクトがあるかどうかに基づいて、以下のスキーマを削除します。

    **Windows ストアプロジェクトの古いバージョン:**\<Package>要素は次のようになります。

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/2010/manifest"
       xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest">

   ```

    **Windows Phone プロジェクトの古いバージョン:**\<Package>要素は次のようになります。

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/2010/manifest"
   xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest"
   xmlns:m3="http://schemas.microsoft.com/appx/2014/manifest"
   xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest">
   ```

    **ユニバーサル Windows プラットフォームの新:** 以下のスキーマを要素に追加し \<Package> ます。 削除したスキーマの要素から、関連した名前空間の識別子のプレフィックスを削除します。 IgnorableNamespaces プロパティを uap mp に更新します。 新しい \<Package> 要素は次のようになります。

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
       xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
       xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
      IgnorableNamespaces= "uap mp">

   ```

3. \<Dependencies>要素に子要素を追加 \<Package> します。 次に \<TargetDeviceFamily> \<Dependencies> 、Name、MinVersion、および MaxVersionTested テストされた属性を使用して、この要素に子要素を追加します。 Name 属性の値に Windows.Universal を指定します。 MinVersion と MaxVersionTested に、インストールしたユニバーサル Windows プラットフォームのバージョンの値を指定します。 この要素は次のようになります。

   ```xml
   <Dependencies>
   <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10069.0" MaxVersionTested="10.0.10069.0" />
   </Dependencies>
   ```

4. **Windows ストアのみ:** 要素に子要素を追加する必要があり \<mp:PhoneIdentity> \<Package> ます。 PhoneProductId 属性と PhonePublisherId 属性を追加します。 要素内の Name 属性と同じ値を持つように、"a" の Productid を設定し \<Identity> ます。 PhonePublishedId の値を 00000000-0000-0000-0000-000000000000 に設定します。 以下に例を示します。

   ```xml
   <Identity Name="aa3815a1-2d97-4c71-8c99-578135b28cd8" Publisher="CN=xxxxxxxx" Version="1.0.0.0" />
   <mp:PhoneIdentity PhoneProductId="aa3815a1-2d97-4c71-8c99-578135b28cd8" PhonePublisherId="00000000-0000-0000-0000-000000000000"/>
   ```

5. 要素を検索 \<Prerequisites> し、この要素とその子要素を削除します。

6. **Uap**名前空間を、 \<Resource> Scale、dxfeaturelevel の各要素に追加します。 次に例を示します。

   ```xml
   <Resources>
     <Resource Language="en-us"/>
    <Resource uap:Scale="180"/>
    <Resource uap:DXFeatureLevel="dx11"/>
   </Resources>

   ```

7. **Uap**名前空間を、次の要素に追加し \<Capability> ます。ドキュメント library、picturesLibrary、videosLibrary、MusicLibrary、Enterpriseauthentication、Sharedusercertificates、removablestorage、アポイント、および contacts。 次に例を示します。

   ```xml
   <Capabilities>
     <uap:Capability Name="documentsLibrary"/>
     <uap:Capability Name="removableStorage"/>
   </Capabilities>

   ```

8. **Uap**名前空間を \<VisualElements> 要素とその子要素に追加します。 次に例を示します。

   ```xml
   <uap:VisualElements
       DisplayName="My WWA App"
       Square150x150Logo="images/150x150.png"
       Square44x44Logo="images/44x44.png"
       Description="My WWA App"
       BackgroundColor="#777777">
     <uap:SplashScreen Image="images/splash.png"/>
   </uap:VisualElements>

   ```

    **Windows ストアにのみ適用されます:** タイル サイズの名前が変更されました。 \<VisualElements>新しい収束タイルのサイズを反映するように要素の属性を変更します。 70x70 は 71x71 になり、30x30 は 44x44 になります。

    **OLD:** タイル サイズの名前

   ```xml
   <m2:VisualElements
       …
       Square30x30Logo="Assets\SmallLogo.png"
       …>
    <m2:DefaultTile
         …
         Square70x70Logo="images/70x70.png">
   </m2:VisualElements>

   ```

    **NEW:** タイル サイズの名前

   ```xml
   <uap:VisualElements
       …
       Square44x44Logo="Assets\SmallLogo.png"
       …>
    <uap:DefaultTile
         …
         Square71x71Logo="images/70x70.png">
   </uap:VisualElements>

   ```

9. とそのすべての子要素に **uap** 名前空間を追加し \<ApplicationContentUriRules> ます。 次に例を示します。

    ```xml
    <uap:ApplicationContentUriRules>
      <uap:Rule Type="include" Match="https://www.microsoft.com/"/>
      <uap:Rule Type="exclude" Match="*.pdf"/>
    </uap:ApplicationContentUriRules>

    ```

10. **Uap**名前空間を、次の \<Extension> 要素とそのすべての子要素に追加します。 appointmentsProvider、windows. alarm、cachedFileUpdate、Windows. Autoplaycontent、、cameraSettings、Windows. fileopenpicker、Windows. Fileopenpicker、fileSavePicke、lockScreenCall、printTaskSettings、shareTarget、、、、、、、、のように指定します。 次に例を示します。

    ```xml
    <Extensions>
      <uap:Extension Category="windows.alarm"/>
      <uap:Extension Category="windows.search" EntryPoint="MyActivateableClassId.baz"/>
      <uap:Extension Category="windows.protocol">
        <uap:Protocol Name="mailto" DesiredView="useHalf">
         <uap:DisplayName>MailTo Protocol</uap:DisplayName>
        </uap:Protocol>
      </uap:Extension>
    </Extensions>

    ```

11. **uap** 名前空間をタイプ chatMessageNotification のバックグラウンド タスクに追加します。 次に例を示します。

    ```xml
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">
     <BackgroundTasks ServerName="MyBackgroundTasks">
        <uap:Task Type="chatMessageNotification"/>
      </BackgroundTasks>
    </Extension>

    ```

12. フレームワークの依存関係を変更します。 すべての要素に発行者名を追加 \<PackageDependency> し、まだ指定されていない場合は MinVersion を指定します。

     **古い:** \<PackageDependency> element

    ```xml
    <Dependencies>
     <PackageDependency Name="Microsoft.VCLibs.120.00" />
    </Dependencies>

    ```

     **新規:** \<PackageDependency> element

    ```xml
    <Dependencies>
     <PackageDependency
          Name="Microsoft.VCLibs.120.00"
          Publisher="CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
          MinVersion="12.0.30113.0" />
    </Dependencies>

    ```

     使用している実際のフレームワークのための適切な Publisher 値と MinVersion 値を使用します。 Windows 10 では、これらの名前が変更される可能性があることに注意してください。

13. gattCharacteristicNotification と rfcommConnection バック グラウンド タイプ タスクを Bluetooth タイプ タスクに置き換えます。 次に例を示します。

     **まで**

    ```xml
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">
    <BackgroundTasks ServerName="MyBackgroundTasks">
                <Task Type="rfcommConnection"/>
               <Task Type="gattCharacteristicNotification"/>
    </BackgroundTasks>
    </Extension>
    ```

     **NEW:** Bluetooth タイプ タスクを使用します。

    ```xml
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">
    <BackgroundTasks ServerName="MyBackgroundTasks">
               <Task Type="bluetooth"/>
    </BackgroundTasks>
    </Extension>
    ```

14. Bluetooth デバイス機能の bluetooth.rfcomm と bluetooth.genericAttributeProfile を汎用の Bluetooth 機能に置き換えます。 次に例を示します。

     **まで**

    ```xml
    <Capabilities>
      <m2:DeviceCapability Name="bluetooth.rfcomm">
        <m2:Device Id="any">
         <m2:Function Type="serviceId:34B1CF4D-1069-4AD6-89B6-E161D79BE4D8"/>
        </m2:Device>
      </m2:DeviceCapability>
      <m2:DeviceCapability Name="bluetooth.genericAttributeProfile">
        <m2:Device Id="any">
         <m2:Function Type="name:heartRate"/>
        </m2:Device>
      </m2:DeviceCapability>
    </Capabilities>
    ```

     **NEW:** 汎用の Bluetooth 機能に置き換えられています。

    ```xml
    <Capabilities>
      <uap:DeviceCapability Name="bluetooth"/>
    </Capabilities>

    ```

15. 非推奨の要素を削除します。

    1. これらの属性 \<VisualElements> は非推奨とされ、削除する必要があります。

       - \<VisualElements>属性: ForegroundText、ToastCapable

       - \<DefaultTile>属性 DefaultSize

       - \<ApplicationView> 要素

         次に例を示します。

       ```xml
       <m2:VisualElements
           …
           ForegroundText="dark"
           ToastCapable="true">
       <m2:DefaultTile DefaultSize="square150x150Logo"/>
         <m2:ApplicationView MinWidth="width320"/>
       </m2:VisualElements>

       ```

    2. Windows.contact と windows.contactPicker 拡張子、およびこれらの拡張子の下のすべての要素を削除します。

16. Package.appxmanifest ファイルを保存します。 その後、Visual Studio を閉じます。

17. ソリューションを再度開く前に、いくつかの隠しファイルを削除する必要があります。

    1. ファイル エクスプローラーを開き、ツールバーの **[表示]** をクリックして、 **[非表示項目]** と **[ファイル名拡張子]** を選択します。 コンピューターで次のフォルダーを開きます: \<path for the location of your solution> \\ . vs \\ {Project Name} \ v14。 .suo ファイル拡張子の付いたファイルがある場合は、それを削除します。

    2. ここで、ソリューションが存在するフォルダーに戻ります。 ソリューション内に存在するプロジェクトのフォルダーを開きます。 これらのプロジェクト フォルダー内のファイルに csproj.user または vbproj.user 拡張子がある場合、それを削除します。

         これで、Visual Studio でソリューションを再び開くことができます。 ユニバーサル Windows プラットフォームを使用して、アプリをコーディング、ビルド、およびデバッグする準備ができました。

         ユニバーサル Windows プラットフォームの新機能を活用するように [コードを適合させる方法](https://msdn.microsoft.com/library/windows/apps/dn954974.aspx) について説明します。

## <a name="changes-required-for-existing-universal-windows-apps-created-with-visual-studio-2015-rc"></a><a name="PreviousVersions"></a> Visual Studio 2015 RC で作成された既存のユニバーサル Windows アプリに必要な変更
 Visual Studio 2015 RC で Windows 10 ユニバーサル アプリを作成した場合は、Visual Studio 2015 の最新版のリリースでインストールされたユニバーサル Windows プラットフォームのバージョンを使用するように、プロジェクトを再ターゲットする必要があります。 以前のバージョンはサポートされていません。 必要な変更は、アプリの作成に使用した言語によって異なります。

- [C#/VB アプリ](#RCUpdate10CSharp)

- [C++ アプリ](#RCUpdate10CPlusPlus)

### <a name="update-your-cvb-projects-to-use-the-latest-universal-windows-platform"></a><a name="RCUpdate10CSharp"></a> 最新のユニバーサル Windows プラットフォームを使用するように C#/VB プロジェクトを更新する
 既存のアプリのソリューションを開くと、アプリを更新する必要があることが表示されます。

 ![ソリューション エクスプローラーでプロジェクトを表示](../misc/media/uwp-updaterequired.png "UWP_UpdateRequired")

 ソリューション エクスプローラーからこのプロジェクトを再読み込みすることを選択する場合は、このダイアログ ボックスが表示されます。

 ![アプリを再ターゲットして適切な SDK を使用する](../misc/media/missingsdkforuap.png "MissingSDKforUAP")

 プロジェクトのユニバーサル Windows プラットフォーム SDK は非サポートになりましたので、インストールできません。 単に [OK] をクリックして、以下の手順に従います。

##### <a name="update-your-cvb-projects-to-use-the-latest-universal-windows-platform"></a>最新のユニバーサル Windows プラットフォームを使用するように、C#/VB のプロジェクトを更新する

1. インストールされているユニバーサル Windows プラットフォームを見つけるには、次のフォルダーを開きます: **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 これには、インストールされているユニバーサル Windows プラットフォームごとのフォルダーの一覧が含まれています。 フォルダー名は、インストールされているユニバーサル Windows プラットフォームのバージョンです。 たとえば、この Windows 10 デバイスには、ユニバーサル Windows プラットフォームのバージョン 10.0.10240.0 がインストールされています。

    ![フォルダーを開いてインストールされているバージョンを表示する](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

    ユニバーサル Windows プラットフォームの複数のバージョンをインストールすることができます。 アプリに対応した最新バージョンを使用することをお勧めします。

2. ファイル エクスプローラーを使用して、UWP プロジェクトが保存されているフォルダーに移動します。 ファイルの packages.config を削除し、このフォルダーに新しい .json ファイルを作成します。 ファイルの名前を project.json にして、次の内容をこのファイルに追加します。

   ```json

   {
     "dependencies": {
       "Microsoft.ApplicationInsights": "1.0.0",
       "Microsoft.ApplicationInsights.PersistenceChannel": "1.0.0",
       "Microsoft.ApplicationInsights.WindowsApps": "1.0.0",
       "Microsoft.NETCore.UniversalWindowsPlatform": "5.0.0"
     },
     "frameworks": {
       "uap10.0": {}
     },
     "runtimes": {
       "win10-arm": {},
       "win10-arm-aot": {},
       "win10-x86": {},
       "win10-x86-aot": {},
       "win10-x64": {},
       "win10-x64-aot": {}
     }
   }

   ```

3. Visual Studio を使用して、C#/VB ユニバーサル Windows アプリを含むソリューションを開きます。 プロジェクト ファイル (.csproj または .vbproj ファイル) を更新する必要があることが分かります。 プロジェクト ファイルを右クリックして、このファイルの編集を選択します。

    ![プロジェクトを右クリックし、[編集] をクリックします](../misc/media/uap-editproject.png "UAP_EditProject")

4. \<PropertyGroup>要素と要素を含む要素を検索し \<TargetPlatformVersion> \<TargetPlatformMinVersion> ます。 要素と要素の既存の \<TargetPlatformVersion> 値 \<TargetPlatformMinVersion> を、インストールしたのと同じバージョンのユニバーサル Windows プラットフォームに変更します。

    ユニバーサル Windows アプリの既定のアセット スケールは 200 です。 Visual Studio 2015 RC で作成されたプロジェクトには100でスケーリングされた資産が含まれてい \<UapDefaultAssetScale> ます。この PropertyGroup には、100の値を持つ要素を追加する必要があります。 詳細については、「 [資産とスケール](https://msdn.microsoft.com/library/jj679352.aspx)」を参照してください。

5. UWP 拡張 SDK (例: Windows Mobile SDK) に参照を追加した場合、SDK のバージョンを更新する必要があります。 たとえば、次の要素があるとし \<SDKReference> ます。

   ```xml
   <SDKReference Include="WindowsMobile, Version=10.0.0.1">
         <Name>Microsoft Mobile Extension SDK for Universal App Platform</Name>
   </SDKReference>

   ```

    次のように変更する必要があります。

   ```xml
   <SDKReference Include="WindowsMobile, Version=10.0.10240.0">
         <Name>Microsoft Mobile Extension SDK for Universal App Platform</Name>
   </SDKReference>

   ```

6. \<Target>Namae という値を持つ、name 属性を持つ要素を検索します。 この要素とそのすべての子要素を削除します。

   ```xml
   <Target Name="EnsureNuGetPackageBuildImports" BeforeTargets="PrepareForBuild">
       <PropertyGroup>
         <ErrorText>This project references NuGet package(s) that are missing on this computer. Use NuGet Package Restore to download them.  For more information, see http://go.microsoft.com/fwlink/?LinkID=322105. The missing file is {0}.</ErrorText>
       </PropertyGroup>
       <Error Condition="!Exists('..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets'))" />
       <Error Condition="!Exists('..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets'))" />
   </Target>
   ```

7. 次のように、プロジェクトおよび条件の属性を持つ要素を見つけて削除します。 \<Import> これは、次のようになります。

   ```xml
   <Import Project="..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets" Condition="Exists('..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets')" />
   <Import Project="..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets" Condition="Exists('..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets')" />

   ```

8. \<ItemGroup> \<Reference> NuGet パッケージに子要素を持つを検索します。 この情報は今後のステップに必要なので、参照している NuGet パッケージに注意してください。 Visual Studio 2015 RC と Visual Studio 2015 RTM の間での Windows 10 プロジェクトの形式における 1 つの大きな違いは、RTM の形式では [NuGet](/nuget/) バージョン 3 を使用することです。

    \<ItemGroup>とそのすべての子を削除します。 たとえば、Visual Studio RC で作成された、ある UWP プロジェクトでは次の NuGet パッケージを削除する必要があるかもしれません。

   ```xml
   <ItemGroup>
       <Reference Include="Microsoft.ApplicationInsights, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
         <HintPath>..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.dll</HintPath>
         <Private>True</Private>
       </Reference>
       <Reference Include="Microsoft.ApplicationInsights.Extensibility.Windows, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
         <HintPath>..\packages\Microsoft.ApplicationInsights.WindowsApps.0.14.3-build00177\lib\win81\Microsoft.ApplicationInsights.Extensibility.Windows.dll</HintPath>
         <Private>True</Private>
       </Reference>
       <Reference Include="Microsoft.ApplicationInsights.PersistenceChannel, Version=0.14.3.186, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
         <HintPath>..\packages\Microsoft.ApplicationInsights.PersistenceChannel.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.PersistenceChannel.dll</HintPath>
         <Private>True</Private>
       </Reference>
       <Reference Include="System.Numerics.Vectors, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
         <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.dll</HintPath>
         <Private>True</Private>
       </Reference>
       <Reference Include="System.Numerics.Vectors.WindowsRuntime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
         <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.WindowsRuntime.dll</HintPath>
         <Private>True</Private>
       </Reference>
     </ItemGroup>

   ```

9. 要素を \<ItemGroup> 含む要素を検索 \<AppxManifest> します。 \<None>Include 属性を packages.config に設定した要素がある場合は、それを削除します。 また、 \<None> Include 属性を持つ要素を追加し、その値を project.jsに設定します。

10. 変更を保存します。 その後、プロジェクト ファイルを閉じます。

11. ソリューション エクスプローラーでプロジェクト ファイルを右クリックし、コンテキスト メニューの [プロジェクトの再読み込み] をクリックします。 これで、プロジェクト内のすべてのファイルがソリューション エクスプローラーに表示されます。

12. ソリューション エクスプローラーで、ApplicationInsights.config のファイルを選択し、そのプロパティを開きます。 "ビルド アクション" プロパティを "コンテンツ" に変更し、"出力ディレクトリにコピー" プロパティを "新しい場合はコピーする" に変更します。

13. プロジェクトの Package.appxmanifest ファイルを開きます。

    1. \<TargetDeviceFamily> 要素を検索します。 MinVersion と MaxVersionTested 属性を変更して、インストールしたユニバーサル Windows プラットフォームのバージョンに対応させます。 以下に例を示します。

        ```xml
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10240.0" />
        ```

    2. 変更を保存します。

14. 前の手順で削除したパッケージを追加するには、NuGet マネージャーを使用します。 Visual Studio 2015 RC と Visual Studio 2015 RTM の間での Windows 10 プロジェクトの形式における 1 つの大きな違いは、RTM の形式では [NuGet](/nuget/) バージョン 3 を使用することです。

    これで、アプリをコーディング、ビルド、およびデバッグすることができます。

    ユニバーサル Windows アプリの単体テスト プロジェクトがある場合は、 [これらの手順](#MigrateUnitTest)も行う必要があります。

### <a name="update-your-c-projects-to-use-the-latest-universal-windows-platform"></a><a name="RCUpdate10CPlusPlus"></a> 最新のユニバーサル Windows プラットフォームを使用するように C++ プロジェクトを更新する

1. インストールされているユニバーサル Windows プラットフォームを見つけるには、次のフォルダーを開きます: **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 これには、インストールされているユニバーサル Windows プラットフォームごとのフォルダーの一覧が含まれています。 フォルダー名は、インストールされているユニバーサル Windows プラットフォームのバージョンです。 たとえば、この Windows 10 デバイスには、ユニバーサル Windows プラットフォームのバージョン 10.0.10240.0 がインストールされています。

     ![フォルダーを開いてインストールされているバージョンを表示する](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

     ユニバーサル Windows プラットフォームの複数のバージョンをインストールすることができます。 アプリに対応した最新バージョンを使用することをお勧めします。

2. C++ Windows ユニバーサル アプリを含むソリューションを開きます。 プロジェクト .vcxproj ファイルを右クリックして、プロジェクト ファイルのアンロードを選択します。 プロジェクトをアンロードした後、プロジェクト ファイルを再度右クリックして、その編集を選択します。

     ![プロジェクトをアンロードし、プロジェクト ファイルを編集する](../misc/media/uap-editearliercplus.png "UAP_EditEarlierCPlus")

3. \<PropertyGroup>Condition 属性を含まないが、要素を含む要素を検索 \<ApplicationTypeRevision> します。 ApplicationTypeRevision の値を 8.2 から 10.0 に更新します。 \<WindowsTargetPlatformVersion>と要素を追加 \<WindowsTargetPlatformMinVersion> し、その値を、インストールしたユニバーサル Windows プラットフォームバージョンの値に設定します。

     要素を追加 \<EnableDotNetNativeCompatibleProfile> し、その値を true に設定します (要素がまだ存在しない場合)。

     ユニバーサル Windows アプリの既定のアセット スケールは 200 です。 Visual Studio 2015 RC で作成されたプロジェクトには100でスケーリングされた資産が含まれてい \<UapDefaultAssetScale> ます。この PropertyGroup には、100の値を持つ要素を追加する必要があります。 詳細については、「 [資産とスケール](https://msdn.microsoft.com/library/jj679352.aspx)」を参照してください。

     この \<PropertyGroup> 要素は次のようになります。

    ```xml
    <PropertyGroup Label="Globals">
        …
        <MinimumVisualStudioVersion>14.0</MinimumVisualStudioVersion>
        <ApplicationType>Windows Store</ApplicationType>
        <ApplicationTypeRevision>10.0</ApplicationTypeRevision>
        <WindowsTargetPlatformVersion>10.0.10240.0</WindowsTargetPlatformVersion>
        <WindowsTargetPlatformMinVersion>10.0.10240.0</WindowsTargetPlatformMinVersion>
        <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>
        <UapDefaultAssetScale>100</UapDefaultAssetScale>
      </PropertyGroup>

    ```

4. 残りの各要素について \<PropertyGroup> 、要素にリリース構成の Condition 属性があるかどうかを確認します。 含まれているが、要素が含まれていない場合は、それを \<UseDotNetNativeToolchain> 追加します。 次のように、要素の値を \<UseDotNetNativeToolchain> true に設定します。

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'" Label="Configuration">
        <ConfigurationType>Application</ConfigurationType>
        <UseDebugLibraries>false</UseDebugLibraries>
        <WholeProgramOptimization>true</WholeProgramOptimization>
        <PlatformToolset>v140</PlatformToolset>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>

    ```

5. 要素と要素を更新して .NET ネイティブを有効にする必要があり \<EnableDotNetNativeCompatibleProfile> \<UseDotNetNativeToolchain> ますが、C++ テンプレートで .NET ネイティブが有効になっていません。

     変更を保存します。 その後、プロジェクト ファイルを閉じます。

6. ソリューション エクスプローラーでプロジェクト ファイルを右クリックし、コンテキスト メニューの [プロジェクトの再読み込み] をクリックします。 これで、プロジェクト内のすべてのファイルがソリューション エクスプローラーに表示されます。

7. プロジェクトの Package.appxmanifest ファイルを開きます。

    1. \<TargetDeviceFamily> 要素を検索します。 MinVersion と MaxVersionTested 属性を変更して、インストールしたユニバーサル Windows プラットフォームのバージョンに対応させます。 以下に例を示します。

        ```xml
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10240.0" />
        ```

    2. 変更を保存します。

         これで、アプリをコーディング、ビルド、およびデバッグすることができます。

         ユニバーサル Windows アプリの単体テスト プロジェクトがある場合は、 [これらの手順](#MigrateUnitTest)も行う必要があります。

## <a name="changes-required-for-existing-unit-test-projects-for-universal-windows-apps-created-with-visual-studio-2015-rc"></a><a name="MigrateUnitTest"></a> Visual Studio 2015 RC で作成されたユニバーサル Windows アプリの既存の単体テストプロジェクトに必要な変更
 Visual Studio 2015 RC で Windows 10 ユニバーサル アプリの単体テスト プロジェクトを作成した場合、これらの追加の変更をプロジェクト ファイルに行い、Visual Studio 2015 の最新版のリリースでこれらのテスト プロジェクトを使用するようにしなければなりません。 必要な変更は、アプリの作成に使用した言語によって異なります。

- [C#/VB アプリ](#UnitTestRCUpdate10CSharp)

- [C++ アプリ](#UnitTestRCUpdate10CPlusPlus)

### <a name="update-your-cvb-unit-test-projects"></a><a name="UnitTestRCUpdate10CSharp"></a> C#/VB 単体テストプロジェクトを更新する

1. Visual Studio を使用して、C#/VB 単体テスト プロジェクトを含むソリューションを開きます。 要素の値 \<OuttputType> を AppContainerExe に変更します。

   ```xml

   <OutputType>AppContainerExe</OutputType>

   ```

2. この要素 \<EnableCoreRuntime> の false \</EnableCoreRuntime> を次の要素に置き換えます。

   ```xml

   <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>

   ```

3. 次の行を削除します。

   ```xml

   <PropertyGroup>
       <AppXPackage>True</AppXPackage>
       <AppxPackageIncludePrivateSymbols>true</AppxPackageIncludePrivateSymbols>
    </PropertyGroup>
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
    <PlatformTarget>AnyCPU</PlatformTarget>
    <DebugSymbols>true</DebugSymbols>
    <DebugType>full</DebugType>
    <Optimize>false</Optimize>
    <OutputPath>bin\Debug\</OutputPath>
    <DefineConstants>DEBUG;TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
    </PropertyGroup>
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
       <PlatformTarget>AnyCPU</PlatformTarget>
       <DebugType>pdbonly</DebugType>
       <Optimize>true</Optimize>
       <OutputPath>bin\Release\</OutputPath>
       <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
       <ErrorReport>prompt</ErrorReport>
       <WarningLevel>4</WarningLevel>
    </PropertyGroup>

   ```

4. 次の要素 \<UseDotNetNativeToolchain> を \</UseDotNetNativeToolchain> 子要素としてこれらのプロパティグループに追加します。

   ```xml

   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|ARM'">
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|X86'">
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|X64'">

   ```

5. 次の要素を削除し \<ItemGroup> ます。

   ```xml

   <ItemGroup>
      <Compile Include="Properties\AssemblyInfo.cs" />
      <Compile Include="UnitTest.cs" />
   </ItemGroup>
   <ItemGroup>
      <AppxManifest Include="Package.appxmanifest">
         <SubType>Designer</SubType>
      </AppxManifest>
      <None Include="packages.config" />
      <None Include="UnitTestProject1_TemporaryKey.pfx" />
   </ItemGroup>
   <ItemGroup>
      <Content Include="Properties\Default.rd.xml" />
      <Content Include="Assets\Logo.scale-240.png" />
      <Content Include="Assets\SmallLogo.scale-240.png" />
      <Content Include="Assets\SplashScreen.scale-240.png" />
      <Content Include="Assets\Square71x71Logo.scale-240.png" />
      <Content Include="Assets\StoreLogo.scale-240.png" />
      <Content Include="Assets\WideLogo.scale-240.png" />
   </ItemGroup>

   ```

    これらの要素に置き換えます。

   ```xml

   <ItemGroup>
      <Compile Include="Properties\AssemblyInfo.cs" />
      <Compile Include="UnitTestApp.xaml.cs">
         <DependentUpon>UnitTestApp.xaml</DependentUpon>
      </Compile>
      <Compile Include="UnitTest.cs" />
   </ItemGroup>
   <ItemGroup>
      <ApplicationDefinition Include="UnitTestApp.xaml">
         <Generator>MSBuild:Compile</Generator>
         <SubType>Designer</SubType>
      </ApplicationDefinition>
   </ItemGroup>
   <ItemGroup>
      <AppxManifest Include="Package.appxmanifest">
         <SubType>Designer</SubType>
      </AppxManifest>
      <None Include="UnitTestProject1_TemporaryKey.pfx" />
   </ItemGroup>
   <ItemGroup>
      <Content Include="Properties\UnitTestApp.rd.xml" />
      <Content Include="Assets\LockScreenLogo.scale-200.png" />
      <Content Include="Assets\SplashScreen.scale-200.png" />
      <Content Include="Assets\Square150x150Logo.scale-200.png" />
      <Content Include="Assets\Square44x44Logo.scale-200.png" />
      <Content Include="Assets\Square44x44Logo.targetsize-24_altform-unplated.png" />
      <Content Include="Assets\StoreLogo.png" />
      <Content Include="Assets\Wide310x150Logo.scale-200.png" />
   </ItemGroup>
   ```

6. 新しい単体テスト プロジェクトを作成し、UnitTestApp.xaml と UnitTestApp.xaml.cs ファイルをその新規のプロジェクトから、更新している既存の単体テスト プロジェクトにコピーします。

7. UnitTestApp.rd.xml ファイルを新しい単体テスト プロジェクトのプロパティ フォルダーから、更新している既存の単体テスト プロジェクトのプロパティ フォルダーにコピーします。

8. プロジェクトの Package.appxmanifest ファイルを開きます。 次に、これらの要素を以下から削除します。

   ```xml

   <Applications>
      <Application Id="vstest.executionengine.universal.App"
            Executable="vstest.executionengine.appcontainer.uap.exe"
            EntryPoint="Microsoft.VisualStudio.TestPlatform.TestExecutor.AppContainer.App">
         <uap:VisualElements
            DisplayName="UnitTestProject1"
            Square150x150Logo="Assets\Logo.png"
            Square44x44Logo="Assets\SmallLogo.png"
            Description="UnitTestProject1"
            BackgroundColor="#464646">
            <uap:SplashScreen Image="Assets\SplashScreen.png" />
         </uap:VisualElements>
      </Application>
   </Applications>
   <Capabilities>
      <Capability Name="internetClientServer" />
   </Capabilities>
   ```

    これらの削除された要素を次の要素に置き換えます。 ProjectName の値として、以下の要素の UnitTestProject1 ではなく、プロジェクトの名前に基づく適切な値を使用します。

   ```xml

   <Applications>
      <Application Id="vstest.executionengine.universal.App"
            Executable="$targetnametoken$.exe"
            EntryPoint="UnitTestProject1.App">
         <uap:VisualElements
               DisplayName="UnitTestProject1"
               Square150x150Logo="Assets\Square150x150Logo.png"
               Square44x44Logo="Assets\Square44x44Logo.png"
               Description="UnitTestProject1"
               BackgroundColor="transparent">
            <uap:DefaultTile Wide310x150Logo="Assets\Wide310x150Logo.png"/>
            <uap:SplashScreen Image="Assets\SplashScreen.png" />
         </uap:VisualElements>
      </Application>
   </Applications>
   <Capabilities>
      <Capability Name="internetClient" />
   </Capabilities>
   ```

   これで単体テストを実行できます。

### <a name="update-your-c-projects-to-use-the-latest-universal-windows-platform"></a><a name="UnitTestRCUpdate10CPlusPlus"></a> 最新のユニバーサル Windows プラットフォームを使用するように C++ プロジェクトを更新する

1. Visual Studio を使用して、C++ 単体テスト プロジェクトを含むソリューションを開きます。 次の要素を削除します。

    ```xml

    <TestApplication>true</TestApplication>
    <AppxPackage>True</AppxPackage>
    <CppWindowsStoreUnitTestLibraryType>true</CppWindowsStoreUnitTestLibraryType>
    <EnableCoreRuntime>false</EnableCoreRuntime>

    ```

2. この \<ProjectConfiguration> \<ItemGroup Label="ProjectConfigurations"> メンバーがまだこの fille にない場合は、次の要素をこの要素の下に追加します。

    ```xml

    <ProjectConfiguration Include="Debug|x64">
       <Configuration>Debug</Configuration>
       <Platform>x64</Platform>
    </ProjectConfiguration>
    <ProjectConfiguration Include="Release|x64">
       <Configuration>Release</Configuration>
       <Platform>x64</Platform>
    </ProjectConfiguration>

    ```

3. この要素のすべての出現箇所を置き換えます。

    ```xml

    <ConfigurationType>DynamicLibrary</ConfigurationType>

    ```

     以下に置き換えます。

    ```xml

    <ConfigurationType>Application</ConfigurationType>

    ```

4. \<PropertyGroup>ファイルにまだ含まれていない場合は、次の要素を追加します。

    ```xml

    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'" Label="Configuration">
       <ConfigurationType>Application</ConfigurationType>
       <UseDebugLibraries>true</UseDebugLibraries>
       <PlatformToolset>v140</PlatformToolset>
    </PropertyGroup>
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'" Label="Configuration">
       <ConfigurationType>Application</ConfigurationType>
       <UseDebugLibraries>false</UseDebugLibraries>
       <WholeProgramOptimization>true</WholeProgramOptimization>
       <PlatformToolset>v140</PlatformToolset>
       <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
    </PropertyGroup>

    ```

5. この要素のすべての出現箇所を置き換えます。

    ```xml

    <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>
    ```

     以下に置き換えます。

    ```xml

    <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>

    ```

6. この要素のすべての出現箇所を置き換えます。

    ```xml

    <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\Lib;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>

    ```

     以下に置き換えます。

    ```xml

    <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>

    ```

7. \<ItemDefinitionGroup>既に他の要素が含まれているセクションに、これらの要素を追加し \<ItemDefinitionGroup> ます。

    ```xml

    <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'">
       <ClCompile>
          <AdditionalOptions>/bigobj %(AdditionalOptions)</AdditionalOptions>
          <DisableSpecificWarnings>4453;28204</DisableSpecificWarnings>
          <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%     (AdditionalIncludeDirectories)</AdditionalIncludeDirectories>
       </ClCompile>
    <Link>
       <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>
    </Link>
    </ItemDefinitionGroup>
    <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'">
       <ClCompile>
          <AdditionalOptions>/bigobj %(AdditionalOptions)</AdditionalOptions>
          <DisableSpecificWarnings>4453;28204</DisableSpecificWarnings>
          <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>
       </ClCompile>
       <Link>
          <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>
       </Link>
    </ItemDefinitionGroup>

    ```

8. 次の要素を削除し \< ItemGroup> ます。

    ```xml

    <ItemGroup>
       <Image Include="Assets\Logo.scale-100.png" />
       <Image Include="Assets\SmallLogo.scale-100.png" />
       <Image Include="Assets\StoreLogo.scale-100.png" />
       <Image Include="Assets\SplashScreen.scale-100.png" />
       <Image Include="Assets\WideLogo.scale-100.png" />
    </ItemGroup>

    ```

     次の要素で置き換え \<ItemGroup> ます。

    ```xml

    <ItemGroup>
       <Image Include="Assets\LockScreenLogo.scale-200.png" />
       <Image Include="Assets\SplashScreen.scale-200.png" />
       <Image Include="Assets\Square44x44Logo.scale-200.png" />
       <Image Include="Assets\Square44x44Logo.targetsize-24_altform-unplated.png" />
       <Image Include="Assets\Square150x150Logo.scale-200.png" />
       <Image Include="Assets\StoreLogo.png" />
       <Image Include="Assets\Wide310x150Logo.scale-200.png" />
    </ItemGroup>

    ```

9. 次の要素を削除し \< ItemGroup> ます。

    ```xml

    <ItemGroup>
       <ClInclude Include="pch.h" />
    </ItemGroup>
    ```

     次の要素に置き換え \<ItemGroup> ます。

    ```xml

    <ItemGroup>
       <ClInclude Include="pch.h" />
       <ClInclude Include="UnitTestApp.xaml.h">
          <DependentUpon>UnitTestApp.xaml</DependentUpon>
       </ClInclude>
    </ItemGroup>
    <ItemGroup>
       <ApplicationDefinition Include="UnitTestApp.xaml">
          <SubType>Designer</SubType>
       </ApplicationDefinition>
    </ItemGroup>

    ```

10. 次の要素を削除します。

    ```xml
    <ClCompile Include="UnitTest.cpp"/>
    ```

     次の要素に置き換え \<CICompile> ます。

    ```xml

    <ClCompile Include="UnitTestApp.xaml.cpp">
       <DependentUpon>UnitTestApp.xaml</DependentUpon>
    </ClCompile>
    <ClCompile Include="UnitTest.cpp"/>

    ```

11. この要素を追加します。

    ```xml
    <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
    ```

     ファイル内のこの要素の上に追加します。

    ```xml

    <ItemGroup>
       <Xml Include="UnitTestApp.rd.xml" />
    </ItemGroup>
    ```

12. 新しい単体テスト C++ プロジェクトを作成し、そのプロジェクトから更新中の既存の単体テスト プロジェクトに UnitTestApp.xaml、UnitTestApp.xaml.cpp、UnitTestApp.xaml.h、および UnitTestApp.rd.xml ファイルをコピーします。

13. プロジェクトの Package.appxmanifest ファイルを開きます。 次に、これらの要素を以下から削除します。

    ```xml

    <Applications>
       <Application Id="vstest.executionengine.universal.App"
             Executable="vstest.executionengine.appcontainer.uap.exe"
             EntryPoint="Microsoft.VisualStudio.TestPlatform.TestExecutor.AppContainer.App">
          <uap:VisualElements
             DisplayName="UnitTestProject1"
             Square150x150Logo="Assets\Logo.png"
             Square44x44Logo="Assets\SmallLogo.png"
             Description="UnitTestProject1"
             BackgroundColor="#464646">
             <uap:SplashScreen Image="Assets\SplashScreen.png" />
          </uap:VisualElements>
       </Application>
    </Applications>
    <Capabilities>
       <Capability Name="internetClientServer" />
    </Capabilities>

    ```

     これらの削除された要素を次の要素に置き換えます。 ProjectName の値として、以下の要素の UnitTestProject1 ではなく、プロジェクトの名前に基づく適切な値を使用します。

    ```xml

    <Applications>
       <Application Id="vstest.executionengine.universal.App"
                Executable="$targetnametoken$.exe"
                EntryPoint="UnitTestProject1.App">
          <uap:VisualElements
                DisplayName="UnitTestProject1"
                Square150x150Logo="Assets\Square150x150Logo.png"
                Square44x44Logo="Assets\Square44x44Logo.png"
                Description="UnitTestProject1"
                BackgroundColor="transparent">
                <uap:DefaultTile Wide310x150Logo="Assets\Wide310x150Logo.png"/>
                <uap:SplashScreen Image="Assets\SplashScreen.png" />
          </uap:VisualElements>
       </Application>
    </Applications>
    <Capabilities>
       <Capability Name="internetClient" />
    </Capabilities>

    ```