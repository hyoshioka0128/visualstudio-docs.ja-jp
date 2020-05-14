---
title: GenerateApplicationManifest タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateApplicationManifest
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateApplicationManifest task
- HostInBrowser property (MSBuild)
- GenerateApplicationManifest task [MSBuild]
ms.assetid: a494102b-0cb2-4755-8e2a-d2c0f39fac1d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f77420c5ab269e1b0052ce6102c4e3196a3be52b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634098"
---
# <a name="generateapplicationmanifest-task"></a>GenerateApplicationManifest タスク

ClickOnce アプリケーション マニフェストまたはネイティブ マニフェストを生成します。 ネイティブ マニフェストでは、コンポーネントの一意の ID を定義し、コンポーネントを構成するアセンブリおよびファイルを指定することによって、コンポーネントを記述します。 ClickOnce アプリケーション マニフェストはネイティブ マニフェストを拡張するもので、アプリケーションのエントリ ポイントを示し、アプリケーションのセキュリティ レベルを指定します。

## <a name="parameters"></a>パラメーター

`GenerateApplicationManifest` タスクのパラメーターの説明を次の表に示します。

| パラメーター | 説明 |
|---------------------------------| - |
| `AssemblyName` | 省略可能な `String` 型のパラメーターです。<br /><br /> 生成されるマニフェストのアセンブリ ID の `Name` フィールドを指定します。 このパラメーターを指定しない場合、名前は `EntryPoint` パラメーターまたは `InputManifest` パラメーターから推測されます。 名前を作成できない場合、タスクはエラーをスローします。 |
| `AssemblyVersion` | 省略可能な `String` 型のパラメーターです。<br /><br /> 生成されるマニフェストのアセンブリ ID の `Version` フィールドを指定します。 このパラメーターを指定しない場合は、既定値の "1.0.0.0" が使用されます。 |
| `ClrVersion` | 省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションで必要な共通言語ランタイム (CLR: Common Language Runtime) の最低限のバージョンを指定します。 既定値は、ビルド システムで使用されている CLR のバージョンです。 タスクがネイティブ マニフェストを生成する場合には、このパラメーターは無視されます。 |
| `ConfigFile` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> アプリケーション構成ファイルがどのアイテムに含まれているのかを指定します。 タスクがネイティブ マニフェストを生成する場合には、このパラメーターは無視されます。 |
| `Dependencies` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 作成するマニフェストが依存する一連のアセンブリを定義したアイテム一覧を指定します。 配置状態に関するその他の情報や依存関係の種類を示したアイテム メタデータを添えると、各アイテムを詳細に記述できます。 詳細については、「[項目メタデータ](#item-metadata)」を参照してください。 |
| `Description` | 省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションまたはコンポーネントの説明を記述します。 |
| `EntryPoint` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 作成されるマニフェスト アセンブリのエントリ ポイントを示すアイテムを 1 つ指定します。<br /><br /> ClickOnce アプリケーション マニフェストの場合、このパラメーターには、アプリケーションの実行時に起動されるアセンブリを指定します。 |
| `ErrorReportUrl` | 省略可能な <xref:System.String?displayProperty=fullName> 型のパラメーターです。<br /><br /> ClickOnce インストールのエラー報告時にダイアログ ボックスに表示される Web ページの URL を指定します。 |
| `FileAssociations` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> ClickOnce の配置マニフェストに関連付けられている 1 つまたは複数のファイルの種類のリストを指定します。<br /><br /> ファイルの関連付けは、.NET Framework 3.5 以降が対象となっている場合にのみ有効です。 |
| `Files` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> マニフェストに含めるファイルです。 各ファイルの完全パスを指定します。 |
| `HostInBrowser` | 省略可能な <xref:System.Boolean> 型のパラメーターです。<br /><br /> `true` の場合、WPF Web ブラウザー アプリケーションのように、アプリケーションがブラウザーでホストされます。 |
| `IconFile` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> アプリケーション アイコンのファイルを示します。 アプリケーション アイコンは、作成されるアプリケーション マニフェストに記述され、 **[スタート]** メニューおよび **[プログラムの追加と削除]** ダイアログで使用されます。 指定しなかった場合には、既定のアイコンが使用されます。 タスクがネイティブ マニフェストを生成する場合には、このパラメーターは無視されます。 |
| `InputManifest` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> マニフェスト ジェネレーターのベースとして使用する、入力 XML ドキュメントを指定します。 これによって、アプリケーション セキュリティまたはカスタム マニフェスト定義など、構造化されたデータが出力マニフェストに反映されます。 XML ドキュメントのルート要素は、asmv1 名前空間内のアセンブリ ノードである必要があります。 |
| `IsolatedComReferences` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 作成されるマニフェスト内で分離する COM コンポーネントを指定します。 このパラメーターを使用すると、"登録を必要としない COM" の配置用に COM コンポーネントを分離できます。 この機能は、標準の COM 登録の定義を使用してマニフェストを自動作成することによって実現されています。 ただし、正しく動作するためには、ビルド処理を行っているコンピューターに、対象の COM コンポーネントが登録されている必要があります。 |
| `ManifestType` | 省略可能な `String` 型のパラメーターです。<br /><br /> 作成するマニフェストの種類を指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `Native`<br />-   `ClickOnce`<br /><br /> このパラメーターが指定されていない場合は、既定の `ClickOnce` が使用されます。 |
| `MaxTargetPath` | 省略可能な `String` 型のパラメーターです。<br /><br /> ClickOnce アプリケーション配置におけるファイル パスの最大許容長を指定します。 この値を指定すると、アプリケーション内の各ファイル パスの長さが、この制限に照らし合わせてチェックされます。 この制限を超える項目に対しては、ビルド警告が出力されます。 この値を指定しないか、ゼロを指定した場合、チェック処理は行われません。 タスクがネイティブ マニフェストを生成する場合には、このパラメーターは無視されます。 |
| `OSVersion` | 省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションで必要なオペレーティング システム (OS) の最低限のバージョンを指定します。 たとえば、"5.1.2600.0" という値は、オペレーティング システムが Windows XP であることを示しています。 このパラメーターを指定しなかった場合には、.NET Framework. でサポートされている最低限の OS である Windows 98 Second Edition を示す "4.10.0.0" が使用されます。 タスクがネイティブ マニフェストを生成する場合には、この入力は無視されます。 |
| `OutputManifest` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> 生成される出力マニフェスト ファイルの名前を指定します。 このパラメーターが指定されていない場合、出力ファイルの名前は、生成されるマニフェストの ID から推測されます。 |
| `Platform` | 省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションの対象プラットフォームを指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `AnyCPU`<br />-   `x86`<br />-   `x64`<br />-   `Itanium`<br /><br /> このパラメーターが指定されていない場合は、既定の `AnyCPU` が使用されます。 |
| `Product` | 省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーション名を示します。 このパラメーターが指定されていない場合、名前は、生成されるマニフェストの ID から推測されます。 この名前は、 **[スタート]** メニューに表示する名前として使用され、 **[プログラムの追加と削除]** ダイアログ ボックスに表示される名前の一部としても使用されます。 |
| `Publisher` | 省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションの発行者を指定します。 このパラメーターが指定されていない場合、名前は、登録されているユーザー名または生成されるマニフェストの ID から推測されます。 この名前は、 **[スタート]** メニューに表示するフォルダー名として使用され、 **[プログラムの追加と削除]** ダイアログ ボックスに表示される名前の一部としても使用されます。 |
| `RequiresMinimumFramework35SP1` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> true の場合、アプリケーションでは .NET Framework 3.5 SP1 またはそれ以降のバージョンが必要です。 |
| `TargetCulture` | 省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションのカルチャを示し、生成されるマニフェストのアセンブリ ID の `Language` フィールドを指定します。 このパラメーターを指定しなかった場合、アプリケーションは、カルチャに依存しないと仮定されます。 |
| `TargetFrameworkMoniker` | 省略可能な `String` 型のパラメーターです。<br /><br /> ターゲット フレームワーク モニカーを指定します。 |
| `TargetFrameworkProfile` | 省略可能な `String` 型のパラメーターです。<br /><br /> ターゲット フレームワーク プロファイルを指定します。 |
| `TargetFrameworkSubset` | 省略可能な `String` 型のパラメーターです。<br /><br /> 対象となる .NET Framework のサブセットの名前を指定します。 |
| `TargetFrameworkVersion` | 省略可能な `String` 型のパラメーターです。<br /><br /> プロジェクトの対象の .NET Framework を指定します。 |
| `TrustInfoFile` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> アプリケーションのセキュリティを指定する XML ドキュメントを示します。 XML ドキュメントのルート要素は、asmv2 名前空間内の trustInfo ノードである必要があります。 タスクがネイティブ マニフェストを生成する場合には、このパラメーターは無視されます。 |
| `UseApplicationTrust` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> true の場合、`Product`、`Publisher`、および `SupportUrl` の各プロパティがアプリケーション マニフェストに書き込まれます。 |

## <a name="remarks"></a>Remarks

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.GenerateManifestBase> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 Task クラスのパラメーターの一覧については、「[Task Base Class](../msbuild/task-base-class.md)」を参照してください。

`GenerateDeploymentManifest` タスクの使用方法については、「[GenerateApplicationManifest タスク](../msbuild/generateapplicationmanifest-task.md)」を参照してください。

各アイテムの配置状態に関するその他の情報を記述したアイテム メタデータを指定すると、依存関係やファイルについての情報をさらに詳細に入力することができます。

## <a name="item-metadata"></a>項目メタデータ

|メタデータ名|説明|
|-------------------|-----------------|
|`DependencyType`|依存関係をアプリケーションと一緒に発行およびインストールするのか、依存関係があらかじめ必要であるのかを示します。 このメタデータは、すべての依存関係に対して有効ですが、ファイルには適用されません。 このメタデータで使用できる値は次のとおりです。<br /><br /> -   `Install`<br />-   `Prerequisite`<br /><br /> 既定値は Install です。|
|`AssemblyType`|依存関係が、マネージド アセンブリであるのかネイティブ アセンブリであるのかを示します。 このメタデータは、すべての依存関係に対して有効ですが、ファイルには適用されません。 このメタデータで使用できる値は次のとおりです。<br /><br /> -   `Managed`<br />-   `Native`<br />-   `Unspecified`<br /><br /> 既定値は `Unspecified` です。この値は、このタスクで自動的にアセンブリの種類を判断することを意味します。|
|`Group`|必要に応じてダウンロードする追加のファイルのグループを示します。 グループ名は、任意の文字列を、アプリケーションで定義します。 空の文字列 (既定) の場合は、ファイルがダウンロード グループに属していないことを示します。 グループに属していないファイルは、アプリケーションの初期ダウンロードの対象になります。 グループに属しているファイルの場合は、<xref:System.Deployment.Application> を使用してアプリケーションから明示的に要求された場合にだけダウンロードされます。<br /><br /> このメタデータは、`IsDataFile` に `false` が設定されているすべてのファイル、および、`DependencyType` に `Install` が設定されているすべての依存関係に対して有効です。|
|`TargetPath`|作成されるマニフェストで、パスを定義する方法を指定します。 この属性はすべてのファイルに対して有効です。 この属性を指定しなかった場合には、アイテムの規定に従います。 この属性は、`DependencyType` に `Install` が設定されているすべてのファイルおよび依存関係に対して有効です。|
|`IsDataFile`|ファイルがデータ ファイルであるかどうかを示す `Boolean` 型のメタデータ値です。 データ ファイルは、アプリケーションを更新したときに移行されるため、特別な扱いが必要です。 このメタデータはファイルに対してのみ有効です。 既定値は `False` です。|

## <a name="example"></a>例

次の例では、`GenerateApplicationManifest` タスクを使用して ClickOnce アプリケーション マニフェストを作成し、`GenerateDeploymentManifest` タスクを使用して、1 つのアセンブリで構成されているアプリケーション用の配置マニフェストを作成します。 次に、`SignFile` タスクを使用して、マニフェストに署名しています。

これは、1 つのプログラム用に ClickOnce マニフェストが作成される、最もシンプルなマニフェスト生成シナリオを示しています。 既定の名前および ID は、マニフェストのアセンブリ名から決定されています。

> [!NOTE]
> 次の例では、マニフェストの作成処理に着目するために、アプリケーションのバイナリはすべてビルド済みであると仮定してあります。 この例では、完全に動作する ClickOnce 配置が生成されます。
>
> [!NOTE]
> この例の `SignFile` タスクで使用されている `Thumbprint` プロパティの詳細については、「[SignFile タスク](../msbuild/signfile-task.md)」を参照してください。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <EntryPoint Include="SimpleWinApp.exe" />
    </ItemGroup>

    <PropertyGroup>
        <Thumbprint>
             <!-- Insert generated thumbprint here -->
        </Thumbprint>
    </PropertyGroup>

    <Target Name="Build">

        <GenerateApplicationManifest
            EntryPoint="@(EntryPoint)">
            <Output
                ItemName="ApplicationManifest"
                TaskParameter="OutputManifest"/>
        </GenerateApplicationManifest>

        <GenerateDeploymentManifest
            EntryPoint="@(ApplicationManifest)">
            <Output
                ItemName="DeployManifest"
                TaskParameter="OutputManifest"/>
        </GenerateDeploymentManifest>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(ApplicationManifest)"/>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(DeployManifest)"/>

    </Target>
</Project>
```

## <a name="example"></a>例

次の例では、`GenerateApplicationManifest` タスクおよび `GenerateDeploymentManifest` タスクを使用して、ClickOnce アプリケーション マニフェストおよびアプリケーションの配置マニフェストを単独のアセンブリで生成しています。このとき、マニフェストの名前と ID を指定しています。

この例は、マニフェストの名前と ID を明示的に指定している点を除けば、前の例に似ています。 また、この例は、インストール アプリケーションではなく、オンライン アプリケーションとして構成されています。

> [!NOTE]
> 次の例では、マニフェストの作成処理に着目するために、アプリケーションのバイナリはすべてビルド済みであると仮定してあります。 この例では、完全に動作する ClickOnce 配置が生成されます。
>
> [!NOTE]
> この例の `SignFile` タスクで使用されている `Thumbprint` プロパティの詳細については、「[SignFile タスク](../msbuild/signfile-task.md)」を参照してください。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <EntryPoint Include="SimpleWinApp.exe" />
    </ItemGroup>

    <PropertyGroup>
        <Thumbprint>
             <!-- Insert generated thumbprint here -->
        </Thumbprint>
    </PropertyGroup>

    <Target Name="Build">

        <GenerateApplicationManifest
            AssemblyName="SimpleWinApp.exe"
            AssemblyVersion="1.0.0.0"
            EntryPoint="@(EntryPoint)"
            OutputManifest="SimpleWinApp.exe.manifest">
            <Output
                ItemName="ApplicationManifest"
                TaskParameter="OutputManifest"/>
        </GenerateApplicationManifest>

        <GenerateDeploymentManifest
                AssemblyName="SimpleWinApp.application"
                AssemblyVersion="1.0.0.0"
                EntryPoint="@(ApplicationManifest)"
                Install="false"
                OutputManifest="SimpleWinApp.application">
                <Output
                    ItemName="DeployManifest"
                    TaskParameter="OutputManifest"/>
        </GenerateDeploymentManifest>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(ApplicationManifest)"/>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(DeployManifest)"/>

    </Target>
</Project>
```

## <a name="example"></a>例

次の例では、`GenerateApplicationManifest` タスクおよび `GenerateDeploymentManifest` タスクを使用して、ClickOnce アプリケーション マニフェストおよびアプリケーションの配置マニフェストを、複数のファイルとアセンブリで生成しています。

> [!NOTE]
> 次の例では、マニフェストの作成処理に着目するために、アプリケーションのバイナリはすべてビルド済みであると仮定してあります。 この例では、完全に動作する ClickOnce 配置が生成されます。
>
> [!NOTE]
> この例の `SignFile` タスクで使用されている `Thumbprint` プロパティの詳細については、「[SignFile タスク](../msbuild/signfile-task.md)」を参照してください。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <EntryPoint Include="SimpleWinApp.exe" />
    </ItemGroup>

    <PropertyGroup>
        <Thumbprint>
             <!-- Insert generated thumbprint here -->
        </Thumbprint>
        <DeployUrl>
            <!-- Insert the deployment URL here -->
        </DeployUrl>
        <SupportUrl>
            <!-- Insert the support URL here -->
        </SupportUrl>
    </PropertyGroup>

    <Target Name="Build">

    <ItemGroup>
        <EntryPoint Include="SimpleWinApp.exe"/>
        <Dependency Include="ClassLibrary1.dll">
            <AssemblyType>Managed</AssemblyType>
            <DependencyType>Install</DependencyType>
        </Dependency>
        <Dependency Include="ClassLibrary2.dll">
            <AssemblyType>Managed</AssemblyType>
            <DependencyType>Install</DependencyType>
            <Group>Secondary</Group>
        </Dependency>
        <Dependency Include="MyAddIn1.dll">
            <AssemblyType>Managed</AssemblyType>
            <DependencyType>Install</DependencyType>
            <TargetPath>Addins\MyAddIn1.dll</TargetPath>
        </Dependency>
        <Dependency Include="ClassLibrary3.dll">
            <AssemblyType>Managed</AssemblyType>
            <DependencyType>Prerequisite</DependencyType>
        </Dependency>

        <File Include="Text1.txt">
            <TargetPath>Text\Text1.txt</TargetPath>
            <Group>Text</Group>
        </File>
        <File Include="DataFile1.xml ">
            <TargetPath>Data\DataFile1.xml</TargetPath>
            <IsDataFile>true</IsDataFile>
        </File>

        <IconFile Include="Heart.ico"/>
        <ConfigFile Include="app.config">
            <TargetPath>SimpleWinApp.exe.config</TargetPath>
        </ConfigFile>
        <BaseManifest Include="app.manifest"/>
    </ItemGroup>

    <Target Name="Build">

        <GenerateApplicationManifest
            AssemblyName="SimpleWinApp.exe"
            AssemblyVersion="1.0.0.0"
            ConfigFile="@(ConfigFile)"
            Dependencies="@(Dependency)"
            Description="TestApp"
            EntryPoint="@(EntryPoint)"
            Files="@(File)"
            IconFile="@(IconFile)"
            InputManifest="@(BaseManifest)"
            OutputManifest="SimpleWinApp.exe.manifest">
            <Output
                ItemName="ApplicationManifest"
                TaskParameter="OutputManifest"/>
        </GenerateApplicationManifest>

        <GenerateDeploymentManifest
            AssemblyName="SimpleWinApp.application"
            AssemblyVersion="1.0.0.0"
            DeploymentUrl="$(DeployToUrl)"
            Description="TestDeploy"
            EntryPoint="@(ApplicationManifest)"
            Install="true"
            OutputManifest="SimpleWinApp.application"
            Product="SimpleWinApp"
            Publisher="Microsoft"
            SupportUrl="$(SupportUrl)"
            UpdateEnabled="true"
            UpdateInterval="3"
            UpdateMode="Background"
            UpdateUnit="weeks">
            <Output
                ItemName="DeployManifest"
                TaskParameter="OutputManifest"/>
        </GenerateDeploymentManifest>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(ApplicationManifest)"/>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(DeployManifest)"/>

    </Target>
</Project>
```

## <a name="example"></a>例

次の例では、`GenerateApplicationManifest` タスクを使用して、*Test.exe* アプリケーション用のネイティブ マニフェストを作成しています。Test.exe は、ネイティブ コンポーネント *Alpha.dll* および分離 COM コンポーネント *Bravo.dll* を参照しています。

この例では *Test.exe.manifest* を作成し、アプリケーションを XCOPY で配置できるようにして、Registration Free COM を利用します。

> [!NOTE]
> 次の例では、マニフェストの作成処理に着目するために、アプリケーションのバイナリはすべてビルド済みであると仮定してあります。 この例では、完全に動作する ClickOnce 配置が生成されます。

```xml
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <File Include="Test.exe" />
        <Dependency Include="Alpha.dll">
            <AssemblyType>Native</AssemblyType>
            <DependencyType>Install</DependencyType>
        </Dependency>
        <ComComponent Include="Bravo.dll" />
    </ItemGroup>

    <Target Name="Build">
        <GenerateApplicationManifest
            AssemblyName="Test.exe"
            AssemblyVersion="1.0.0.0"
            Dependencies="@(Dependency)"
            Files="@(File)"
            IsolatedComReferences="@(ComComponent)"
            ManifestType="Native">
            <Output
                ItemName="ApplicationManifest"
                TaskParameter="OutputManifest"/>
        </GenerateApplicationManifest>

    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [GenerateDeploymentManifest タスク](../msbuild/generatedeploymentmanifest-task.md)
- [SignFile タスク](../msbuild/signfile-task.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
