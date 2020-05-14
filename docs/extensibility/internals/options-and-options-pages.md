---
title: オプションとオプションページ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d21bf6d5ab7e23047a02e1188fff9a47d0cbd58
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706832"
---
# <a name="options-and-options-pages"></a>オプションとオプション ページ
[**ツール**] メニューの **[オプション**] をクリックすると、[**オプション]** ダイアログ ボックスが開きます。 このダイアログ ボックスのオプションは、まとめてオプション ページと呼ばれます。 ナビゲーション ウィンドウのツリー コントロールにはオプション カテゴリが含まれ、すべてのカテゴリにはオプション ページがあります。 ページを選択すると、そのオプションが右側のペインに表示されます。 これらのページでは、VSPackage の状態を決定するオプションの値を変更できます。

## <a name="support-for-options-pages"></a>オプション ページのサポート
 この<xref:Microsoft.VisualStudio.Shell.Package>クラスは、オプション ページとオプション カテゴリの作成をサポートします。 この<xref:Microsoft.VisualStudio.Shell.DialogPage>クラスは、オプション ページを実装します。

 の既定の<xref:Microsoft.VisualStudio.Shell.DialogPage>実装では、プロパティの一般的なグリッドでユーザーにパブリック プロパティを提供します。 ページ上のさまざまなメソッドをオーバーライドして、独自のユーザー インターフェイス (UI) を持つカスタム オプション ページを作成することで、この動作をカスタマイズできます。 詳細については、「[オプション ページの作成](../../extensibility/creating-an-options-page.md)」を参照してください。

 クラス<xref:Microsoft.VisualStudio.Shell.DialogPage>は、<xref:Microsoft.VisualStudio.Shell.IProfileManager>オプション ページとユーザー設定の永続性を提供する を実装します。 <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A>メソッドと メソッド<xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A>の既定の実装では、プロパティを文字列に変換したり、文字列から変換したりできる場合は、プロパティの変更がレジストリのユーザー セクションに永続化されます。

## <a name="options-page-registry-path"></a>オプション ページのレジストリ パス
 既定では、オプション ページによって管理されるプロパティのレジストリ パスは<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>、DialogPage という単語と、オプション ページ クラスの型名を組み合わせて決定します。 たとえば、オプション ページ クラスは次のように定義できます。

 [!code-csharp[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_1.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_1.vb)]

 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> HKEY_CURRENT_USER\ソフトウェア\VisualStudio\8.0Exp の場合、プロパティ名と値のペアはHKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0Exp\ダイアログページのサブキーです。

 オプション ページ自体のレジストリ パスは<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、"ツールオプションページ" という単語、およびオプション ページのカテゴリと名前を組み合わせて決定します。 たとえば、[カスタム オプション] ページにカテゴリ、[マイ オプション ページ]<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>があり、HKEY_LOCAL_MACHINE\SOFTWARE\VisualStudio\8.0Exp の場合、オプション ページにはレジストリ キーHKEY_LOCAL_MACHINE\ソフトウェア\VisualStudio\8.0Exp\ToolsOptionsPages\My オプション ページ\カスタムがあります。

## <a name="toolsoptions-page-attributes-and-layout"></a>ツール/オプション ページの属性とレイアウト
 この<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性は、[オプション]**ダイアログ**ボックスのナビゲーション ツリーで、カスタム オプション ページをカテゴリにグループ化するかどうかを決定します。 この<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性は、インターフェイスを提供する VSPackage にオプション ページを関連付けます。 次のコードがあるとします。

 [!code-csharp[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_2.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_2.vb)]

 これは、MyPackage が 2 つのオプション ページを提供することを宣言します。 [**オプション]** ダイアログ ボックスでは、[**マイ オプション ページ**] カテゴリに[**全般**] と [**カスタム**] の各オプション ページがそれぞれ表示されます。

## <a name="option-attributes-and-layout"></a>オプションの属性とレイアウト
 ページが提供するユーザー インターフェイス (UI) によって、カスタム オプション ページのオプションの外観が決まります。 汎用オプション ページのオプションのレイアウト、ラベル付け、および説明は、次の属性によって決まります。

- <xref:System.ComponentModel.CategoryAttribute>オプションのカテゴリを決定します。

- <xref:System.ComponentModel.DisplayNameAttribute>オプションの表示名を指定します。

- <xref:System.ComponentModel.DescriptionAttribute>は、オプションの説明を決定します。

  > [!NOTE]
  > 同等の属性、SRCategory、LocDisplayName、および SRDescription は、ローカライズ用の文字列リソースを使用し、[マネージ プロジェクト サンプル](/azure/devops/integrate/index)で定義されています。

  次のコードがあるとします。

  [!code-csharp[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_3.cs)]
  [!code-vb[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_3.vb)]

  オプションオプションは、[オプション] カテゴリの **[整数オプション]** として**オプション**ページに表示されます。 このオプションが選択されている場合は、説明ボックスに [**自分の整数] オプション**が表示されます。

## <a name="accessing-options-pages-from-another-vspackage"></a>別の VS パッケージからオプション ページにアクセスする
 オプション ページをホストおよび管理する VSPackage は、オートメーション モデルを使用して、別の VSPackage からプログラムによってアクセスできます。 たとえば、次のコードでは、VSPackage がオプション ページのホストとして登録されています。

 [!code-csharp[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_4.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_4.vb)]

 次のコード例は、MyOptionPage からオプション整数の値を取得します。

 [!code-csharp[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_5.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_5.vb)]

 属性が<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>オプション ページを登録するとき、属性の引数が の場合は AutomationProperties`SupportsAutomation`キーの下に`true`ページが登録されます。 オートメーションは、関連付けられている VSPackage を検索するには、このレジストリ エントリを調べ、オートメーションは、ホストされているオプション ページを使用してプロパティにアクセスします。、この場合は、マイ グリッド ページです。

 オートメーション プロパティのレジストリ パスは<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、単語、AutomationProperties、およびオプション ページのカテゴリと名前を組み合わせて決定されます。 たとえば、オプション ページに [マイ カテゴリ] カテゴリ、マイ グリッド ページ名<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、および の HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp がある場合、オートメーション プロパティにはレジストリ キーHKEY_LOCAL_MACHINE\SOFTWARE\VisualStudio\8.0Exp\オートメーション プロパティ\マイ カテゴリ\マイ グリッド ページがあります。

> [!NOTE]
> 標準名の [グリッド ページCategory.Myは、このキーの Name サブキーの値です。
