---
title: ソリューションとプロジェクトの作成 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.openprojectfromweb
- vs.newproject
- VS.ToolsOptionsPages.Projects.General
- SolutionItemsProject
helpviewer_keywords:
- solutions [Visual Studio], deleting
- solutions [Visual Studio], creating
- projects [Visual Studio], creating
ms.assetid: 836f8ca0-3fc9-4f4b-9090-45f2e4d2e9c8
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 03ecd3fcc253f255afc59c2d6412f3864fe253b8
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300603"
---
# <a name="creating-solutions-and-projects"></a>Creating Solutions and Projects
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクトは、アプリケーションをビルドするのに必要なものすべての論理的なコンテナーです。 メイン メニューから **[ファイル &#124; 新規作成 &#124; プロジェクト]** の順に選択してプロジェクトを作成すると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によりプロジェクトを含むソリューションが作成されます。 その後、必要に応じて新規または既存のプロジェクトをソリューションにさらに追加できます。 既存のコード ファイルからプロジェクトを作成することができますし、作業が終った時に削除する一時プロジェクト (.NET のみ) を作成することもできます。

> [!NOTE]
> このトピックの説明は、Visual Studio Community エディション に基づいています。 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、使用中の設定または Visual Studio のエディションによっては、この中の説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="create-a-project-from-an-installed-project-template"></a>インストールされたプロジェクト テンプレートからプロジェクトを作成する
 メイン メニューから **[ファイル &#124; 新規 &#124; プロジェクト]** の順に選択し、[新しいプロジェクト] ダイアログを表示します。 **[インストール済み &#124; テンプレート]** の下の左側のウィンドウで、プログラミング言語とプラットフォームまたはテクノロジを選択します。それから、中央のウィンドウで、使用可能なテンプレートを選択します。

 **[新しいプロジェクト]** ダイアログでは、 **[ソリューション]** ドロップダウンで、新規プロジェクトを新規または既存のソリューションに作成するか、または Visual Studio の新しいインスタンスに作成するかについてのオプションが選べます。

## <a name="create-a-project-from-existing-code-files"></a>既存のコード ファイルからプロジェクトを作成する
 制約の緩いソース ファイルのコレクションがあれば、それらを含むプロジェクトを簡単に作成できます。 **[ファイル &#124; 新規 &#124; 既存のコードからプロジェクトを作成]** の順に選択して、 **[既存コード ファイルからの新しいプロジェクトの作成ウィザード]** を開始し、指示に従います。

> [!TIP]
> このオプションは、比較的単純なファイルのコレクションに最適です。

## <a name="create-a-temporary-project-c-and-visual-basic"></a>一時プロジェクト (C# および Visual Basic) を作成する
 一時プロジェクトで作業することにより、ディスクの場所を指定しなくても、.NET プロジェクトを作成して試してみることができます。 プロジェクトを作成するとき、プロジェクトの種類とテンプレートを選択し、 **[新しいプロジェクト]** ダイアログ ボックスに名前を指定するだけでかまいません。 一時プロジェクトの作業中いつでも、プロジェクトを保存したり破棄できます。

## <a name="create-a-net-project-that-targets-a-specific-version-of-the-net-framework"></a>.NET Framework の特定のバージョンを対象とする .NET プロジェクトの作成
 **[新しいプロジェクト]** ダイアログ ボックスの上部にある **[.NET Framework]** バージョンのドロップダウン メニューを使用して、.NET Framework の旧バージョンを対象とするプロジェクトを作成することもできます。 このバージョンの .NET Framework と互換性のあるテンプレートのみが一覧に表示されるため、プロジェクト テンプレートを選択する前にこの値を設定します。

 4 以前のバージョンの .NET Framework にアクセスするには、.NET Framework 3.5 がシステムにインストールされている必要があります。

## <a name="downloading-sample-solutions"></a>サンプル ソリューションのダウンロード
 Visual Studio を使用して、 [MSDN コード ギャラリー](https://go.microsoft.com/fwlink/?LinkId=254185)から、サンプル ソリューションをダウンロードしてインストールすることができます。

 サンプルを個別にダウンロードすることも、テクノロジやトピックを共有する関連サンプルが含まれたサンプル パックをダウンロードすることもできます。 ダウンロードしたサンプルについてソース コードの変更が発行された場合は、そのことが通知されます。

 詳細については、「[Visual Studio のサンプル](../ide/visual-studio-samples.md)」を参照してください。

## <a name="adding-single-files-at-the-solution-level"></a>ソリューション レベルで 1 つのファイルを追加する
 複数のプロジェクトが 1 つのファイルを参照することがあります。または、特定のプロジェクトの下ではなく、ソリューション レベルで論理的に属するテキストまたはその他のデータが 1 つのファイルに含まれていることがあります。  1 つの項目を 1 つのソリューションに追加するには:

1. **ソリューション エクスプローラー**でソリューション ノードを右クリックし、 **[追加 &#124; 新しい項目]** の順に選択するか、 **[追加 &#124; 既存の項目]** の順に選択します。

## <a name="creating-empty-solutions"></a>空のソリューションの作成
 プロジェクトはソリューション内に配置されている必要がありますが、プロジェクトを持たないソリューションを作成することもできます。

#### <a name="to-create-an-empty-solution"></a>空のソリューションを作成するには

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[新しいプロジェクト]** をクリックします。

2. 左ペインで **[インストール済み]** をクリックし、 **[その他のプロジェクトの種類]** をクリックしてから、展開された一覧から **[Visual Studio ソリューション]** をクリックします。

3. 中央のペインで、 **[空のソリューション]** を選択します。

4. ソリューションの **[名前]** および **[場所]** の値を設定し、 **[OK]** をクリックします。

   空のソリューションの作成後、 **[プロジェクト]** メニューの **[新しい項目の追加]** または **[既存項目の追加]** をクリックして、新規または既存のプロジェクトまたは項目を追加できます。

### <a name="deleting-solutions"></a>ソリューションの削除
 ソリューションを完全に削除することもできますが、その場合は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]は使用しません。 ソリューションを削除する前に、別のソリューションで再利用するプロジェクトはすべて移動しておいてください。 次に、ファイル エクスプローラーを使用して、.sln および .suo ソリューション ファイルのあるディレクトリを削除します。

> [!NOTE]
> .suo ファイルは隠しファイルであり、ファイル エクスプローラーの既定の設定では表示されません。

##### <a name="to-delete-a-solution"></a>ソリューションを削除するには

1. **ソリューション エクスプローラー**で、削除するソリューションを右クリックし、 **[エクスプローラーでフォルダーを開く]** をクリックします。

2. ファイル エクスプローラーで、1 つ上の階層に移動します。

3. ソリューションのあるディレクトリを選択し、Del キーを押します。

## <a name="see-also"></a>関連項目
 [ソリューションとプロジェクト](../ide/solutions-and-projects-in-visual-studio.md) [NIB 方法: 複数のプロジェクトから成るソリューションを作成する](https://msdn.microsoft.com/02ecd6dd-0114-46fe-b335-ba9c5e3020d6)
