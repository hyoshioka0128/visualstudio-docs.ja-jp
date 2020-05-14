---
title: プロパティ ページ |マイクロソフトドキュメント
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
ms.openlocfilehash: ac788f51bcdc52cd39469a272909890333c5016b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706050"
---
# <a name="property-pages"></a>[プロパティ ページ]
ユーザーは、プロパティ ページを使用して、プロジェクト構成依存プロパティおよび -独立プロパティを表示および変更できます。 [**プロパティ]** ウィンドウまたはソリューション エクスプローラーのツール バーで、[プロパティ ページ **]** ボタンが有効になり、選択したオブジェクトのプロパティ ページ ビューを提供します。 プロパティ ページは、環境によって作成され、ソリューションとプロジェクトで使用できます。 ただし、構成に依存するプロパティを使用するプロジェクト項目で使用することもできます。 この機能は、プロジェクト内のファイルが適切にビルドするために異なるコンパイラ スイッチ設定を必要とする場合に使用できます。

## <a name="using-property-pages"></a>プロパティ ページの使用
 プロパティ ページが既に表示されている場合に、選択内容が変更された場合 (たとえば、ソリューションからプロジェクトに)、ページに表示される情報が変更され、新しい選択項目のプロパティが表示されます。 プロパティ ページをサポートするオブジェクトにプロパティがない場合、プロパティ ページは空です。

 複数のオブジェクトを選択した場合、プロパティ ページには、選択したすべてのアイテムのプロパティの交差部分が表示されます。 選択した項目に構成依存のプロパティが含まれておらず、ソリューション エクスプローラーのツール バーの **[プロパティ ページ]** ボタンがクリックされた場合は、[プロパティ] ウィンドウにフォーカスが移動します。 [プロパティ] ウィンドウと選択項目に関する詳細については、「[プロパティの拡張](../../extensibility/internals/extending-properties.md)」を参照してください。

 複数のオブジェクトに対してプロパティが表示され、プロパティ ページで値を変更した場合、オブジェクトの値はすべて、最初は異なる値であった場合でも新しい値に設定され、個々のオブジェクトのプロパティが表示されたときにページが空白になります。

 の [**プロジェクトプロパティ ページ]** ダイアログ ボックスには[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、一般的な 2 種類があります。 最初の Visual Basic プロジェクトでは、たとえば、次のスクリーンショットに示すように、プロパティ ページはフィールド形式で表示されます。 2 番目のセクションでは、プロパティ ページはプロパティ ウィンドウに表示されるプロパティ グリッドと同様のプロパティ グリッドをホストします。

 ![Visual Basic プロパティ ページ](../../extensibility/internals/media/vsvbproppages.gif "をクリックします。")フィールド形式とツリー構造を持つ [プロジェクト プロパティ ページ] ダイアログ ボックス

 [プロパティ ページ] ダイアログ ボックスのツリー構造は<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>、 を使用して作成されていません。 環境は、<xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>および インターフェースによって渡されるレベル名に基づいて<xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>、それを構築します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロパティ ページでは、次の 2 つの最上位カテゴリしか使用できません。

- [共通プロパティ] : 選択したオブジェクトのコンフィギュレーションに依存しない情報を表示します。 その結果、共通プロパティ サブカテゴリのいずれかが選択されている場合、ダイアログ ボックスの上部にある [構成]、[プラットフォーム]、および [構成マネージャー] の各オプションは使用できません。

- 構成プロパティ: ソリューションまたはプロジェクトのデバッグ、最適化、およびビルド のパラメーターに関連する構成に依存する情報が含まれています。

  追加の最上位カテゴリを作成することはできませんが、 の`IVsPropertyPage`実装でどちらか一方を表示しないように選択できます。 たとえば、オブジェクトに対して表示する構成に依存しないプロパティがない場合は、[共通プロパティ] カテゴリを表示しないように選択できます。 構成オブジェクト (`ISpecifyPropertyPages`を実装する 、 、および 関連するインターフェイス ) に`ISpecifyPropertyPages`実装する場合は、項目の参照`IVsCfg`オブジェクト`IVsProjectCfg`および構成プロパティから共通プロパティが実装されている場合は、共通プロパティを表示します。

  最上位のカテゴリの下に表示される各カテゴリは、個別のプロパティ ページを表します。 ダイアログ ボックスで使用できるカテゴリとサブカテゴリのエントリは、 および`ISpecifyPropertyPages``IVsPropertyPage`の実装によって決まります。

  `IDispatch`プロパティ ページに表示するプロパティを持つ選択コンテナー内の項目のオブジェクト`ISpecifyPropertyPages`は、クラス ID の一覧を列挙するために実装します。 クラス ID は変数として渡`ISpecifyPropertyPages`され、プロパティ ページのインスタンス化に使用されます。 クラス ID のリストも、ダイアログ ボックス`IVsPropertyPage`の左側にツリー構造を作成するために渡されます。 プロパティ ページは、各ページの情報`IDispatch`を実装`ISpecifyPropertyPages`して入力するオブジェクトに情報を返します。

  参照オブジェクトのプロパティは、選択コンテナ内の`IDispatch`各オブジェクトを使用して取得されます。

  VSPackage に実装`Help::DisplayTopicFromF1Keyword`すると、ヘルプ ボタンの機能が提供されます。

  詳細については、MSDN`IDispatch`ライブラリ`ISpecifyPropertyPages`を参照してください。

  サンプルに表示される 2 番目の種類のプロパティ ページは、次のスクリーンショットに示すように、プロパティ グリッドの形式をホストします。

  ![VC プロパティ ページ](../../extensibility/internals/media/vsvcproppages.gif "をクリックします。")プロパティ グリッドを使用した [プロパティ ページ] ダイアログ ボックス

  インターフェイス`IVSMDPropertyBrowser`と`IVSMDPropertyGrid`(vsmanaged.h で宣言) は、ダイアログ ボックスまたはウィンドウ内のプロパティ グリッドを作成および設定するために使用されます。

  プロジェクトのアーキテクチャは、以前の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]バージョンの . 特に、どのプロジェクトがアクティブであるかという概念が変わりました。 では[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、アクティブなプロジェクトの概念はありません。 以前の開発環境では、アクティブなプロジェクトは、コンテキストに関係なくコマンドをビルドおよび配置するプロジェクトでした。 ソリューションは、どのビルド コマンドと配置コマンドをどのプロジェクトに適用するかを制御し、調停します。

  以前アクティブなプロジェクトが、次の 3 つの方法のいずれかでキャプチャされるようになりました。

- スタートアップ プロジェクト

   ユーザーが F5 キーを押すか、[ビルド] メニューから [実行] を選択したときに開始される、ソリューションのプロパティ ページからプロジェクトを指定できます。 これは、ソリューション エクスプローラーに太字フォントで名前が表示されるという意味で、古いアクティブ なプロジェクトと同様の方法で動作します。

   スタートアップ プロジェクトをオートメーション モデルのプロパティとして取得する場合は、`DTE.Solution.SolutionBuild.StartupProjects`を呼び出します。 VSPackage では、 または<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A>メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A>呼び出します。 `IVsSolutionBuildManager`は、SID_SVsSolutionBuildManagerでサービス`QueryService`として利用できます。 詳細については、「[プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)と[ソリューションの構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

- アクティブ ソリューション ビルド構成

   [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、実装によってオートメーション モデルで利用できるアクティブなソリューション`DTE.Solution.SolutionBuild.ActiveConfiguration`構成を持っています。 ソリューション構成は、ソリューション内のプロジェクトごとに 1 つのプロジェクト構成を含むコレクションです (各プロジェクトは、複数のプラットフォーム上で、名前が異なる複数の構成を持つことができます)。 ソリューションのプロパティ ページに関連する詳細については、「ソリューションの[構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

- 現在選択されているプロジェクト

   選択した<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A>プロジェクト階層とプロジェクト項目を取得するメソッドを実装します。 DTE から、 と`SelectedItems.SelectedItem.Project``SelectedItems.SelectedItem.ProjectItem`メソッドを使用します。 コア[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ドキュメントの見出しの下にサンプル コードがあります。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
- [ソリューション構成](../../extensibility/internals/solution-configuration.md)
