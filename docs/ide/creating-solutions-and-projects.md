---
title: ソリューションとプロジェクトを作成する
ms.date: 02/06/2018
ms.topic: conceptual
f1_keywords:
- vs.openprojectfromweb
- VS.ToolsOptionsPages.Projects.General
- SolutionItemsProject
helpviewer_keywords:
- solutions [Visual Studio], creating
- projects [Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 503b343299f7b30e9f5e834099274215b262a635
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589748"
---
# <a name="create-solutions-and-projects"></a>ソリューションとプロジェクトを作成する

"*プロジェクト*" には、ソース コード ファイル、ビットマップ、アイコン、コンポーネント、サービス参照など、Visual Studio でアプリをビルドするために必要なアイテムが格納されています。 新しいプロジェクトを作成すると、そのプロジェクトを含む*ソリューション*が Visual Studio によって作成されます。 その後、必要に応じて他の新規または既存のプロジェクトをソリューションに追加できます。 ソリューションには、特定のプロジェクトに関連付けられていないファイルを含めることもできます。

![ソリューション/プロジェクト階層](./media/vside-proj-soln.png)

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac でのプロジェクトの作成](/visualstudio/mac/create-new-projects)に関するページを参照してください。

**ソリューション エクスプローラー**という名称のツール ウィンドウでソリューションやプロジェクトを表示できます。 次のスクリーンショットは、**ソリューション エクスプローラー** (**BikeSharing.Xamarin-UWP**) のサンプル ソリューションです。**BikeSharing.Clients.Core** と **BikeSharing.Clients.Windows** という 2 つのプロジェクトが含まれています。 各プロジェクトに複数のファイル、フォルダー、参照が含まれています。 太字のプロジェクト名は*スタートアップ プロジェクト*です。つまり、アプリを実行すると起動するプロジェクトです。 スタートアップ プロジェクトにするプロジェクトを指定できます。

![ソリューション エクスプローラーとプロジェクト](./media/vside-solution-explorer-projects.png)

プロジェクトは自分で作成できますが (必要なファイルをプロジェクトに追加する方法で)、Visual Studio ではさまざまプロジェクト テンプレートが用意されており、プロジェクトを簡単に作成できます。 テンプレートから新しいプロジェクトを作成する場合、そのプロジェクトの種類の基本要素が与えられます。そこからファイルの名前を変更したり、新しいコード、既存のコード、その他のリソースを必要に応じて追加したりできます。

ただし、Visual Studio でアプリを開発するにあたり、ソリューションとプロジェクトは必須ではありません。 また、Git からコピーしたか、他の場所からダウンロードしたコードを開くことができます。 詳細については、「[プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)」を参照してください。

## <a name="create-a-project-from-a-project-template"></a>プロジェクト テンプレートからプロジェクトを作成する

テンプレートから新しいプロジェクトを作成する方法の詳細については、「[Create a new project in Visual Studio](create-new-project.md)」(Visual Studio で新しいプロジェクトを作成する) に関するページを参照してください。

## <a name="create-a-project-from-existing-code-files"></a>既存のコード ファイルからプロジェクトを作成する

コード ソース ファイルのコレクションがある場合、それらをプロジェクトに簡単に追加できます。

1. メニューで、 **[ファイル]**  >  **[新規作成]**  >  **[既存のコードからプロジェクトを作成]** の順に選択します。

1. **[既存のコードからプロジェクトを作成]** ウィザードの **[作成するプロジェクトの種類を入力してください]** ドロップダウン リスト ボックスでプロジェクトの種類を選択し、 **[次へ]** ボタンを選択します。

1. ウィザードで、ファイルの場所を参照し、 **[名前]** ボックスに新しいプロジェクトの名前を入力します。 完了したら、 **[完了]** ボタンを選択します。

> [!NOTE]
> このオプションは、比較的単純なファイルのコレクションに最適です。 現在のところ、C++、Apache Cordova、Visual Basic、C# のみがプロジェクトの種類としてサポートされています。

## <a name="add-files-to-a-solution"></a>ソリューションにファイルを追加する

ソリューションの Readme ファイルや、特定のプロジェクトの配下ではなく、ソリューション レベルで論理的に属する他のファイルなど、あるファイルが複数のプロジェクトに適用されている場合、そのようなファイルはソリューション自体に追加できます。 ソリューションに項目を追加するには、**ソリューション エクスプローラー**でソリューション ノードのコンテキスト (右クリック) メニューで、 **[追加]**  >  **[新しい項目]** の順に選択するか、 **[追加]**  >  **[既存の項目]** の順に選択します。

## <a name="create-a-net-project-that-targets-a-specific-version-of-the-net-framework"></a>.NET Framework の特定のバージョンを対象とする .NET プロジェクトの作成

.NET Framework プロジェクトを作成するとき、そのプロジェクトで使用する .NET Framework のバージョンを指定できます。 (.NET Core プロジェクトを作成するとき、フレームワークのバージョンは指定しません。)

