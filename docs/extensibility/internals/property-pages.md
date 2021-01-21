---
title: プロパティページ |Microsoft Docs
description: ユーザーがプロジェクトのプロパティを表示および変更できるようにするために、Visual Studio SDK で新しいプロジェクトの種類のプロパティページを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- configuration options, changing properties
- property pages
- property pages, changing configuration options
ms.assetid: b9b3e6e8-1e30-4c89-9862-330265dcf38c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5d446e731c08b85c2c903c2414528ac2a7370c26
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97875532"
---
# <a name="property-pages"></a>[プロパティ ページ]
ユーザーは、プロパティページを使用して、プロジェクトの構成に依存し、依存しないプロパティを表示および変更できます。 選択したオブジェクトのプロパティページビューを提供するオブジェクトの **プロパティウィンドウまた** はソリューションエクスプローラーツールバーで、[**プロパティページ**] ボタンが有効になります。 プロパティページは環境によって作成され、ソリューションとプロジェクトで使用できます。 ただし、構成に依存するプロパティを使用するプロジェクトアイテムに対しても使用できます。 この機能は、プロジェクト内のファイルが、正しくビルドするために異なるコンパイラスイッチ設定を必要とする場合に使用できます。

## <a name="using-property-pages"></a>プロパティページの使用
 プロパティページが既に表示されていて、選択内容が変更された場合 (たとえば、ソリューションからプロジェクトに変更した場合)、ページに表示される情報が変更され、新しい選択項目のプロパティが表示されます。 プロパティページをサポートするプロパティがオブジェクトに存在しない場合、プロパティページは空になります。

 複数のオブジェクトが選択されている場合、プロパティページには、選択したすべての項目のプロパティの共通部分が表示されます。 選択した項目に構成に依存するプロパティが含まれておらず、[ソリューションエクスプローラー] ツールバーの [ **プロパティページ** ] ボタンがクリックされると、プロパティウィンドウにフォーカスが移動します。 プロパティウィンドウと選択に関する詳細については、「 [プロパティの拡張](../../extensibility/internals/extending-properties.md)」を参照してください。

 複数のオブジェクトに対してプロパティが表示され、プロパティページで値を変更した場合、オブジェクトのすべての値は、最初は異なる場合でも新しい値に設定され、個々のオブジェクトのプロパティが表示されたときにそのページは空白になります。

 で使用できる [ **Projectproperty Pages** ] ダイアログボックスには、次の2種類があり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 たとえば、Visual Basic プロジェクトでは、次のスクリーンショットに示すように、フィールド形式を使用してプロパティページが表示されます。 2番目のセクションでは、プロパティページが、[プロパティ] ウィンドウに表示されるのと同様のプロパティグリッドをホストしています。

 ![Visual Basic プロパティページ](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages") フィールド形式とツリー構造を持つ [プロジェクトプロパティページ] ダイアログボックス

 [プロパティページ] ダイアログボックスのツリー構造は、を使用して構築されていません <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。 環境は、およびインターフェイスによって渡されるレベル名に基づい <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage> て構築されます。

 プロパティページで使用できる最上位レベルのカテゴリは2つだけ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] です。

- [共通プロパティ]: 選択したオブジェクトの構成に依存しない情報が表示されます。 その結果、[共通プロパティ] サブカテゴリの1つを選択した場合、ダイアログボックスの上部にある [構成]、[プラットフォーム]、および [Configuration Manager] オプションは使用できません。

