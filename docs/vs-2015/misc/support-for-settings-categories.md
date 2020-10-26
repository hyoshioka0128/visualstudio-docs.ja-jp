---
title: 設定カテゴリのサポート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- settings, supporting with Visual Studio SDK
- Visual Studio SDK, supporting settings
ms.assetid: 3bac375d-8bd5-41be-a8de-32eb33c5cfac
caps.latest.revision: 20
manager: jillfra
ms.openlocfilehash: 15a3896f8a2010a063393d3a11c1ed3453a008d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65689093"
---
# <a name="support-for-settings-categories"></a>設定カテゴリのサポート
設定カテゴリは統合開発環境 (IDE) をカスタマイズするためのグループで構成されます。 たとえば設定により、メニューの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のウィンドウとコンテンツのレイアウトを制御できます。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックし、 **設定のインポートとエクスポート ウィザード**を開始します。 ウィザードには、設定のエクスポート、インポート、リセットという 3 つの選択肢があります。 たとえば、エクスポートを選択すると、ウィザードの **[エクスポートする設定の選択]** ページが表示されます。  
  
 このページのナビゲーション ウィンドウには、ツリー コントロールにカテゴリが表示されます。 カテゴリは、"カスタム設定ポイント" という関連する設定 (チェック ボックス) のグループです。 これらのチェック ボックスを使用して、.vsettings ファイルに保持するカテゴリを選択します。 ウィザードでは、.vsettings ファイルに名前を付け、パスを指定することができます。  
  
> [!NOTE]
> 設定はカテゴリとして保存または復元されます。また、個々の設定名はウィザードに表示されません。  
  
 Managed Package Framework (MPF) は、最小限の追加コードでの設定カテゴリの作成をサポートしています。  
  
- <xref:Microsoft.VisualStudio.Shell.Package> クラスをサブクラス化して、カテゴリのコンテナーとして使用するには、VSPackage を作成します。  
  
- カテゴリ自体を作成するには、<xref:Microsoft.VisualStudio.Shell.DialogPage> クラスから派生させます。  
  
- これら 2 つは <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> で接続します。  
  
## <a name="support-for-settings-categories"></a>設定カテゴリのサポート  
 <xref:Microsoft.VisualStudio.Shell.Package> クラスは、カテゴリの作成をサポートしています。 <xref:Microsoft.VisualStudio.Shell.DialogPage> クラスは、カテゴリを実装しています。 <xref:Microsoft.VisualStudio.Shell.DialogPage> の既定の実装では、カテゴリとしてパブリック プロパティがユーザーに提供されます。 詳細については、「 [Creating a Settings Category](../extensibility/creating-a-settings-category.md)」を参照してください。  
  
 <xref:Microsoft.VisualStudio.Shell.DialogPage> クラスは <xref:Microsoft.VisualStudio.Shell.IProfileManager> を実装しており、オプション ページとユーザー設定の両方について保持機能を提供しています。 <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromXml%2A> メソッドと <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToXml%2A> メソッドは、設定を .vssettings ファイルに保持します。このファイルは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がそれぞれ <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsWriter> として提供します。 <xref:Microsoft.VisualStudio.Shell.IProfileManager.ResetSettings%2A> メソッドは、設定を既定値にリセットします。  
  
 <xref:Microsoft.VisualStudio.Shell.DialogPage> クラスを使用すると、xml フィードから名前と値のペアを読み取り、反映を使用して <xref:Microsoft.VisualStudio.Shell.DialogPage> 派生クラスのパブリック プロパティを検出する <xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromXml%2A> メソッドを実装できます。 名前と値のペアと一致する名前を持つプロパティには、対応する値が指定されます。  
  
 <xref:Microsoft.VisualStudio.Shell.DialogPage.SaveSettingsToXml%2A> の既定の実装では、反映を使用して <xref:Microsoft.VisualStudio.Shell.DialogPage> 派生クラスのパブリック プロパティを検出し、プロパティ名と値を名前と値のペアとして XML フィードに出力します。  
  
### <a name="settings-category-registry-path"></a>設定カテゴリのレジストリ パス  
 設定カテゴリのレジストリ パスは、<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、単語、UserSettings、設定カテゴリ、カスタム設定ポイントの名前の組み合わせで決まります。 設定カテゴリとカスタム設定ポイントの名前は、アンダースコア区切りでレジストリに表示されるローカライズされない正規名の形式に結合されます。 たとえば、設定カテゴリが "My Category"、カスタム設定ポイント名が "My Settings"、ApplicationRegistryRoot が HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp の場合、設定カテゴリのレジストリ キーは HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\UserSettings\My Category_My Settings になります。  
  
> [!NOTE]
> 正規名はユーザー インターフェイス (UI) に表示されません。 正規名は、プログラム ID (ProgID) と同様に、判読できる名前を設定カテゴリに関連付けるために使用されます。  
  
### <a name="settings-category-attribute"></a>設定カテゴリの属性  
 では、 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> **設定のインポートおよびエクスポートウィザード** のカスタム設定ポイントへのカテゴリのマッピングが、カテゴリを提供する VSPackage に関連付けられて決定されます。 次のコードがあるとします。  
  
 [!code-csharp[VSSDKSupportForSettingsCategories#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforsettingscategories/cs/vssdksupportforsettingscategoriespackage.cs#1)]
 [!code-vb[VSSDKSupportForSettingsCategories#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforsettingscategories/vb/vssdksupportforsettingscategoriespackage.vb#1)]  
  
 リソース ID 106 は "My Category" に、107 は "My Settings" に、108 は "Various Options" にマッピングされます。 これは、 `MyPackage` がカテゴリ My Category_My Settings を提供するという宣言です。 カテゴリは `OptionsPageGeneral` クラスから提供されます。この場合、<xref:Microsoft.VisualStudio.Shell.IProfileManager> を実装する必要があります。 このカテゴリの設定は、 `OptionsPageGeneral` クラスのパブリック プロパティです。  
  
 **設定のインポートとエクスポート ウィザード**で、設定ポイントの名前は "My Settings" です。 設定ポイントを選択すると、" **さまざまなオプション**" という説明が表示されます。 設定ポイント名と説明は、ローカライズされた文字列リソースから取得されます。  
  
## <a name="see-also"></a>参照  
 [オプションページの作成](../extensibility/creating-an-options-page.md)   
 [VSSDK のサンプル](../misc/vssdk-samples.md)   
 [VSPackage の状態](../misc/vspackage-state.md)   
 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)