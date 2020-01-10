---
title: ソリューションとプロジェクト
ms.date: 10/05/2017
ms.topic: conceptual
f1_keywords:
- vs.addnewitem
- vs.addnewsolutionitem
- vs.openproject
- vs.addexistingitem
- vs.addexistingsolutionitem
- vs.environment.projects
- vs.environment.solutions
- VS.SolutionExplorer
- VS.SolutionExplorer.Solutions
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ffa561667ea31f215306c7cac4b9820d7b386b5c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590086"
---
# <a name="solutions-and-projects-in-visual-studio"></a>Visual Studio のソリューションおよびプロジェクト

このページでは、Visual Studio での "*プロジェクト*" と "*ソリューション*" の概念について説明します。 また、ソリューション エクスプローラー ツール ウィンドウ、および新しいプロジェクトの作成方法についても簡単に説明します。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac のプロジェクトおよびソリューション](/visualstudio/mac/projects-and-solutions)に関するページを参照してください。

## <a name="projects"></a>プロジェクト

Visual Studio で、アプリまたは Web サイトを作成するときは、"*プロジェクト*" から始めます。 論理的には、実行可能ファイル、ライブラリ、または Web サイトにコンパイルされる、すべてのファイルがプロジェクトに含まれています。 これらのファイルには、ソース コード、アイコン、イメージ、データ ファイルなどを含めることができます。 また、プロジェクトには、プログラムが通信するさまざまなサービスまたはコンポーネントで必要になる可能性がある、コンパイラ設定とその他の構成ファイルも含まれています。

### <a name="project-file"></a>プロジェクト ファイル

Visual Studio では、[MSBuild](../msbuild/msbuild.md) を使用してソリューション内の各プロジェクトをビルドします。各プロジェクトには MSBuild プロジェクト ファイルが含まれています。 ファイル拡張子は、C# プロジェクト (.csproj)、Visual Basic プロジェクト (.vbproj)、またはデータベース プロジェクト (.dbproj) などのプロジェクトの種類を反映しています。 プロジェクト ファイルは、MSBuild がプロジェクトをビルドするために必要なすべての情報と手順が含まれる XML ドキュメントです。これには、コンテンツ、プラットフォーム要件、バージョン管理情報、Web サーバーまたはデータベース サーバーの設定、実行するタスクなどがあります。

プロジェクト ファイルは、[MSBuild XML スキーマ](../msbuild/msbuild-project-file-schema-reference.md)に基づいています。 Visual Studio で最新の [sdk スタイルのプロジェクト ファイル](../msbuild/how-to-use-project-sdk.md)のコンテンツを確認するには、 **[ソリューション エクスプローラー]** 内でプロジェクト ノードを右クリックし、 **[\<projectname\> の編集]** を選択します。 .NET フレームワークのコンテンツや、そのスタイルのその他のプロジェクトのコンテンツを確認するには、まずプロジェクトをアンロードします ( **[ソリューション エクスプローラー]** を右クリックして、 **[プロジェクトのアンロード]** を選択します)。 次に、プロジェクトを右クリックして、 **[\<projectname\> の編集]** を選択します。

> [!NOTE]
> Visual Studio でソリューションまたはプロジェクトを使用して、コードの編集、ビルド、デバッグを行う必要はありません。 単に Visual Studio でソース ファイルを含むフォルダーを開いて編集を開始できます。 詳細については、「[プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)」を参照してください。

## <a name="solutions"></a>解決策

プロジェクトは*ソリューション* 内に含まれます。 ソリューションは、その名前にもかかわらず、"答え" ではありません。 1 つ以上の関連するプロジェクト、およびビルド情報、Visual Studio ウィンドウの設定、特定のプロジェクトに関連付けられていないその他のファイルに対するコンテナーに過ぎません。 ソリューションは独自の形式を持つテキスト ファイル (拡張子 *.sln*) で記述され、手動での編集は想定されていません。

Visual Studio では、ソリューションの設定を格納するために、2 種類のファイル ( *.sln* および *.suo*) を使用します。

|拡張子|名前|説明|
|---------------|----------|-----------------|
|.sln|Visual Studio ソリューション|ソリューション内のプロジェクト、プロジェクト項目、およびソリューション項目を整理します。|
|.suo|ソリューション ユーザー オプション|ユーザー レベルの設定やブレークポイントなどのカスタマイズを格納します。|

## <a name="create-new-projects"></a>新しいプロジェクトの作成

新しいプロジェクトを作成する最も簡単な方法は、特定の種類のアプリケーションまたは Web サイトのプロジェクト テンプレートから始めることです。 プロジェクト テンプレートは、生成済みのコード ファイル、構成ファイル、資産、設定の基本セットで構成されます。 これらのテンプレートは、新しいプロジェクトを作成するダイアログ ボックスで利用できます ( **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** )。 詳細については、「[Visual Studio で新しいプロジェクトを作成する](create-new-project.md)」と「[ソリューションとプロジェクトを作成する](../ide/creating-solutions-and-projects.md)」を参照してください。

特定の方法で、頻繁にプロジェクトをカスタマイズする場合、新しいプロジェクトを作成するために使用できるカスタム プロジェクト テンプレートを作成できます。 詳細については、[プロジェクト テンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)に関するページをご覧ください。

作成した新しいプロジェクトは既定で *%USERPROFILE%\source\repos* に保存されます。 この場所は、 **[ツール]**  >  **[オプション]**  >  **[プロジェクトとソリューション]**  >  **[場所]** の **[プロジェクトの場所]** で変更できます。 詳細については、「[[プロジェクトおよびソリューション] ページの [オプション] ダイアログ ボックス](../ide/reference/projects-and-solutions-options-dialog-box.md)」を参照してください。

## <a name="solution-explorer"></a>ソリューション エクスプローラー

新しいプロジェクトを作成した後は、**ソリューション エクスプローラー**を使用して、プロジェクトとソリューション、およびそれらの関連項目を表示して管理できます。 次の図に、2 つのプロジェクトを含む C# ソリューションが表示された**ソリューション エクスプローラー**を示します。

![ソリューション エクスプローラー](../ide/media/vs2015_solution_explorer.png)

多くのメニュー コマンドは、**ソリューション エクスプローラー**で各種項目の右クリック メニューから使用できます。 これらのコマンドには、プロジェクトのビルド、NuGet パッケージの管理、参照の追加、ファイル名の変更、テストの実行などが含まれます。 **ソリューション エクスプローラー**の上部のツールバーには、ソリューション ビューからフォルダー ビューに切り替える、隠しファイルを表示する、すべてのノードを折りたたむためなどのボタンがあります。

ASP.NET Core プロジェクトでは、**ソリューション エクスプローラー**でファイルを入れ子にする方法をカスタマイズできます。 詳細については、[ソリューション エクスプローラーでのファイルの入れ子のカスタマイズ](file-nesting-solution-explorer.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio IDE](../get-started/visual-studio-ide.md)
- [プロジェクトとソリューション (Visual Studio for Mac)](/visualstudio/mac/projects-and-solutions)
- [プロジェクト アイテムの追加と削除 (Visual Studio for Mac)](/visualstudio/mac/add-and-remove-project-items)
