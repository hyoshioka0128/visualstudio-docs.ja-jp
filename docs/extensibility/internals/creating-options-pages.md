---
title: オプション ページの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 368efaa78a56723d4a72c482bea9ee739385127e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709147"
---
# <a name="create-options-pages"></a>オプション ページの作成
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理パッケージ フレームワークでは、[**ツール**]<xref:Microsoft.VisualStudio.Shell.DialogPage>メニューの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **[オプション]** ページを追加して、派生したクラスが IDE を拡張します。

 指定された**ツール オプション**ページを実装するオブジェクトは、オブジェクトによって特定<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>の VSPackages に関連付けられます。

 環境は、特定のページが IDE によって表示されるときに、特定**のツール オプション**ページを実装するオブジェクトをインスタンス化するためです。

- **ツール オプション**ページは、VSPackage を実装するオブジェクトではなく、独自のオブジェクトに実装する必要があります。

- オブジェクトは、複数の**ツール オプション**ページを実装できません。

## <a name="register-as-a-tools-options-page-provider"></a>[ツール オプション] ページ プロバイダーとして登録する
 **ツール オプション**ページを通じてユーザーの構成をサポートする VSPackage は、実装に<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>適用されたのインスタンスを<xref:Microsoft.VisualStudio.Shell.Package>適用することによって、これらの**ツール オプション**ページを提供するオブジェクトを示します。

 **ツール オプション**ページを<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>実装する派生型ごとに<xref:Microsoft.VisualStudio.Shell.DialogPage>1 つのインスタンスが必要です。

 の各インスタンス<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>では、[**ツール オプション]** ページを実装する型、ツール オプション ページの識別に使用されるカテゴリとサブカテゴリを含む文字列、および **[ツール****オプション]** ページを提供するとしてリソース情報を使用して、その型を登録します。

## <a name="persist-tools-options-page-state"></a>[ツール オプション] ページの状態を保持する
 ツール**オプション**ページの実装がオートメーション サポートを有効にして登録されている場合、IDE は、他のすべての**ツール オプション**ページと共にページの状態を保持します。

 VSPackage は、 を使用して独自<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>の永続性を管理できます。 1 つまたは他の永続化方法のみを使用する必要があります。

## <a name="implement-dialogpage-class"></a>クラスを実装します。
 VSPackage の派生型の実装を提供する<xref:Microsoft.VisualStudio.Shell.DialogPage>オブジェクトは、次の継承された機能を利用できます。

- 既定のユーザー インターフェイス ウィンドウ。

- クラスに適用されている<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>場合、またはクラスに適用される<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A>に対して`true`プロパティがに設定されている場合に<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>使用できる既定の永続化メカニズム。

- オートメーションのサポート。

  **ツール オプション**ページを使用して<xref:Microsoft.VisualStudio.Shell.DialogPage>実装するオブジェクトの最小要件は、パブリック プロパティの追加です。

  クラスが**ツール オプション**ページ プロバイダーとして適切に登録されている場合、そのパブリック プロパティは、プロパティ グリッドの形式で **、[ツール**] メニューの **[オプション]** セクションで使用できます。

  これらの既定の機能はすべてオーバーライドできます。 たとえば、より高度なユーザー インターフェイスを作成するには、 の既定の実装をオーバーライド<xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A>するだけで済みます。

## <a name="example"></a>例
 以下は、オプションページのシンプルな「Hello world」実装です。 **メニュー コマンド**オプションを選択した Visual Studio パッケージ テンプレートで作成された既定のプロジェクトに次のコードを追加すると、オプション ページの機能を適切に示します。

### <a name="description"></a>説明
 次のクラスは、最小限の "Hello world" オプション ページを定義します。 ユーザーは、開いたときに、プロパティ グリッド`HelloWorld`でパブリック プロパティを設定できます。

### <a name="code"></a>コード
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_1.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_1.vb)]

### <a name="description"></a>説明
 パッケージ クラスに次の属性を適用すると、パッケージの読み込み時にオプション ページが使用可能になります。 数値はカテゴリとページの任意のリソース ID であり、最後のブール値はページがオートメーションをサポートするかどうかを指定します。

### <a name="code"></a>コード
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_2.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_2.vb)]

### <a name="description"></a>説明
 次のイベント ハンドラは、オプション ページのプロパティ セットの値に応じて結果を表示します。 このメソッドは<xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A>、カスタム オプション ページの種類に明示的にキャストされた結果を持つメソッドを使用して、ページによって公開されるプロパティにアクセスします。

 パッケージ テンプレートによって生成されたプロジェクトの場合は、この関数を`MenuItemCallback`関数から呼び出して、[**ツール]** メニューに追加された既定のコマンドにアタッチします。

### <a name="code"></a>コード
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_3.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_3.vb)]

## <a name="see-also"></a>関連項目
- [ユーザー設定とオプションを拡張する](../../extensibility/extending-user-settings-and-options.md)
- [オプション・ページの自動化サポート](../../extensibility/internals/automation-support-for-options-pages.md)
