---
title: プロジェクトおよび構成プロパティのサポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project properties, supporting with Visual Studio SDK
- configuration properties, supporting with Visual Studio SDK
ms.assetid: 9fcfaa0f-7b41-4b68-82ec-7a151dca5d7e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c21d552e26add3a5159febd666c1f60573697535
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704901"
---
# <a name="support-for-project-and-configuration-properties"></a>プロジェクトおよび構成プロパティのサポート
統合開発環境 (IDE) の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **「プロパティー」** ウィンドウには、プロジェクトおよび構成プロパティーを表示できます。 ユーザーがアプリケーションのプロパティを設定できるように、独自のプロジェクトの種類のプロパティ ページを提供できます。

 **ソリューション エクスプローラー**でプロジェクト ノードを選択し、[**プロジェクト**] メニューの **[プロパティ**] をクリックすると、プロジェクトと構成のプロパティを含むダイアログ ボックスを開くことができます。 および[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)][!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]および これらの言語から派生したプロジェクトの種類では、このダイアログ ボックスは [全般] ダイアログ ボックス[の [環境] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)にタブ付きのページとして表示されます。 詳細については、「[ビルドに含まれていない: チュートリアル: プロジェクトと構成のプロパティの公開 (C#)」](https://msdn.microsoft.com/library/d850d63b-25e2-4505-9f3d-eb038d7c1d0e)を参照してください。

 プロジェクト用管理パッケージ フレームワーク (MPFProj) には、新しいプロジェクト システムを作成および管理するためのヘルパー クラスが用意されています。 ソース コードとコンパイル手順については、[プロジェクトの MPF - Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10)を参照してください。

## <a name="persistence-of-project-and-configuration-properties"></a>プロジェクトと構成プロパティの永続化
 プロジェクトと構成のプロパティは、.csproj、.vbproj、.myproj など、プロジェクトの種類に関連付けられたファイル名拡張子を持つプロジェクト ファイルに保存されます。 言語プロジェクトは、通常、テンプレート ファイルを使用してプロジェクト ファイルを生成します。 ただし、プロジェクトの種類とテンプレートを関連付ける方法はいくつかあります。 詳細については、「テンプレート[ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。

 プロジェクトと構成のプロパティは、テンプレート ファイルに項目を追加することによって作成されます。 これらのプロパティは、このテンプレートを使用するプロジェクトの種類を使用して作成されたプロジェクトで使用できます。 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]プロジェクトと MPFProj はどちらも、テンプレート ファイル[のビルド時に Not in ビルド: MSBuild の概要](/previous-versions/visualstudio/visual-studio-2008/ms171452(v=vs.90))スキーマを使用します。 これらのファイルには、各構成のプロパティ グループ セクションがあります。 プロジェクトのプロパティは、通常、最初の PropertyGroup セクションに永続化されます。

 次のコードは、基本的な MSBuild プロジェクト ファイルの開始を示しています。

```
<Project MSBuildVersion="2.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Name>SomeProjectSix</Name>
    <SchemaVersion>2.0</SchemaVersion>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
    <Optimize>false</Optimize>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <Optimize>true</Optimize>
```

 このプロジェクト ファイルで`<Name>`、`<SchemaVersion>`プロジェクト プロパティであり`<Optimize>`、構成プロパティです。

 プロジェクト ファイルのプロジェクトプロパティと構成プロパティを永続化するのは、プロジェクトの責任です。

> [!NOTE]
> プロジェクトでは、既定値と異なるプロパティ値のみを永続化することで、永続化を最適化できます。

## <a name="support-for-project-and-configuration-properties"></a>プロジェクトおよび構成プロパティのサポート
 この`Microsoft.VisualStudio.Package.SettingsPage`クラスは、プロジェクトおよび構成のプロパティ ページを実装します。 の既定の`SettingsPage`実装では、汎用プロパティ グリッドのユーザーにパブリック プロパティを提供します。 この`Microsoft.VisualStudio.Package.HierarchyNode.GetPropertyPageGuids`メソッドは、プロジェクト プロパティ`SettingsPage`グリッドの派生クラスを選択します。 この`Microsoft.VisualStudio.Package.ProjectNode.GetConfigPropertyPageGuids`メソッドは、構成プロパティ`SettingsPage`グリッドの派生クラスを選択します。 プロジェクトの種類は、これらのメソッドをオーバーライドして、適切なプロパティ ページを選択する必要があります。

 クラス`SettingsPage`とクラスは`Microsoft.VisualStudio.Package.ProjectNode`、プロジェクトと構成プロパティを永続化するためにこれらのメソッドを提供します。

- `Microsoft.VisualStudio.Package.ProjectNode.GetProjectProperty`プロジェクト`Microsoft.VisualStudio.Package.ProjectNode.SetProjectProperty`プロパティを永続化します。

- `Microsoft.VisualStudio.Package.SettingsPage.GetConfigProperty`構成`Microsoft.VisualStudio.Package.SettingsPage.SetConfigProperty`プロパティを保持します。

  > [!NOTE]
  > `Microsoft.VisualStudio.Package.SettingsPage`クラスと クラス`Microsoft.VisualStudio.Package.ProjectNode`の実装では`Microsoft.Build.BuildEngine`、プロジェクト ファイルからプロジェクトプロパティと構成プロパティを取得および設定するために (MSBuild) メソッドを使用します。

  派生元のクラスは`SettingsPage`、プロジェクト`Microsoft.VisualStudio.Package.SettingsPage.ApplyChanges``Microsoft.VisualStudio.Package.SettingsPage.BindProperties`ファイルのプロジェクト プロパティまたは構成プロパティを実装し、永続化する必要があります。

## <a name="provideobjectattribute-and-registry-path"></a>オブジェクト属性とレジストリ パスを指定します。
 派生`SettingsPage`したクラスは、VSPackage 間で共有されるように設計されています。 VSPackage が から派生したクラスを作成できるように、`SettingsPage`から`Microsoft.VisualStudio.Shell.Package`派生した`Microsoft.VisualStudio.Shell.ProvideObjectAttribute`クラスに を追加します。

 [!code-csharp[VSSDKSupportProjectConfigurationProperties#1](../../extensibility/internals/codesnippet/CSharp/support-for-project-and-configuration-properties_1.cs)]
 [!code-vb[VSSDKSupportProjectConfigurationProperties#1](../../extensibility/internals/codesnippet/VisualBasic/support-for-project-and-configuration-properties_1.vb)]

 属性がアタッチされている VSPackage は重要ではありません。 VSPackage が[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]に登録されると、作成できるオブジェクトのクラス id (CLSID) が登録され、呼び出<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry.CreateInstance%2A>しを呼び出して作成できます。

 作成できるオブジェクトのレジストリ パスは<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>、オブジェクトの種類の 、単語、CLSID、および GUID を組み合わせて決定します。 クラス`MyProjectPropertyPage`の GUID が {3c693da2-5bca-49b3-bd95-ffe0a39dd723} で、ユーザーレジストリルートがHKEY_CURRENT_USER\ソフトウェア\VisualStudio\8.0Exp である場合、 その後、レジストリ パスはHKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0Exp\CLSID\\{3c693da2-5bca-49b3-bd95-ffe0a39dd723} になります。

## <a name="project-and-configuration-property-attributes-and-layout"></a>プロジェクトと構成のプロパティの属性とレイアウト
 、<xref:System.ComponentModel.CategoryAttribute>および<xref:System.ComponentModel.DisplayNameAttribute><xref:System.ComponentModel.DescriptionAttribute>属性は、汎用プロパティ ページのプロジェクトおよび構成プロパティのレイアウト、ラベリング、および説明を決定します。 これらの属性によって、オプションのカテゴリ、表示名、および説明がそれぞれ決定されます。

> [!NOTE]
> 同等の属性、SRCategory、LocDisplayName、および SRDescription は、ローカライズに文字列リソースを使用し、プロジェクトの MPF で定義されています[- Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10).

 次のコードがあるとします。

 [!code-vb[VSSDKSupportProjectConfigurationProperties#2](../../extensibility/internals/codesnippet/VisualBasic/support-for-project-and-configuration-properties_2.vb)]
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#2](../../extensibility/internals/codesnippet/CSharp/support-for-project-and-configuration-properties_2.cs)]

 構成`MyConfigProp`プロパティは、構成プロパティ ページに [**マイ**カテゴリ] の **[マイ コンフィグレーション プロパティ]** として表示されます。 このオプションが選択されている場合は、説明パネルに **「説明**」が表示されます。

## <a name="see-also"></a>関連項目
- [プロパティ ページの追加と削除](../../extensibility/adding-and-removing-property-pages.md)
- [プロジェクト](../../extensibility/internals/projects.md)
- [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