- 構成プロパティ。ソリューションまたはプロジェクトのデバッグ、最適化、およびビルドパラメーターに関連する構成に依存する情報が含まれています。

  追加の最上位レベルのカテゴリを作成することはできませんが、の実装に表示しないように選択することもでき `IVsPropertyPage` ます。 たとえば、オブジェクトに対して表示する構成に依存しないプロパティがない場合は、[共通プロパティ] カテゴリを表示しないように選択できます。 `ISpecifyPropertyPages` `ISpecifyPropertyPages` 構成オブジェクト (、 `IVsCfg` 、および関連インターフェイスを実装するオブジェクト) でを実装するときに、項目の Browse オブジェクトと構成プロパティからを実装する場合は、共通プロパティを表示し `IVsProjectCfg` ます。

  最上位レベルのカテゴリの下に表示される各カテゴリは、個別のプロパティページを表します。 ダイアログボックスで使用できるカテゴリおよびサブカテゴリのエントリは、およびの実装によって決まり `ISpecifyPropertyPages` `IVsPropertyPage` ます。

  `IDispatch` プロパティページに表示されるプロパティを持つ選択コンテナー内の項目のオブジェクトは、 `ISpecifyPropertyPages` クラス id の一覧を列挙するために実装されます。 クラス Id はに変数として渡され、 `ISpecifyPropertyPages` プロパティページをインスタンス化するために使用されます。 また、 `IVsPropertyPage` ダイアログボックスの左側にツリー構造を作成するために、クラス id の一覧もに渡されます。 プロパティページでは、を実装するオブジェクトに情報が渡され、 `IDispatch` `ISpecifyPropertyPages` 各ページの情報が入力されます。

  参照オブジェクトのプロパティは、 `IDispatch` 選択コンテナー内の各オブジェクトに対してを使用して取得されます。

  VSPackage にを実装すると、[ `Help::DisplayTopicFromF1Keyword` ヘルプ] ボタンの機能が提供されます。

  詳細については、MSDN ライブラリの「」および「」を参照してください `IDispatch` `ISpecifyPropertyPages` 。

  サンプルに表示されるプロパティページの2番目の種類は、次のスクリーンショットに示すように、プロパティグリッドのフォームをホストします。

  ![VC プロパティページ](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages") プロパティグリッドがある [プロパティページ] ダイアログボックス

  インターフェイス `IVSMDPropertyBrowser` および `IVSMDPropertyGrid` (vsmanaged .h で宣言された) は、ダイアログボックスまたはウィンドウ内でプロパティグリッドを作成および設定するために使用されます。

  プロジェクトのアーキテクチャは、以前のバージョンのから大幅に変更されてい [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 特に、アクティブなプロジェクトの概念は変更されています。 で [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、アクティブなプロジェクトの概念はありません。 以前の開発環境では、コンテキストに関係なく、ビルドおよび配置コマンドが既定で適用されるプロジェクトとして、アクティブなプロジェクトがありました。 ここで、ソリューションによって、ビルドおよび配置コマンドがどのプロジェクトに適用されるかを制御および判別します。

  以前にアクティブなプロジェクトは、次の3つの方法のいずれかでキャプチャされるようになりました。

- スタートアッププロジェクト

   ユーザーが F5 キーを押したとき、または [ビルド] メニューの [実行] を選択したときに開始される、ソリューションのプロパティページからプロジェクトまたはプロジェクトを指定できます。 これは、古いアクティブプロジェクトと同様の方法で動作します。これは、名前が太字のフォントでソリューションエクスプローラーに表示されることを意味します。

   を呼び出すことによって、オートメーションモデルのプロパティとしてスタートアッププロジェクトを取得でき `DTE.Solution.SolutionBuild.StartupProjects` ます。 VSPackage で <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> は、メソッドまたはメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> ます。 `IVsSolutionBuildManager` は、SID_SVsSolutionBuildManager でサービスとして使用でき `QueryService` ます。 詳細については、「 [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md) と [ソリューション構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

- アクティブソリューションビルド構成

   [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、を実装することによって、オートメーションモデルで使用できるアクティブなソリューション構成があり `DTE.Solution.SolutionBuild.ActiveConfiguration` ます。 ソリューション構成は、ソリューション内のプロジェクトごとに1つのプロジェクト構成を含むコレクションです (各プロジェクトは複数の構成を持つことができ、複数のプラットフォームでは名前が異なる場合があります)。 ソリューションのプロパティページに関する詳細については、「 [ソリューションの構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

- 現在選択されているプロジェクト

   <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A>プロジェクト階層とプロジェクト項目、または選択した項目を取得するメソッドを実装します。 DTE からは、 `SelectedItems.SelectedItem.Project` メソッドとメソッドを使用し `SelectedItems.SelectedItem.ProjectItem` ます。 コアドキュメントには、これらの見出しの下にサンプルコードがあり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
- [ソリューションの構成](../../extensibility/internals/solution-configuration.md)