::: moniker range="vs-2017"

.NET Framework バージョンを指定するには、 **[新しいプロジェクト]** ダイアログ ボックスの **[Framework]** ドロップダウン メニューを選択します。

![[新しいプロジェクト] ダイアログ ボックスの [Framework] ドロップダウン リスト](./media/vside-newproject-framework.png)

> [!NOTE]
> 4 以前のバージョンの .NET Framework にアクセスするには、.NET Framework 3.5 がシステムにインストールされている必要があります。

::: moniker-end

::: moniker range=">=vs-2019"

.NET Framework バージョンを指定するには、 **[新しいプロジェクトの作成]** ページの **[Framework]** ドロップダウン メニューを選択します。

![新しいプロジェクトの構成でのフレームワーク セレクター](media/vs-2019/configure-new-project-framework.png)

::: moniker-end

## <a name="create-empty-solutions"></a>空のソリューションの作成

プロジェクトのない空のソリューションも作成できます。 独自のソリューションとプロジェクトを一から作成する場合、空のソリューションが適しています。

### <a name="to-create-an-empty-solution"></a>空のソリューションを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

::: moniker range="vs-2017"

2. 左側の ( **[テンプレート]** ) ウィンドウで、 **[その他のプロジェクトの種類]** > 展開された一覧で **[Visual Studio ソリューション]** を選択します。

3. 中央のペインで、 **[空のソリューション]** を選択します。

4. 使用するソリューションの **[名前]** と **[場所]** の値を入力して、 **[OK]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

2. **[新しいプロジェクトの作成]** ページで、検索ボックスに「**ソリューション**」と入力します。

3. **[空のソリューション]** テンプレートを選択して、 **[次へ]** をクリックします。

4. 使用するソリューションの **[名前]** と **[場所]** の値を入力して、 **[作成]** を選択します。

::: moniker-end

空のソリューションの作成後、 **[プロジェクト]** メニューの **[新しい項目の追加]** または **[既存項目の追加]** を選んで、新規または既存のプロジェクトや項目を追加できます。

前述のように、プロジェクトやソリューションがなくてもコード ファイルを開くことができます。 この方法でコードを開発する方法については、「[プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)」を参照してください。

::: moniker range="vs-2017"

## <a name="create-a-temporary-project"></a>一時的なプロジェクトを作成する

(C# および Visual Basic のみ)

ディスクの場所を指定せずに .NET ベースのプロジェクトを作成する場合、それは一時的なプロジェクトになります。 一時的なプロジェクトでは、.NET プロジェクトで実験できます。 一時的なプロジェクトで作業しているときはいつでも、一時的なプロジェクトを保存したり、破棄したりできます。

一時的なプロジェクトを作成するには、まず **[ツール]**  >  **[オプション]**  >  **[プロジェクトおよびソリューション]**  >  **[全般]** の順に進み、 **[作成時に新しいプロジェクトを保存]** チェックボックスのチェックをオフにします。 それから、通常どおり、 **[新しいプロジェクト]** ダイアログ ボックスを開きます。

::: moniker-end

## <a name="delete-a-solution-project-or-item"></a>ソリューション、プロジェクト、アイテムを削除する

ソリューションとそのコンテンツを完全に削除できますが、Visual Studio IDE でそれを行うことはできません。 Visual Studio 内でアイテムを削除した場合、現在のソリューションまたはプロジェクトから削除されるだけです。 ソリューションやその他のコンポーネントをシステムから完全に削除するには、エクスプローラーを利用し、 *.sln* または *.suo* のソリューション ファイルが含まれるフォルダーを削除します。 ただし、ソリューションを完全に削除する前に、再び必要になる場合に備え、プロジェクトやファイルをバックアップしておくことをお勧めします。

> [!NOTE]
> *.suo* ファイルは隠しファイルであり、エクスプローラーの既定の設定では表示されません。 隠しファイルを表示するには、エクスプローラーの **[表示]** メニューで **[非表示項目]** チェックボックスをオンにします。

### <a name="permanently-delete-a-solution"></a>ソリューションを完全に削除する

1. **ソリューション エクスプローラー**で、削除するソリューションの右クリック (コンテキスト) メニューから **[エクスプローラーでフォルダーを開く]** を選択します。

1. ファイル エクスプローラーで、1 つ上の階層に移動します。

1. ソリューションが含まれるフォルダーを選択して、**Del** キーを押します。

## <a name="see-also"></a>関連項目

- [ソリューションおよびプロジェクト](../ide/solutions-and-projects-in-visual-studio.md)
- [GitHub の Microsoft のオープン ソース リポジトリ](https://github.com/Microsoft)
- [開発者コード サンプル](https://code.msdn.microsoft.com/)
- [プロジェクトの作成 (Visual Studio for Mac)](/visualstudio/mac/create-new-projects)
