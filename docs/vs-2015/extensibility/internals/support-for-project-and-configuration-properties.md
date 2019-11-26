---
title: プロジェクトおよび構成プロパティのサポート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project properties, supporting with Visual Studio SDK
- configuration properties, suppporting with Visual Studio SDK
ms.assetid: 9fcfaa0f-7b41-4b68-82ec-7a151dca5d7e
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b03bc04b1d5b87219110aa65bee53c4a4a8f77e2
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301068"
---
# <a name="support-for-project-and-configuration-properties"></a>プロジェクトおよび構成プロパティのサポート
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 統合開発環境 (IDE) の **[プロパティ]** ウィンドウでは、プロジェクトと構成のプロパティを表示できます。 ユーザーがアプリケーションのプロパティを設定できるように、独自のプロジェクトの種類のプロパティページを提供できます。  
  
 **ソリューションエクスプローラー**でプロジェクトノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックすると、プロジェクトと構成のプロパティを含むダイアログボックスを開くことができます。 これらの言語から派生した [!INCLUDE[csprcs](../../includes/csprcs-md.md)] および [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]、およびプロジェクトの種類では、このダイアログボックスは、 [[全般] ([オプション] ダイアログボックス-[環境](../../ide/reference/general-environment-options-dialog-box.md)]) のタブ付きページとして表示されます。 詳細については、「[ビルド内にありません: チュートリアル: プロジェクトC#および構成プロパティを公開する」 ()](https://msdn.microsoft.com/d850d63b-25e2-4505-9f3d-eb038d7c1d0e)を参照してください。  
  
 プロジェクト用の Managed Package Framework (MPFProj) には、新しいプロジェクトシステムを作成および管理するためのヘルパークラスが用意されています。 ソースコードとコンパイルの手順については、「 [MPF For Projects-Visual Studio 2013](https://archive.codeplex.com/?p=mpfproj12)」を参照してください。  
  
## <a name="persistence-of-project-and-configuration-properties"></a>プロジェクトおよび構成プロパティの永続化  
 プロジェクトと構成のプロパティは、プロジェクトの種類に関連付けられたファイル名拡張子を持つプロジェクトファイルに保存されます (.csproj、.vbproj、myproj など)。 言語プロジェクトでは、通常、プロジェクトファイルを生成するためにテンプレートファイルを使用します。 ただし、プロジェクトの種類とテンプレートを関連付けるには、実際にいくつかの方法があります。 詳細については、「 [NIB: Visual Studio のテンプレート](https://msdn.microsoft.com/141fccaa-d68f-4155-822b-27f35dd94041)と[テンプレートディレクトリの説明 ()」を参照してください。Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。  
  
 プロジェクトと構成のプロパティは、テンプレートファイルに項目を追加することによって作成されます。 これらのプロパティは、このテンプレートを使用するプロジェクトの種類を使用して作成されたプロジェクトで使用できます。 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] プロジェクトと MPFProj は両方とも、テンプレートファイルの "[ビルド内にありません: MSBuild の概要](https://msdn.microsoft.com/b588fd73-a45b-4706-908f-cc131bccfbde)" スキーマを使用します。 これらのファイルには、構成ごとに PropertyGroup セクションがあります。 通常、プロジェクトのプロパティは、構成引数が null 文字列に設定されている最初の PropertyGroup セクションに保存されます。  
  
 次のコードは、基本的な MSBuild プロジェクトファイルの開始を示しています。  
  
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
  
 このプロジェクトファイルの `<Name>` と `<SchemaVersion>` はプロジェクトのプロパティであり、`<Optimize>` は構成プロパティです。  
  
 プロジェクトファイルのプロジェクトおよび構成プロパティを永続化するのはプロジェクトの役割です。  
  
> [!NOTE]
> プロジェクトで永続化を最適化するには、既定値とは異なるプロパティ値のみを保持します。  
  
## <a name="support-for-project-and-configuration-properties"></a>プロジェクトおよび構成プロパティのサポート  
 `Microsoft.VisualStudio.Package.SettingsPage` クラスは、プロジェクトと構成のプロパティページを実装します。 `SettingsPage` の既定の実装では、汎用プロパティグリッド内のユーザーにパブリックプロパティを提供します。 `Microsoft.VisualStudio.Package.HierarchyNode.GetPropertyPageGuids` メソッドは、プロジェクトのプロパティグリッドの `SettingsPage` から派生したクラスを選択します。 `Microsoft.VisualStudio.Package.ProjectNode.GetConfigPropertyPageGuids` メソッドは、構成プロパティグリッドの `SettingsPage` から派生したクラスを選択します。 適切なプロパティページを選択するには、プロジェクトの種類でこれらのメソッドをオーバーライドする必要があります。  
  
 `SettingsPage` クラスと `Microsoft.VisualStudio.Package.ProjectNode` クラスは、次のメソッドを提供してプロジェクトと構成のプロパティを保持します。  
  
- `Microsoft.VisualStudio.Package.ProjectNode.GetProjectProperty` および `Microsoft.VisualStudio.Package.ProjectNode.SetProjectProperty` プロジェクトのプロパティを保持します。  
  
- `Microsoft.VisualStudio.Package.SettingsPage.GetConfigProperty` および `Microsoft.VisualStudio.Package.SettingsPage.SetConfigProperty` 構成プロパティを保持します。  
  
  > [!NOTE]
  > `Microsoft.VisualStudio.Package.SettingsPage` クラスと `Microsoft.VisualStudio.Package.ProjectNode` クラスの実装では、`Microsoft.Build.BuildEngine` (MSBuild) メソッドを使用して、プロジェクトファイルからプロジェクトと構成のプロパティを取得および設定します。  
  
  `SettingsPage` から派生するクラスは `Microsoft.VisualStudio.Package.SettingsPage.ApplyChanges` を実装し、プロジェクトファイルのプロジェクトまたは構成プロパティを永続化するために `Microsoft.VisualStudio.Package.SettingsPage.BindProperties` する必要があります。  
  
## <a name="provideobjectattribute-and-registry-path"></a>属性とレジストリパス  
 `SettingsPage` から派生したクラスは、Vspackage 間で共有されるように設計されています。 VSPackage が `SettingsPage`から派生したクラスを作成できるようにするには、`Microsoft.VisualStudio.Shell.Package`から派生したクラスに `Microsoft.VisualStudio.Shell.ProvideObjectAttribute` を追加します。  
  
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#1](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/cs/vssdksupportprojectconfigurationpropertiespackage.cs#1)]
 [!code-vb[VSSDKSupportProjectConfigurationProperties#1](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/vb/vssdksupportprojectconfigurationpropertiespackage.vb#1)]  
  
 属性がアタッチされている VSPackage は、重要ではありません。 VSPackage が [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]に登録されると、作成可能な任意のオブジェクトのクラス id (CLSID) が登録され、<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry.CreateInstance%2A> の呼び出しによって作成されるようになります。  
  
 作成できるオブジェクトのレジストリパスは、<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>、単語、CLSID、およびオブジェクトの種類の guid を組み合わせることによって決定されます。 `MyProjectPropertyPage` クラスの guid が {3c693da2-5bca-49b3-bd95-ffe0a39dd723} で、UserRegistryRoot が \Software\Microsoft\VisualStudio\8.0Exp HKEY_CURRENT_USER の場合、レジストリパスは \Software\Microsoft\VisualStudio\8.0Exp\CLSID\\{3c693da2-5bca-49b3-bd95-ffe0a39dd723} HKEY_CURRENT_USER になります。  
  
## <a name="project-and-configuration-property-attributes-and-layout"></a>プロジェクトおよび構成プロパティの属性とレイアウト  
 <xref:System.ComponentModel.CategoryAttribute>、<xref:System.ComponentModel.DisplayNameAttribute>、および <xref:System.ComponentModel.DescriptionAttribute> 属性によって、一般的なプロパティページのプロジェクトおよび構成プロパティのレイアウト、ラベル付け、および説明が決まります。 これらの属性によって、オプションのカテゴリ、表示名、および説明がそれぞれ決まります。  
  
> [!NOTE]
> 同等の属性、SRCategory、LocDisplayName、および Srcategory では、ローカライズに文字列リソースを使用し、[プロジェクトの Visual Studio 2013 に対して MPF](https://archive.codeplex.com/?p=mpfproj12)で定義されています。  
  
 次のコードがあるとします。  
  
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#2](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/cs/myprojectpropertypage.cs#2)]
 [!code-vb[VSSDKSupportProjectConfigurationProperties#2](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/vb/myprojectpropertypage.vb#2)]  
  
 `MyConfigProp` 構成プロパティは、構成 プロパティページの **マイカテゴリ** カテゴリの  **Config プロパティ**として表示されます。 このオプションが選択されている場合は、説明パネルに " **My description**" という説明が表示されます。  
  
## <a name="see-also"></a>関連項目  
 [ビルド内にありません: チュートリアル: プロジェクトおよび構成C#プロパティの公開 ()](https://msdn.microsoft.com/d850d63b-25e2-4505-9f3d-eb038d7c1d0e)   
 [プロパティページの追加と削除](../../extensibility/adding-and-removing-property-pages.md)   
 [VSPackage 状態](../../misc/vspackage-state.md)   
 [プロジェクト](../../extensibility/internals/projects.md)   
 [NIB: Visual Studio テンプレート](https://msdn.microsoft.com/141fccaa-d68f-4155-822b-27f35dd94041)   
 [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
