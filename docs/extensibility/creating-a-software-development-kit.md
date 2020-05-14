---
title: ソフトウェア開発キットの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 8496afb4-1573-4585-ac67-c3d58b568a12
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f7cf6cf092edf96280c566018231cc00d34c0994
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739591"
---
# <a name="create-a-software-development-kit"></a>ソフトウェア開発キットの作成

ソフトウェア開発キット (SDK) は、Visual Studio で 1 つの項目として参照できる API のコレクションです。 [**参照マネージャ**]ダイアログ ボックスには、プロジェクトに関連するすべての SDK が一覧表示されます。 プロジェクトに SDK を追加すると、その API を Visual Studio で使用できます。

SDK には、次の 2 つのタイプがあります。

- プラットフォーム SDK は、プラットフォーム用のアプリを開発するための必須コンポーネントです。 たとえば、SDK[!INCLUDE[win81](../debugger/includes/win81_md.md)]はアプリを開発[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]するために必要です。

- 拡張機能 SDK は、プラットフォームを拡張するオプション コンポーネントですが、そのプラットフォーム用のアプリを開発する際には必須ではありません。

次のセクションでは、SDK の一般的なインフラストラクチャと、プラットフォーム SDK と拡張 SDK を作成する方法について説明します。

## <a name="platform-sdks"></a>プラットフォーム SDK

プラットフォーム SDK は、プラットフォーム用のアプリを開発するために必要です。 たとえば、SDK[!INCLUDE[win81](../debugger/includes/win81_md.md)]は のアプリを開発するために[!INCLUDE[win81](../debugger/includes/win81_md.md)]必要です。

### <a name="installation"></a>インストール

すべてのプラットフォーム SDK は *、HKLM\ソフトウェア\マイクロソフト\マイクロソフト SDK\\[TPI]\v[TPV]\\ @InstallationFolder = [SDK ルート]* にインストールされます。 したがって[!INCLUDE[win81](../debugger/includes/win81_md.md)]、SDK は*HKLM\ソフトウェア\マイクロソフト\マイクロソフト SDK\Windows\v8.1*にインストールされます。

### <a name="layout"></a>レイアウト

プラットフォーム SDK のレイアウトは次のとおりです。

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
| *参照*フォルダ | コード化できる API を含むバイナリが含まれています。 これらには、Windows メタデータ (WinMD) ファイルまたはアセンブリが含まれます。 |
| *デザインタイム*フォルダ | 実行前/デバッグ時にのみ必要なファイルが含まれています。 これには、XML ドキュメント、ライブラリ、ヘッダー、ツールボックスのデザイン時バイナリ、MSBuild アーティファクトなどが含まれます。<br /><br /> XML ドキュメントは *、理想的には \DesignTime*フォルダーに配置されますが、参照用の XML ドキュメントは引き続き Visual Studio の参照ファイルと一緒に配置されます。 たとえば、参照<em>\\\参照 [config] [arch]\sample.dll\\</em>の XML ドキュメントは*\References\\\\[config] [arch]\sample.xml*になり、そのドキュメントのローカライズ版は*\References\\[config]\\[locale] [locale]\sample.xml\\*になります。 |
| *構成*フォルダー | *フォルダーは、デバッグ*、*リテール*、*および共通構成*の 3 つのフォルダーのみ存在できます。 SDK 作成者は、SDK コンシューマーが対象とする構成に関係なく、同じ SDK ファイルセットを使用する必要がある場合に、ファイルを*CommonConfiguration*の下に配置できます。 |
| *アーキテクチャ*フォルダ | サポートされている*アーキテクチャ*フォルダは、いずれも存在できます。 Visual Studio では、x86、x64、ARM、およびニュートラルのアーキテクチャがサポートされています。 注: Win32 は x86 にマップされ、AnyCPU はニュートラルにマップされます。<br /><br /> MSBuild は、プラットフォーム SDK の*\Common 構成\ニュートラル*の下でのみ表示されます。 |
| *XML* | このファイルでは、Visual Studio が SDK を使用する方法について説明します。 SDK マニフェストのを見[!INCLUDE[win81](../debugger/includes/win81_md.md)]てください。<br /><br /> `<FileList             DisplayName = "Windows"             PlatformIdentity = "Windows, version=8.1"             TargetFramework = ".NET for Windows Store apps, version=v4.5.1; .NET Framework, version=v4.5.1"             MinVSVersion = "14.0">              <File Reference = "Windows.winmd">                <ToolboxItems VSCategory = "Toolbox.Default" />             </File> </FileList>`<br /><br /> **表示名:**[参照] ボックスの一覧に表示されるオブジェクト ブラウザーの値。<br /><br /> **プラットフォーム ID:** この属性の存在は、SDK がプラットフォーム SDK であり、そこから追加された参照をローカルにコピーしてはならないことを Visual Studio と MSBuild に指示します。<br /><br /> **ターゲットフレームワーク:** この属性は、この属性の値で指定された同じフレームワークを対象とするプロジェクトのみが SDK を使用できるようにするために、Visual Studio によって使用されます。<br /><br /> **最小バージョン:** この属性は、Visual Studio で適用される SDK のみを使用するために使用されます。<br /><br /> **参考:** この属性は、コントロールを含む参照に対してのみ指定する必要があります。 参照にコントロールが含まれるかどうかを指定する方法については、以下を参照してください。 |

