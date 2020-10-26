---
title: '[オプション] ページと [オプション] ページ |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
caps.latest.revision: 35
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4512867f636e2362aa28d52c5af28bf8eb9697f9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75851150"
---
# <a name="options-and-options-pages"></a>オプションとオプション ページ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[**ツール**] メニューの [**オプション**] をクリックすると、[**オプション**] ダイアログボックスが開きます。 このダイアログボックスのオプションは、総称してオプションページと呼ばれます。 ナビゲーションウィンドウのツリーコントロールにはオプションカテゴリが含まれており、すべてのカテゴリにオプションページがあります。 ページを選択すると、そのページのオプションが右ペインに表示されます。 これらのページを使用すると、VSPackage の状態を決定するオプションの値を変更できます。  
  
## <a name="support-for-options-pages"></a>オプションページのサポート  
 クラスは、 <xref:Microsoft.VisualStudio.Shell.Package> オプションページとオプションのカテゴリを作成するためのサポートを提供します。 クラスは、 <xref:Microsoft.VisualStudio.Shell.DialogPage> オプションページを実装します。  
  
 の既定の実装では、 <xref:Microsoft.VisualStudio.Shell.DialogPage> プロパティの汎用グリッド内のユーザーに対してパブリックプロパティが提供されます。 この動作をカスタマイズするには、ページのさまざまなメソッドをオーバーライドして、独自のユーザーインターフェイス (UI) を持つカスタムオプションページを作成します。 詳細については、「 [オプションページの作成](../../extensibility/creating-an-options-page.md)」を参照してください。  
  
 <xref:Microsoft.VisualStudio.Shell.DialogPage>クラスはを実装します <xref:Microsoft.VisualStudio.Shell.IProfileManager> 。これは、オプションページとユーザー設定の永続化を提供します。 メソッドとメソッドの既定の実装では、 <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A> <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A> プロパティを文字列との間で変換できる場合、プロパティの変更がレジストリのユーザーセクションに保持されます。  
  
## <a name="options-page-registry-path"></a>[オプション] ページのレジストリパス  
 既定では、[オプション] ページによって管理されるプロパティのレジストリパスは <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> 、[オプション] ページクラスの [テキスト] ページと [型名] の組み合わせによって決定されます。 たとえば、オプションページクラスは次のように定義できます。  
  
 [!code-csharp[VSSDKSupportForOptionsPages#1](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#1)]
 [!code-vb[VSSDKSupportForOptionsPages#1](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#1)]  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>が \software\microsoft\visualstudio\8.0exp HKEY_CURRENT_USER 場合、プロパティ名と値のペアは HKEY_CURRENT_USER \software\microsoft\visualstudio\8.0exp\dialogpage\company.optionspage.optionspagegeneral. のサブキーになります。  
  
 オプションページ自体のレジストリパスは <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> 、、word、ToolsOptionsPages、およびオプションページのカテゴリと名前を組み合わせることによって決定されます。 たとえば、[カスタムオプション] ページに [カテゴリ]、[マイオプション] ページ、および [\SOFTWARE\Microsoft\VisualStudio\8.0Exp] HKEY_LOCAL_MACHINE がある場合、 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> [オプション] ページには \Software\microsoft\visualstudio\8.0exp\toolsoptionspages\my Option Pages\Custom. というレジストリキーが HKEY_LOCAL_MACHINE ます。  
  
## <a name="toolsoptions-page-attributes-and-layout"></a>[ツール]/[オプション] ページの属性とレイアウト  
 属性を指定すると、 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> [ **オプション** ] ダイアログボックスのナビゲーションツリーで、カスタムオプションページのグループ化がカテゴリに設定されます。 属性は、 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> オプションページと、インターフェイスを提供する VSPackage を関連付けます。 次のコードがあるとします。  
  
 [!code-csharp[VSSDKSupportForOptionsPages#2](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#2)]
 [!code-vb[VSSDKSupportForOptionsPages#2](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#2)]  
  
 これは、MyPackage が2つのオプションページ、OptionsPageGeneral と OptionsPageCustom を提供することを宣言します。 [ **オプション** ] ダイアログボックスの **[マイオプションページ** ] カテゴリには、それぞれ **[全般** ] と [ **カスタム**] という両方のオプションページが表示されます。  
  
## <a name="option-attributes-and-layout"></a>オプションの属性とレイアウト  
 ページに表示されるユーザーインターフェイス (UI) によって、カスタムオプションページのオプションの外観が決まります。 汎用オプションページのオプションのレイアウト、ラベル付け、説明は、次の属性によって決定されます。  
  
- <xref:System.ComponentModel.CategoryAttribute> オプションのカテゴリを決定します。  
  
- <xref:System.ComponentModel.DisplayNameAttribute> オプションの表示名を決定します。  
  
- <xref:System.ComponentModel.DescriptionAttribute> オプションの説明を決定します。  
  
  > [!NOTE]
  > 同等の属性、SRCategory、LocDisplayName、および Srcategory は、ローカライズに文字列リソースを使用し、 [マネージプロジェクトのサンプル](https://msdn.com/vsx)で定義します。  
  
  次のコードがあるとします。  
  
  [!code-csharp[VSSDKSupportForOptionsPages#3](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/optionspagecustom.cs#3)]
  [!code-vb[VSSDKSupportForOptionsPages#3](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/optionspagegeneral.vb#3)]  
  
  オプションの整数オプションは、[オプション] ページの [**マイオプション**] カテゴリの [**整数] オプション**で表示されます。 このオプションが選択されている場合は、[説明] ボックスに **[整数] オプション**が表示されます。  
  
## <a name="accessing-options-pages-from-another-vspackage"></a>別の VSPackage からオプションページにアクセスする  
 オプションページをホストおよび管理する VSPackage は、オートメーションモデルを使用して別の VSPackage からプログラムでアクセスできます。 たとえば、次のコードでは、VSPackage はオプションページのホストとして登録されています。  
  
 [!code-csharp[VSSDKSupportForOptionsPages#4](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#4)]
 [!code-vb[VSSDKSupportForOptionsPages#4](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#4)]  
  
 次のコード片は、MyOptionPage から OptionInteger の値を取得します。  
  
 [!code-csharp[VSSDKSupportForOptionsPages#5](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#5)]
 [!code-vb[VSSDKSupportForOptionsPages#5](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#5)]  
  
 属性が <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> オプションページを登録すると、属性の引数がの場合、ページは automationproperties.automationid キーの下に登録され `SupportsAutomation` `true` ます。 オートメーションは、このレジストリエントリを調べて関連する VSPackage を見つけます。オートメーションは、ホストされているオプションページ (この場合は [マイグリッド] ページ) を使用してプロパティにアクセスします。  
  
 オートメーションプロパティのレジストリパスは <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> 、、word、automationproperties.automationid、およびオプションページのカテゴリと名前を組み合わせることによって決定されます。 たとえば、[オプション] ページに [マイカテゴリ] カテゴリ、[マイグリッド] ページ名、および HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio\8.0Exp がある場合、 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> [オートメーション] プロパティには HKEY_LOCAL_MACHINE \Software\microsoft\visualstudio\8.0exp\automationproperties\my Category\My Grid ページのレジストリキーがあります。  
  
> [!NOTE]
> 標準の名前である My Category.My Grid ページは、このキーの Name サブキーの値です。
