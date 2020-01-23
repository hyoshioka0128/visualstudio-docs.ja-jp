---
title: '方法: ドメイン固有言語ソリューションを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.designerwizard
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools], creating domain-specific language
- Domain-Specific Language Tools, creating solutions
ms.assetid: e585b63b-34d2-405a-8d81-39ea22317975
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e17171b79e06a273e9a9f4bb5032781963e8d818
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918820"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>方法: ドメイン固有言語ソリューションを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ドメイン固有言語 (DSL) は、特殊な [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションを使用して作成されます。

## <a name="prerequisites"></a>[前提条件]
 この手順を開始する前に、次のコンポーネントをインストールする必要があります。

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[https://www.visualstudio.com/](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[Visual Studio SDK](../extensibility/visual-studio-sdk.md)|
|Visual Studio Visualization and Modeling SDK|[SDK のダウンロードのモデリング](https://www.microsoft.com/download/details.aspx?id=48148)|

## <a name="creating-a-domain-specific-language-solution"></a>ドメイン固有言語ソリューションの作成

#### <a name="to-create-a-domain-specific-language-solution"></a>ドメイン固有言語ソリューションを作成するには

1. DSL ウィザードを起動します。

   1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

   2. **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

   3. **[プロジェクトの種類]** の **[その他のプロジェクトの種類]** ノードを展開し、 **[機能拡張]** をクリックします。

   4. **[ドメイン固有言語デザイナー]** をクリックします。

   5. **[名前]** ボックスに、ソリューションの名前を入力します。 **[OK]** をクリックします。

       **ドメイン固有言語デザイナーウィザード**が表示されます。

      > [!NOTE]
      > コードの生成に使用される可能性があるため、 C#入力する名前は有効なビジュアル識別子である必要があります。

      ![DSL ダイアログの作成](../modeling/media/create-dsldialog.png "Create_DSLDialog")

2. DSL テンプレートを選択します。

    **[ドメイン固有言語オプションの選択]** ページで、 **[最小言語]** などのソリューションテンプレートの1つを選択します。 作成する DSL に似たテンプレートを選択します。

    ソリューションテンプレートの詳細については、「[ドメイン固有言語ソリューションテンプレートの選択](../modeling/choosing-a-domain-specific-language-solution-template.md)」を参照してください。

3. **[ファイル拡張子]** ページでファイル名拡張子を入力します。 コンピューターと DSL をインストールするすべてのコンピューターで一意である必要があります。 "**この拡張機能を使用しているアプリケーションまたは Visual Studio エディターはありません**" というメッセージが表示されます。

   - 以前の実験的な Dsl で完全にインストールされていないファイル名拡張子を使用していた場合は、 **[実験用インスタンスのリセット]** ツールを使用してオフにすることができます。これは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] SDK メニューにあります。

   - このファイル拡張子を使用する別の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能がコンピューターに完全にインストールされている場合は、アンインストールすることを検討してください。 **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。

4. ウィザードの残りのページにあるフィールドを検査し、必要に応じて調整します。 設定に問題がなければ、 **[完了]** をクリックします。 設定の詳細については、「 [DSL デザイナーウィザードのページ](#settings)」を参照してください。

    ウィザードによって、 **Dsl**および**dslpackage**という名前の2つのプロジェクトを持つソリューションが作成されます。

   > [!NOTE]
   > 信頼されていないソースからテキストテンプレートを実行しないことを通知するメッセージが表示された場合は、[ **OK]** をクリックします。 このメッセージを再度表示しないように設定できます。

## <a name="settings"></a>DSL デザイナーウィザードのページ
 一部のフィールドは、既定値のままにしておくことができます。 ただし、必ず [ファイル拡張子] フィールドを設定してください。

### <a name="solution-settings-page"></a>[ソリューションの設定] ページ
 **ドメイン固有言語の基になるテンプレートを選択してください。**
作成する DSL に似たテンプレートを選択します。 さまざまなテンプレートは、便利な開始点を提供します。 ソリューションテンプレートを選択すると、ウィザードに説明が表示されます。 ソリューションテンプレートの詳細については、「[ドメイン固有言語ソリューションテンプレートの選択](../modeling/choosing-a-domain-specific-language-solution-template.md)」を参照してください。

 **ドメイン固有言語に名前を付けるにはどうすればよいですか?**
既定では、ソリューション名になります。 この値からコードが生成されます。 これは、 C#クラス名として有効である必要があります。

### <a name="file-extension-page"></a>[ファイル拡張子] ページ
 **モデルファイルで使用する拡張機能**
新しいファイル拡張子を入力します。

 次のように、このファイル拡張子がこのコンピューターで使用するように登録されていないことを確認してください。

 **この拡張機能を処理するために登録されている [その他のツールとアプリケーション**] を確認します。 "**アプリケーションまたは Visual Studio エディターがこの拡張機能を使用していません**" というメッセージが表示された場合は、このファイル拡張子を使用できます。

 ツールまたはパッケージの一覧が表示された場合は、次のいずれかの操作を行う必要があります。

- 別のファイル拡張子を入力してください。

     \- または

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 実験用インスタンスをリセットします。 これにより、以前に作成したすべての Dsl が登録解除されます。 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[2010 SDK]** 、 **[ツール]** の順に Microsoft Visual Studio、 **Microsoft Visual Studio 2010 の実験用インスタンスをリセット**します。 もう一度使用する Dsl を再構築できます。

     \- または

- このファイル拡張子を使用する [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能がコンピューターに完全にインストールされている場合は、アンインストールします。 **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。

### <a name="product-settings-page"></a>[製品の設定] ページ
 **新しいドメイン固有言語が属する製品の名前は何ですか?**
既定値は DSL 名です。

 この値は、Windows エクスプローラー (またはファイルエクスプローラー) で、このファイル拡張子を持つファイルを記述するために使用されます。

 **製品が属している会社の名前は何ですか?**
会社名。

 この値は、DSL パッケージの AssemblyInfo プロパティに組み込まれています。

 **このソリューションのプロジェクトのルート名前空間は何ですか?**
既定では、会社名と製品名で構成される名前が使用されます。

### <a name="signing-page"></a>[署名] ページ
 **厳密な名前のキーファイルを作成する**既定のオプションでは、DSL アセンブリに署名するための新しいキーが作成されます。

 **既存の厳密な名前のキーを使用する**DSL を別のアセンブリと統合する場合は、このオプションを使用します。

 厳密な名前付けの詳細については、「[厳密な名前付きアセンブリの作成と使用](/dotnet/standard/assembly/create-use-strong-named)」を参照してください。

## <a name="see-also"></a>参照
 [ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)[ドメイン固有言語ツール用語集](/previous-versions/bb126564(v=vs.100))