## <a name="extension-sdks"></a>拡張 SDK

次のセクションでは、拡張 SDK をデプロイするために必要な操作について説明します。

### <a name="installation"></a>インストール

拡張 SDK は、レジストリ キーを指定せずに、特定のユーザーまたはすべてのユーザーに対してインストールできます。 すべてのユーザーに対して SDK をインストールするには、次のパスを使用します。

*%プログラム ファイル%\マイクロソフト SDK\<ターゲット\>プラットフォーム \v\>プラットフォームバージョン番号 \拡張機能 \拡張子Sdk<*

ユーザー固有のインストールの場合は、次のパスを使用します。

*\<ターゲット プラットフォーム\>\v<プラットフォーム のバージョン番号\>\拡張機能*

別の場所を使用する場合は、次のいずれかの操作を行う必要があります。

1. レジストリ キーで指定します。

     **HKLM\ソフトウェア\マイクロソフト\マイクロソフト\<SDK ターゲット プラットフォーム>\<v\>プラットフォームのバージョン番号\<\拡張\<SdkKs SDKName>SDKVersion>**\

     をクリックし、値が の (既定)`<path to SDK><SDKName><SDKVersion>`サブキーを追加します。

2. プロジェクト ファイルに`SDKReferenceDirectoryRoot`MSBuild プロパティを追加します。 このプロパティの値は、参照する拡張 SDK が存在するディレクトリのセミコロン区切りのリストです。

### <a name="installation-layout"></a>インストールレイアウト

拡張 SDK には、次のインストール レイアウトがあります。

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

1. \\<SDKName\> \\<\>SDKVersion : SDK の名前とバージョンは、SDK ルートへのパスにある対応するフォルダー名から派生します。 MSBuild では、この ID を使用してディスク上の SDK を検索し、Visual Studio では、この ID が **[プロパティ**] ウィンドウと **[参照マネージャー** ] ダイアログに表示されます。

2. *参照*フォルダー: API を含むバイナリ。 これらは、Windows メタデータ (WinMD) ファイルまたはアセンブリである可能性があります。

3. *Redist*フォルダー: ランタイム/デバッグに必要なファイルで、ユーザーのアプリケーションの一部としてパッケージ化する必要があります。 すべてのバイナリは*\redist\\<\> \\ \><arch*の下に配置する必要があり、バイナリ名は一意性を確保するために次の形式を持つ必要があります: *]*\<会社>。\<製品>。\<目的>。\<拡張><em>。たとえば、*Cpp.Build.dll</em>. 他の SDK のファイル名と衝突する可能性のあるファイル (javascript、css、pri、xaml、png、jpg など) を持つファイルはすべて<em>、XAML コントロールに\\関連付\>\\けられているファイル\>\\を除いて\>\*、\redist<arch<sdkname<\redist<config の下に配置する必要があります。これらの\>\\ファイルは、arch\><コンポーネント名の下<*\redist\\<構成\>\\の下に配置する必要があります</em>。

4. *DesignTime*フォルダー: 実行前/デバッグ時にのみ必要なファイルで、ユーザーのアプリケーションの一部としてパッケージ化しないでください。 XML ドキュメント、ライブラリ、ヘッダー、ツールボックスのデザイン時バイナリ、MSBuild アーティファクトなどが考えられます。 ネイティブ プロジェクトで使用する対象の SDK には *、SDKName.props*ファイルが必要です。 この種類のファイルのサンプルを次に示します。

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

    XML 参照ドキュメントは、参照ファイルと一緒に配置されます。 たとえば*\\、\References<config\> \\<arch\>\sample.dll*アセンブリの XML 参照ドキュメントは*\references\\<config\> \\<arch\>\sample.xml*であり、そのドキュメントのローカライズされたバージョンは*\references<、arch\\ \> \\ \> \\<ロケール\>\sample.xml*<構成です。

