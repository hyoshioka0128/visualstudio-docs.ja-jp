---
title: ソフトウェア開発キットを作成する |Microsoft Docs
description: Sdk の一般的なインフラストラクチャと、プラットフォーム SDK と拡張 SDK の作成方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8496afb4-1573-4585-ac67-c3d58b568a12
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b3a793e3d7233eb1b6d0aaaa74fbe16d52cf6f43
ms.sourcegitcommit: 5027eb5c95e1d2da6d08d208fd6883819ef52d05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94974331"
---
# <a name="create-a-software-development-kit"></a>ソフトウェア開発キットを作成する

ソフトウェア開発キット (SDK) は、Visual Studio で1つの項目として参照できる Api のコレクションです。 [ **参照マネージャー** ] ダイアログボックスには、プロジェクトに関連するすべての sdk が一覧表示されます。 SDK をプロジェクトに追加すると、Visual Studio で Api を使用できるようになります。

Sdk には、次の2種類があります。

- プラットフォーム Sdk は、プラットフォーム用のアプリを開発するための必須コンポーネントです。 たとえば、SDK は、 [!INCLUDE[win81](../debugger/includes/win81_md.md)] アプリを開発するために必要です [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 。

- 拡張 Sdk は、プラットフォームを拡張するオプションのコンポーネントですが、そのプラットフォーム用のアプリを開発する場合には必須ではありません。

以下のセクションでは、Sdk の一般的なインフラストラクチャと、プラットフォーム SDK と拡張 SDK を作成する方法について説明します。

## <a name="platform-sdks"></a>プラットフォーム SDK

プラットフォーム用のアプリを開発するには、プラットフォーム Sdk が必要です。 たとえば、 [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK は、用のアプリを開発するために必要です [!INCLUDE[win81](../debugger/includes/win81_md.md)] 。

### <a name="installation"></a>インストール

すべてのプラットフォーム Sdk は、 *HKLM\Software\Microsoft\Microsoft sdk \\ [tpi] \ v [tpi] \\ @InstallationFolder = [SDK root]* にインストールされます。 これにより、 [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK は *HKLM\Software\Microsoft\Microsoft SDKs\Windows\v8.1* にインストールされます。

### <a name="layout"></a>Layout

プラットフォーム Sdk には次のレイアウトがあります。

```
\[InstallationFolder root]
            SDKManifest.xml
            \References
                  \[config]
                        \[arch]
            \DesignTime
                  \[config]
                        \[arch]
```

| ノード | 説明 |
|------------------------| - |
| *参照* フォルダー | コーディング可能な Api を含むバイナリが含まれています。 これには、Windows メタデータ (WinMD) ファイルまたはアセンブリを含めることができます。 |
| *デザイン時* フォルダー | 実行前またはデバッグ時にのみ必要なファイルが含まれています。 これには、XML ドキュメント、ライブラリ、ヘッダー、ツールボックスのデザイン時バイナリ、MSBuild 成果物などが含まれます。<br /><br /> XML ドキュメントは *\designtime どちら* フォルダーに配置するのが理想的ですが、参照用の xml ドキュメントは引き続き Visual Studio の参照ファイルと共に配置されます。 たとえば、参照用の XML ドキュメントである [config] [arch]<em> \\ \\ \sample.dll</em> は、 *\\ [config \\*] [arch] \sample.xmlと参照され、そのドキュメントのローカライズ版は [ *\\ config] \\ [arch] \\ [locale] \sample.xml* になります。 |
| *構成* フォルダー | フォルダーは、 *Debug*、 *Retail* 、および *commonconfiguration* の3つだけです。 Sdk の作成者は、sdk のコンシューマーが対象とする構成に関係なく、同じ一連の SDK ファイルを使用する必要がある場合に、それらのファイルを *Commonconfiguration* の下に配置できます。 |
| *アーキテクチャ* フォルダー | サポートされている *アーキテクチャ* フォルダーが存在していてもかまいません。 Visual Studio では、x86、x64、ARM、およびニュートラルアーキテクチャがサポートされています。 注: Win32 は x86 にマップされ、AnyCPU はニュートラルにマップされます。<br /><br /> MSBuild は、プラットフォーム Sdk の *\CommonConfiguration\neutral* の下でのみ参照できます。 |
| *SDKManifest.xml* | このファイルでは、Visual Studio が SDK をどのように使用するかを説明します。 の SDK マニフェストを確認し [!INCLUDE[win81](../debugger/includes/win81_md.md)] ます。<br /><br /> `<FileList             DisplayName = "Windows"             PlatformIdentity = "Windows, version=8.1"             TargetFramework = ".NET for Windows Store apps, version=v4.5.1; .NET Framework, version=v4.5.1"             MinVSVersion = "14.0">              <File Reference = "Windows.winmd">                <ToolboxItems VSCategory = "Toolbox.Default" />             </File> </FileList>`<br /><br /> **DisplayName:** オブジェクトブラウザーが参照一覧に表示する値。<br /><br /> **Platformidentity:** この属性が存在することは、SDK が platform SDK であること、およびその SDK から追加された参照をローカルにコピーできないことを Visual Studio と MSBuild に通知します。<br /><br /> **Targetframework:** この属性は、この属性の値に指定されているものと同じフレームワークを対象とするプロジェクトだけが SDK を使用できるようにするために、Visual Studio によって使用されます。<br /><br /> **Minvsversion:** この属性は、それに適用される Sdk のみを使用するために Visual Studio によって使用されます。<br /><br /> **参照:** この属性は、コントロールを含む参照に対してのみ指定する必要があります。 参照にコントロールが含まれているかどうかを指定する方法については、以下を参照してください。 |

## <a name="extension-sdks"></a>拡張 SDK

以下のセクションでは、拡張機能 SDK をデプロイするために必要な作業について説明します。

### <a name="installation"></a>インストール

拡張 Sdk は、レジストリキーを指定せずに、特定のユーザーまたはすべてのユーザーに対してインストールできます。 すべてのユーザーに対して SDK をインストールするには、次のパスを使用します。

*% Program Files%\Microsoft Sdk- \<target platform\> v<プラットフォームのバージョン番号/ \> extensionsdk*

ユーザー固有のインストールの場合は、次のパスを使用します。

*%USERPROFILE%\AppData\Local\Microsoft Sdk- \<target platform\> v<プラットフォームのバージョン番号/ \> extensionsdk*

別の場所を使用する場合は、次の2つのいずれかを実行する必要があります。

1. レジストリキーで指定します。

     **HKLM\Software\Microsoft\Microsoft Sdk- \<target platform> v<プラットフォームのバージョン番号/ \> extensionsdk\<SDKName>\<SDKVersion>**\

     との値を持つ (既定の) サブキーを追加し `<path to SDK><SDKName><SDKVersion>` ます。

2. MSBuild プロパティ `SDKReferenceDirectoryRoot` をプロジェクトファイルに追加します。 このプロパティの値は、参照する拡張 Sdk が存在するディレクトリのセミコロン区切りの一覧です。

### <a name="installation-layout"></a>インストールレイアウト

拡張 Sdk には次のインストールレイアウトがあります。

```
\<ExtensionSDKs root>
           \<SDKName>
                 \<SDKVersion>
                        SDKManifest.xml
                        \References
                              \<config>
                                    \<arch>
                        \Redist
                              \<config>
                                    \<arch>
                        \DesignTime
                               \<config>
                                     \<arch>

```

1. \\<SDKName \> \\<SDKVersion \> : 拡張 sdk の名前とバージョンは、sdk ルートへのパス内の対応するフォルダー名から派生します。 MSBuild はこの id を使用してディスク上の SDK を検索し、Visual Studio は [ **プロパティ** ] ウィンドウと [ **参照マネージャー** ] ダイアログボックスにこの id を表示します。

2. *References* フォルダー: api を含むバイナリ。 これは、Windows メタデータ (WinMD) ファイルまたはアセンブリである可能性があります。

3. *Redist* フォルダー: ランタイム/デバッグに必要なファイルは、ユーザーのアプリケーションの一部としてパッケージ化される必要があります。 すべてのバイナリは、 *\\<config \> \\<arch \>* の下に配置する必要があります。また、このバイナリ名は、一意性を確保するために次の形式にする必要があります。 *]* \<company> . \<product> \<purpose> \<extension> ..<em>.たとえば、* Microsoft.Cpp.Build.dllのように</em>なります。 他の Sdk のファイル名と競合する可能性のある名前を持つすべてのファイル (javascript、css、pri、xaml、png、jpg ファイルなど) は、sdkname config<arch<の<下に配置する必要があり<em> \\ ます ( \> \\ \> \\ \> \* xaml コントロールに関連付けられているファイルを除く)。これらのファイルは、* \ redist \\<config \> \\<arch \> \\<componentname \> \\ の下に配置する必要があり</em>ます。

4. *デザイン時* folder: 実行前またはデバッグ時にのみ必要なファイルで、ユーザーのアプリケーションの一部としてパッケージ化することはできません。 これには、XML ドキュメント、ライブラリ、ヘッダー、ツールボックスのデザイン時バイナリ、MSBuild 成果物などがあります。 ネイティブプロジェクトでの使用を目的とした SDK には、 *SDKName* ファイルが含まれている必要があります。 この種類のファイルの例を次に示します。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <PropertyGroup>
       <ExecutablePath>C:\Temp\ExecutablePath;$(ExecutablePath)</ExecutablePath>
       <IncludePath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\CommonConfiguration\Neutral\include;$(IncludePath)</IncludePath>
       <AssemblyReferencePath>C:\Temp\AssemblyReferencePath;(AssemblyReferencePath)</AssemblyReferencePath>
       <LibraryPath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\Debug\ARM;$(LibraryPath)</LibraryPath>
       <SourcePath>C:\Temp\SourcePath\X64;$(SourcePath)</SourcePath>
       <ExcludePath>C:\Temp\ExcludePath\X64;$(ExcludePath)</ExcludePath>
       <_PropertySheetDisplayName>DevILSDK, 1.0</_PropertySheetDisplayName>
     </PropertyGroup>
   </Project>

   ```

    XML 参照ドキュメントは、参照ファイルと共に配置されます。 たとえば、 *\ references \\<config \> \\<arch \>\sample.dll* assembly の XML リファレンスドキュメントは *\ 参照 \\<config \> \\<arch \>\sample.xml*、そのドキュメントのローカライズされたバージョンは *\ 参照<config<<\\ \> \\ \> \\ \>\sample.xmllocale* です。

5. *構成* フォルダー: *Debug*、 *Retail*、および *commonconfiguration* という3つのサブフォルダー。 Sdk の作成者は、sdk のコンシューマーが対象とする構成に関係なく、同じ一連の SDK ファイルを使用する必要がある場合に、 *Commonconfiguration* の下にファイルを配置できます。

6. *アーキテクチャ* フォルダー: x86、X64、ARM、ニュートラルの各アーキテクチャがサポートされています。 Win32 は x86 にマップされ、AnyCPU はニュートラルにマップされます。

### <a name="sdkmanifestxml"></a>SDKManifest.xml

*SDKManifest.xml* ファイルでは、Visual STUDIO が SDK をどのように使用するかを説明します。 次に例を示します。

```
<FileList>
DisplayName = "My SDK"
ProductFamilyName = "My SDKs"
TargetFramework = ".NETCore, version=v4.5.1; .NETFramework, version=v4.5.1"
MinVSVersion = "14.0"
MaxPlatformVersion = "8.1"
AppliesTo = "WindowsAppContainer + WindowsXAML"
SupportPrefer32Bit = "True"
SupportedArchitectures = "x86;x64;ARM"
SupportsMultipleVersions = "Error"
CopyRedistToSubDirectory = "."
DependsOn = "SDKB, version=2.0"
MoreInfo = "https://msdn.microsoft.com/MySDK">
<File Reference = "MySDK.Sprint.winmd" Implementation = "XNASprintImpl.dll">
<Registration Type = "Flipper" Implementation = "XNASprintFlipperImpl.dll" />
<Registration Type = "Flexer" Implementation = "XNASprintFlexerImpl.dll" />
<ToolboxItems VSCategory = "Toolbox.Default" />
</File>
</FileList>
```

次の一覧は、ファイルの要素を示しています。

1. DisplayName: Visual Studio のユーザーインターフェイスの参照マネージャー、ソリューションエクスプローラー、オブジェクトブラウザー、およびその他の場所に表示される値。

2. ProductFamilyName: SDK 製品の全体的な名前。 たとえば、sdk に [!INCLUDE[winjs_long](../debugger/includes/winjs_long_md.md)] は、"WinJS" と "WinJS" という名前が付けられています。これは、sdk 製品ファミリ "WinJS" の同じファミリに属しています。 この属性は、Visual Studio と MSBuild がその接続を行うことを許可します。 この属性が存在しない場合は、SDK 名が製品ファミリ名として使用されます。

3. FrameworkIdentity: 1 つ以上の Windows コンポーネントライブラリに対する依存関係を指定します。 この属性の値は、コンシューマー側アプリのマニフェストに格納されます。 この属性は、Windows コンポーネントライブラリにのみ適用できます。

4. TargetFramework: 参照マネージャーとツールボックスで使用できる Sdk を指定します。 これは、ターゲットフレームワークモニカーのセミコロン区切りの一覧です。たとえば、".NET Framework, version = v2.0; .NET Framework, version = v1.0" のようになります。 同じターゲットフレームワークの複数のバージョンが指定されている場合、参照マネージャーは、フィルター処理のために指定された最も低いバージョンを使用します。 たとえば、".NET Framework, version = v2.0; .NET Framework, version = v1.0" が指定されている場合、参照マネージャーは ".NET Framework, version = v2.0" を使用します。 特定のターゲットフレームワークプロファイルが指定されている場合、そのプロファイルだけが、フィルター処理のために参照マネージャーによって使用されます。 たとえば、"Silverlight, version = v4.0, profile = Appname.windowsphone" を指定した場合、参照マネージャーは、Windows Phone プロファイルのみをフィルター処理します。完全な Silverlight 4.0 フレームワークを対象とするプロジェクトでは、参照マネージャーで SDK が表示されません。

5. MinVSVersion: Visual Studio の最小バージョン。

6. MaxPlatformVerson: 拡張機能 SDK が動作しないプラットフォームのバージョンを指定するには、ターゲットプラットフォームの最大バージョンを使用する必要があります。 たとえば、Microsoft Visual C++ ランタイムパッケージ v1.0 は、Windows 8 プロジェクトでのみ参照する必要があります。 このため、Windows 8 プロジェクトの MaxPlatformVersion は8.0 です。 これは、参照マネージャーが Windows 8.1 プロジェクトのランタイムパッケージをフィルターで Microsoft Visual C++ 除外することを意味し、MSBuild がプロジェクトを参照したときに MSBuild がエラーをスローすることを意味し [!INCLUDE[win81](../debugger/includes/win81_md.md)] ます。 注: この要素は以降でサポートされてい [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] ます。

7. AppliesTo: 適用可能な Visual Studio プロジェクトの種類を指定して、参照マネージャーで使用できる Sdk を指定します。 Windows では、WindowsAppContainer、VisualC、VB、CSharp、Windowsappcontainer、JavaScript、Managed、および Native の9つの値が認識されます。 SDK の作成者は and ("+") または ("&#124;") を使用できますが、("!") は使用できません。SDK に適用されるプロジェクトの種類のスコープを厳密に指定する演算子。

    WindowsAppContainer は、アプリのプロジェクトを識別 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] します。

8. SupportPrefer32Bit: サポートされている値は "True" と "False" です。 既定値は "True" です。 値が "False" に設定されている場合、SDK を参照している [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] プロジェクトで Prefer32Bit が有効になっている場合、MSBuild はプロジェクト (またはデスクトッププロジェクトの警告) のエラーを返します。 Prefer32Bit の詳細については、「[ [ビルド] ページ、プロジェクトデザイナー (C#)](../ide/reference/build-page-project-designer-csharp.md) 」または「 [[コンパイル] ページ (プロジェクトデザイナー) (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md)」を参照してください。

9. SupportedArchitectures: SDK がサポートする、セミコロンで区切られたアーキテクチャの一覧。 使用中のプロジェクトで対象の SDK アーキテクチャがサポートされていない場合、MSBuild は警告を表示します。 この属性が指定されていない場合、MSBuild ではこの種類の警告は表示されません。

10. Supports複数バージョン: この属性が " **エラー** " または " **警告**" に設定されている場合、MSBuild は同じプロジェクトが同じ SDK ファミリの複数のバージョンを参照できないことを示します。 この属性が存在しない場合、または [ **許可**] に設定されている場合、MSBuild はこの種類のエラーまたは警告を表示しません。

11. AppX: ディスク上の Windows コンポーネントライブラリのアプリケーションパッケージへのパスを指定します。 この値は、ローカルデバッグ中に Windows コンポーネントライブラリの登録コンポーネントに渡されます。 ファイル名の名前付け *規則は.... \<Company> . \<Product> \<Architecture> \<Configuration> \<Version>appx*。 属性名の構成とアーキテクチャは省略可能で、Windows コンポーネントライブラリに適用されない場合は属性値です。 この値は、Windows コンポーネントライブラリにのみ適用されます。

12. CopyRedistToSubDirectory: アプリパッケージルート (つまり、**アプリパッケージの作成** ウィザードで選択された **パッケージの場所**) およびランタイムレイアウトルートを基準として、 *\ redist* フォルダーの下にあるファイルをコピーする場所を指定します。 既定の場所は、アプリケーションパッケージのルートと **F5** レイアウトです。

13. DependsOn: この SDK が依存する sdk を定義する SDK id の一覧。 この属性は、参照マネージャーの詳細ペインに表示されます。

14. 詳細情報: ヘルプと詳細情報を提供する web ページの URL。 この値は、参照マネージャーの右ペインにある [詳細情報] リンクに使用されます。

15. 登録の種類: アプリマニフェストの WinMD 登録を指定します。これは、対応する実装 DLL を持つネイティブ WinMD に必要です。

16. ファイル参照: コントロールが含まれているかネイティブ WinMDs である参照のみに対して指定されています。 参照にコントロールが含まれているかどうかを指定する方法については、以下の「 [ツールボックスアイテムの場所の指定](#ToolboxItems) 」を参照してください。

## <a name="specify-the-location-of-toolbox-items"></a><a name="ToolboxItems"></a> ツールボックスアイテムの場所の指定

*SDKManifest.xml* スキーマの **ToolBoxItems** 要素は、プラットフォーム sdk と拡張 sdk の両方で、ツールボックス項目のカテゴリと場所を指定します。 次の例では、異なる場所を指定する方法を示します。 これは、WinMD 参照または DLL 参照に適用されます。

1. ツールボックスの既定のカテゴリにコントロールを配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Default"/>
    </File>
    ```

2. コントロールを特定のカテゴリ名の下に配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory= "MyCategoryName"/>
    </File>
    ```

3. 特定のカテゴリ名の下にコントロールを配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems VSCategory = "Data">
        <ToolboxItems />
    </File>
    ```

4. Blend と Visual Studio で、異なるカテゴリ名の下にコントロールを配置します。

    ```xml
    // Blend accepts a slightly different structure for the category name because it allows a path rather than a single category.
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph" BlendCategory = "Controls/sample/Graph">
        <ToolboxItems />
    </File>
    ```

5. Blend と Visual Studio で特定のコントロールを列挙する。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems BlendCategory = "Controls/sample/Graph">
        <ToolboxItems/>
    </File>
    ```

6. 特定のコントロールを列挙し、Visual Studio の共通パスの下に配置するか、[すべてのコントロール] グループだけに配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Common">
        <ToolboxItems />
        <ToolboxItems VSCategory = "Toolbox.All">
        <ToolboxItems />
    </File>
    ```

7. 特定のコントロールを列挙し、[ツールボックス] に項目を表示せずに特定のセットのみを表示します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.ChooseItemsOnly">
        <ToolboxItems />
    </File>
    ```

## <a name="see-also"></a>関連項目

- [チュートリアル: C++ を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [チュートリアル: C# または Visual Basic を使用した SDK の作成](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)
