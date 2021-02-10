---
title: '方法: ドメイン固有言語ソリューションを作成する'
description: 特殊化された Visual Studio ソリューションを使用して、ドメイン固有言語 (DSL) を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.designerwizard
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools], creating domain-specific language
- Domain-Specific Language Tools, creating solutions
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5d04366c908494386edc9921129db27df0ead4f7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99941412"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>方法: ドメイン固有言語ソリューションを作成する
ドメイン固有言語 (DSL) は、特化した Visual Studio ソリューションを使用して作成されます。

## <a name="prerequisites"></a>前提条件

この手順を開始する前に、次のコンポーネントをインストールします。

- Visual Studio
- Visual Studio SDK ( **Visual studio 拡張機能の開発** ワークロードの一部としてインストールされます)
- モデリング SDK (Visual Studio コンポーネントとしてインストールされます)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="creating-a-domain-specific-language-solution"></a>Domain-Specific 言語ソリューションの作成

1. 新しい **ドメイン固有言語デザイナー** プロジェクトを作成して、DSL ウィザードを起動します。

   > [!NOTE]
   > プロジェクトに対して選択する名前は、コードの生成に使用される可能性があるため、有効な Visual C# 識別子である必要があります。

   ::: moniker range="vs-2017"

   ![DSL ダイアログの作成](../modeling/media/create_dsldialog.png)

   ::: moniker-end

2. DSL テンプレートを選択します。

    [ **Domain-Specific 言語オプションの選択** ] ページで、[ **最小言語**] などのソリューションテンプレートの1つを選択します。 作成する DSL に似たテンプレートを選択します。

    ソリューションテンプレートの詳細については、「 [Domain-Specific 言語ソリューションテンプレートの選択](../modeling/choosing-a-domain-specific-language-solution-template.md)」を参照してください。

3. [ **ファイル拡張子** ] ページでファイル名拡張子を入力します。 コンピューターと DSL をインストールするすべてのコンピューターで一意である必要があります。 " **この拡張機能を使用しているアプリケーションまたは Visual Studio エディターはありません**" というメッセージが表示されます。

   - まだインストールされていない以前の実験用 Dsl でファイル名拡張子を使用していた場合は、[ **実験用インスタンスのリセット** ] ツールを使用して消去できます。これは、VISUAL Studio SDK のメニューにあります。

   - このファイル拡張子を使用する別の Visual Studio 拡張機能がコンピューターに完全にインストールされている場合は、アンインストールすることを検討してください。 [ **ツール** ] メニューの [ **拡張機能マネージャー**] をクリックします。

4. ウィザードの残りのページにあるフィールドを検査し、必要に応じて調整します。 設定に問題がなければ、[ **完了**] をクリックします。 設定の詳細については、「 [DSL デザイナーウィザードのページ](#settings)」を参照してください。

    ウィザードによって、 **Dsl** および **dslpackage** という名前の2つのプロジェクトを持つソリューションが作成されます。

   > [!NOTE]
   > 信頼されていないソースからテキストテンプレートを実行しないことを通知するメッセージが表示された場合は、[ **OK]** をクリックします。 このメッセージを再度表示しないように設定できます。

## <a name="the-dsl-designer-wizard-pages"></a><a name="settings"></a> DSL デザイナーウィザードのページ
 一部のフィールドは、既定値のままにしておくことができます。 ただし、必ず [ファイル拡張子] フィールドを設定してください。

### <a name="solution-settings-page"></a>[ソリューションの設定] ページ
 **ドメイン固有言語の基になるテンプレートを選択してください。**
作成する DSL に似たテンプレートを選択します。 さまざまなテンプレートは、便利な開始点を提供します。 ソリューションテンプレートを選択すると、ウィザードに説明が表示されます。 ソリューションテンプレートの詳細については、「 [Domain-Specific 言語ソリューションテンプレートの選択](../modeling/choosing-a-domain-specific-language-solution-template.md)」を参照してください。

 **ドメイン固有言語に名前を付けるにはどうすればよいですか?**
既定では、ソリューション名になります。 この値からコードが生成されます。 これは、C# クラス名として有効である必要があります。

### <a name="file-extension-page"></a>[ファイル拡張子] ページ
 **モデルファイルで使用する拡張機能**
新しいファイル拡張子を入力します。

 次のように、このファイル拡張子がこのコンピューターで使用するように登録されていないことを確認してください。

 **この拡張機能を処理するために登録されている [その他のツールとアプリケーション**] を確認します。 " **アプリケーションまたは Visual Studio エディターがこの拡張機能を使用していません**" というメッセージが表示された場合は、このファイル拡張子を使用できます。

 ツールまたはパッケージの一覧が表示された場合は、次のいずれかの操作を行う必要があります。

- 別のファイル拡張子を入力してください。

     \- または

- Visual Studio の実験的なインスタンスをリセットします。 これにより、以前に作成したすべての Dsl が登録解除されます。 [ **スタート** ] ボタンをクリックし、[ **すべてのプログラム**]、[ **2010 SDK**]、[ **ツール**] の順に Microsoft Visual Studio、 **Microsoft Visual Studio 2010 の実験用インスタンスをリセット** します。 もう一度使用する Dsl を再構築できます。

     \- または

- このファイル拡張子を使用する Visual Studio 拡張機能がコンピューターに完全にインストールされている場合は、アンインストールします。 [ **ツール** ] メニューの [ **拡張機能マネージャー**] をクリックします。

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
 **厳密な名前のキーファイルを作成する** 既定のオプションでは、DSL アセンブリに署名するための新しいキーが作成されます。

 **既存の厳密な名前のキーを使用する** DSL を別のアセンブリと統合する場合は、このオプションを使用します。

 厳密な名前付けの詳細については、「 [Strong-Named アセンブリの作成と使用](/dotnet/standard/assembly/create-use-strong-named)」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)
- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))