5. *構成*フォルダ: 3 つのサブフォルダ:*デバッグ*、*リテール*、*および共通構成*。 SDK 作成者は、SDK コンシューマーの対象となる構成に関係なく、同じ SDK ファイルのセットを使用する必要がある場合に、ファイルを*CommonConfiguration*の下に配置できます。

6. *アーキテクチャ*フォルダ: x86、x64、ARM、ニュートラルのアーキテクチャがサポートされています。 Win32 は x86 にマップされ、AnyCPU はニュートラルにマップされます。

### <a name="sdkmanifestxml"></a>XML

*SDKManifest.xml*ファイルでは、Visual Studio が SDK を使用する方法について説明します。 以下に例を示します。

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

次のリストは、ファイルの要素を示しています。

1. 表示名: Visual Studio のユーザー インターフェイスで参照マネージャー、ソリューション エクスプローラー、オブジェクト ブラウザー、およびその他の場所に表示される値。

2. 製品ファミリ名: 全体的な SDK 製品名。 たとえば[!INCLUDE[winjs_long](../debugger/includes/winjs_long_md.md)]、SDK の名前は "Microsoft.WinJS.1.0" と "Microsoft.WinJS.2.0" で、同じ SDK 製品ファミリ "Microsoft.WinJS" に属します。 この属性を使用すると、Visual Studio と MSBuild がその接続を確立できます。 この属性が存在しない場合、SDK 名が製品ファミリ名として使用されます。

3. フレームワークの Id: 1 つまたは複数の Windows コンポーネント ライブラリへの依存関係を指定します。 この属性の値は、使用するアプリのマニフェストに配置されます。 この属性は、Windows コンポーネント ライブラリにのみ適用されます。

4. ターゲット フレームワーク: 参照マネージャーとツールボックスで使用できる SDK を指定します。 これは、セミコロンで区切られたターゲット フレームワーク モニカーのリストです。 同じターゲット フレームワークの複数のバージョンが指定されている場合、参照マネージャーは、フィルター処理のために最も低い指定バージョンを使用します。 たとえば、".NET Framework、バージョン=v2.0;.NET Framework、バージョン=v4.5.1"が指定されている場合、参照マネージャーは ".NET Framework、バージョン =v2.0" を使用します。 特定のターゲット フレームワーク プロファイルが指定されている場合、そのプロファイルのみが参照マネージャーによってフィルター処理のために使用されます。 たとえば、"シルバーライト、バージョン =v4.0、プロファイル=WindowsPhone" が指定されている場合、参照マネージャーは Windows Phone プロファイルのみをフィルター処理します。完全な Silverlight 4.0 Framework を対象とするプロジェクトでは、参照マネージャーに SDK が表示されません。

5. 最小バージョン: 最小バージョンのビジュアル スタジオ。

6. MaxPlatformVerson: 拡張機能 SDK が機能しないプラットフォーム バージョンを指定するには、ターゲット プラットフォームの最大バージョンを使用する必要があります。 たとえば、Visual C++ ランタイム パッケージ v11.0 は、Windows 8 プロジェクトでのみ参照する必要があります。 したがって、Windows 8 プロジェクトの最大プラットフォームバージョンは 8.0 です。 つまり、参照マネージャーは、Windows 8.1 プロジェクトの Microsoft Visual C++ ランタイム パッケージをフィルター処理し、MSBuild はプロジェクトが参照するときにエラーを[!INCLUDE[win81](../debugger/includes/win81_md.md)]スローします。 注: この要素は、[!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)]で始まるサポートされています。

