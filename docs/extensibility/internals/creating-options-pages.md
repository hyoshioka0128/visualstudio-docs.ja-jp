---
title: オプションページを作成する |Microsoft Docs
description: Visual Studio の [ツール] メニューの [オプション] ページを作成する方法については、「マネージパッケージフレームワークからの表示ページクラスの実装」を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f7b1b8b92f978739bfa4e540013347e216781cd4
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217243"
---
# <a name="create-options-pages"></a>オプションページの作成
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]マネージパッケージフレームワークでは、から派生したクラスは <xref:Microsoft.VisualStudio.Shell.DialogPage> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、[**ツール**] メニューの下に **オプション** ページを追加して IDE を拡張します。

 特定の **ツールオプション** ページを実装するオブジェクトは、オブジェクトによって特定の vspackage に関連付けられ <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> ます。

 環境では、特定の **ツールオプション** ページを実装するオブジェクトをインスタンス化するため、IDE によって特定のページが表示されます。

- **ツールオプション** ページは、VSPackage を実装するオブジェクトではなく、独自のオブジェクトに実装する必要があります。

- オブジェクトは、複数の **ツールオプション** ページを実装することはできません。

## <a name="register-as-a-tools-options-page-provider"></a>ツールオプションページプロバイダーとして登録
 [ **ツールオプション]** ページを使用してユーザー構成をサポートする VSPackage は、実装に適用されたのインスタンスを適用することによって、これらの **ツールオプション** ページを提供するオブジェクトを示し <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> <xref:Microsoft.VisualStudio.Shell.Package> ます。

 [ <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> <xref:Microsoft.VisualStudio.Shell.DialogPage> **ツールオプション** ] ページを実装するすべての派生型に対して、のインスタンスを1つ用意する必要があります。

 の各インスタンス <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> は、[ツール] **オプション** ページを実装する型、[ **ツールオプション** ] ページを識別するために使用されるカテゴリとサブカテゴリを含む文字列、および [ **ツールオプション** ] ページを提供するために型を登録するためのリソース情報を使用します。

## <a name="persist-tools-options-page-state"></a>[ツールオプション] ページの状態の保持
 [ **ツールオプション** ] ページの実装が、オートメーションサポートが有効な状態で登録されている場合、IDE では、その他のすべての **ツールオプション** ページと共にページの状態が維持されます。

 VSPackage は、を使用して、独自の永続化を管理でき <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> ます。 1つまたは他の永続化方法のみを使用する必要があります。

## <a name="implement-dialogpage-class"></a>[ページの実装] クラス
 派生型の VSPackage の実装を提供するオブジェクトは <xref:Microsoft.VisualStudio.Shell.DialogPage> 、次の継承された機能を利用できます。

- 既定のユーザーインターフェイスウィンドウ。

- がクラスに適用されている場合 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 、または <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A> `true` クラスに適用されているに対してプロパティがに設定されている場合は、既定の永続化機構を使用でき <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> ます。

- オートメーションのサポート。

  を使用して **ツールオプション** ページを実装するオブジェクトの最小要件 <xref:Microsoft.VisualStudio.Shell.DialogPage> は、パブリックプロパティの追加です。

  クラスが **ツールオプション** ページプロバイダーとして適切に登録されている場合は、プロパティグリッドの形式で [**ツール**] メニューの [**オプション**] セクションでそのパブリックプロパティを使用できます。

  これらの既定の機能はすべてオーバーライドできます。 たとえば、より高度なユーザーインターフェイスを作成するには、の既定の実装をオーバーライドするだけで済み <xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A> ます。

## <a name="example"></a>例
 次に示すのは、オプションページの単純な "Hello world" の実装です。 Visual Studio パッケージテンプレートによって作成された既定のプロジェクトに、 **メニューコマンド** オプションを選択して次のコードを追加すると、オプションページの機能が適切に示されます。

### <a name="description"></a>説明
 次のクラスでは、最小限の "Hello world" オプションページを定義しています。 ユーザーは、開いたときに、 `HelloWorld` プロパティグリッドでパブリックプロパティを設定できます。

### <a name="code"></a>コード
:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/class1.cs" id="Snippet11":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/class1.vb" id="Snippet11":::

### <a name="description"></a>説明
 パッケージクラスに次の属性を適用すると、パッケージの読み込み時にオプションページが使用できるようになります。 数値は、カテゴリおよびページの任意のリソース Id であり、最後のブール値は、ページがオートメーションをサポートするかどうかを指定します。

### <a name="code"></a>コード
:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/uiusersettingstoolsoptionspagespackage.cs" id="Snippet07":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/uiusersettingstoolsoptionspagespackage.vb" id="Snippet07":::

### <a name="description"></a>説明
 次のイベントハンドラーは、[オプション] ページで設定されたプロパティの値に応じて結果を表示します。 この例では、メソッドを使用して、 <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> 結果をカスタムオプションページ型に明示的にキャストし、ページによって公開されるプロパティにアクセスします。

 パッケージテンプレートによって生成されたプロジェクトの場合は、関数からこの関数を呼び出して `MenuItemCallback` 、[ **ツール** ] メニューに追加された既定のコマンドにアタッチします。

### <a name="code"></a>コード
:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/uiusersettingstoolsoptionspagespackage.cs" id="Snippet08":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/uiusersettingstoolsoptionspagespackage.vb" id="Snippet08":::

## <a name="see-also"></a>関連項目
- [ユーザー設定とオプションの拡張](../../extensibility/extending-user-settings-and-options.md)
- [オプションページのオートメーションサポート](../../extensibility/internals/automation-support-for-options-pages.md)