7. 適用先: Visual Studio のプロジェクトの種類を指定することによって参照マネージャーで使用できる SDK を指定します。 9 つの値が認識されます: WindowsApp コンテナー、ビジュアル C、VB、CSharp、ウィンドウズ XAML、JavaScript、マネージ、およびネイティブ。 SDKの作成者は、("!")ではなく、および(「+」)、または(「&#124;」)を使用できます。演算子を使用して、SDK に適用されるプロジェクトの種類のスコープを正確に指定できます。

    アプリのプロジェクトを識別します[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]。

8. サポートPrefer32Bit: サポートされる値は"True"と"偽"です。 デフォルトは"True"です。 値が "False" に設定されている場合、SDK を参照[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]するプロジェクトで Prefer32Bit が有効になっている場合、MSBuild はプロジェクトのエラー (またはデスクトップ プロジェクトの警告) を返します。 Prefer32Bit の詳細については、「[ビルド ページ、プロジェクト デザイナー (C#)、](../ide/reference/build-page-project-designer-csharp.md)[またはコンパイル ページ、プロジェクト デザイナー (Visual Basic)」](../ide/reference/compile-page-project-designer-visual-basic.md)を参照してください。

9. サポートされているアーキテクチャ: SDK がサポートするアーキテクチャのセミコロン区切りのリスト。 MSBuild は、使用しているプロジェクト内の対象となる SDK アーキテクチャがサポートされていない場合に警告を表示します。 この属性が指定されていない場合、MSBuild ではこの種類の警告は表示されません。

10. サポート複数バージョン: この属性が**エラー**または**警告**に設定されている場合、MSBuild は同じプロジェクトが同じ SDK ファミリの複数のバージョンを参照できないということを示します。 この属性が存在しないか、または **[許可]** に設定されている場合、MSBuild ではこの種類のエラーまたは警告は表示されません。

11. AppX: ディスク上の Windows コンポーネント ライブラリのアプリ パッケージへのパスを指定します。 この値は、ローカル デバッグ中に Windows コンポーネント ライブラリの登録コンポーネントに渡されます。 ファイル名の命名規則は*\<会社>です。\<製品>。\<建築>。\<構成>。バージョン\<>.appx*. 構成とアーキテクチャは、属性名と属性値 (Windows コンポーネント ライブラリに適用されない場合) のオプションです。 この値は、Windows コンポーネント ライブラリにのみ適用されます。

12. CopyRedistToSubDirectory: *\redist*フォルダーの下のファイルを、アプリ パッケージのルート (つまり、[**アプリ パッケージの作成**] ウィザードで選択したパッケージの**場所**) とランタイム レイアウト ルートに対して相対的にコピーする場所を指定します。 既定の場所は、アプリ パッケージと**F5**レイアウトのルートです。

13. DependsOn: SDK が依存する SDK を定義する SDK ID のリスト。 この属性は、参照マネージャーの詳細ペインに表示されます。

14. 詳細情報: ヘルプと詳細情報を提供する Web ページの URL。 この値は、参照マネージャーの右側のペインにある [詳細情報] リンクで使用されます。

15. 登録の種類: アプリ マニフェストで WinMD の登録を指定し、対応する実装 DLL を持つネイティブの WinMD に必要です。

16. ファイル参照: コントロールを含む参照、またはネイティブの Winmds である参照に対してのみ指定します。 参照にコントロールが含まれるかどうかを指定する方法については、以下[の「ツールボックス項目の場所を指定する](#ToolboxItems)」を参照してください。

## <a name="specify-the-location-of-toolbox-items"></a><a name="ToolboxItems"></a>ツールボックス項目の場所を指定する

*SDKManifest.xml*スキーマの**ToolBoxItems**要素は、プラットフォームと拡張 SDK の両方でツールボックス項目のカテゴリと場所を指定します。 次の例は、異なる場所を指定する方法を示しています。 これは、WinMD または DLL 参照に適用されます。

1. ツールボックスの既定のカテゴリにコントロールを配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Default"/>
    </File>
    ```

2. 特定のカテゴリ名でコントロールを配置します。

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

4. ブレンドと Visual Studio で、さまざまなカテゴリ名でコントロールを配置します。

    ```xml
    // Blend accepts a slightly different structure for the category name because it allows a path rather than a single category.
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph" BlendCategory = "Controls/sample/Graph">
        <ToolboxItems />
    </File>
    ```

5. ブレンドと Visual Studio で特定のコントロールを別々に列挙します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems BlendCategory = "Controls/sample/Graph">
        <ToolboxItems/>
    </File>
    ```

6. 特定のコントロールを列挙し、Visual Studio コモン パスの下に配置するか、またはすべてのコントロール グループにのみ配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Common">
        <ToolboxItems />
        <ToolboxItems VSCategory = "Toolbox.All">
        <ToolboxItems />
    </File>
    ```

7. 特定のコントロールを列挙し、ツールボックスに含まれずに[ChooseItems] に特定のセットのみを表示します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.ChooseItemsOnly">
        <ToolboxItems />
    </File>
    ```

## <a name="see-also"></a>関連項目

- [チュートリアル: C++ を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [チュートリアル: C# または Visual Basic を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)
