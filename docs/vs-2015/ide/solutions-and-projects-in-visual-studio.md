---
title: ソリューションとプロジェクト
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.savedeferredsaveprojectonclose
- vs.untrustedtemplateopeningdocuments
- Project Properties.FullPath
- vs.addnewsolutionitem
- vs.environment.projects
- vs.openproject
- vs.getopenfilename
- vs.addnewitem
- vs.encoding
- vs.addexistingitem
- Project Properties.URL
- VS.SolutionExplorer
- Project Properties.FileName
- SolutionProperties.Name
- VS.SaveChangesDlg
- vs.newproject
- VS.SolutionExplorer.Selection
- SolutionProperties.Path
- vs.getdirectoryname
- vs.addexistingsolutionitem
- SolutionProperties.Description
- vs.environment.solutions
- vs.saveordiscarddeferredsaveproject
- VS.SolutionExplorer.Solutions
helpviewer_keywords:
- vs.solutionpropertypages
- vs.solutionpropertypages.startupproject
- vs.solutionpropertypages.configurationsettings
- solution items, folder in Solution Explorer
- solution items, shared
- solutions [Visual Studio]
- project items [Visual Studio], about project items
- workspaces
- solutions [Visual Studio], designing
- projects [Visual Studio]
- solutions [Visual Studio], projects and
- vs.solutionpropertypages.projectdependencies
- applications [Visual Studio]
- projects [Visual Studio], setting up
- miscellaneous files
ms.assetid: aeaf56cb-c2dd-47f6-b012-23b84b7a7254
caps.latest.revision: 41
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0b1783adadd1bfab32bfbbdcfb5ae28df7c0aae4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72661191"
---
# <a name="solutions-and-projects-in-visual-studio"></a>Visual Studio のソリューションおよびプロジェクト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio でアプリケーション、Web サイト、Web アプリ、スクリプト、プラグインなどを作成するときは、 *プロジェクト*から始めます。 論理的には、実行可能プログラムや Web サイトにコンパイルされるか、またはコンパイルを実行するために必要とされる、すべてのソース コード ファイル、アイコン、イメージ、データ ファイル、およびその他の要素がプロジェクトに含まれています。  プロジェクトには、プログラムが通信するさまざまなサービスまたはコンポーネントで必要になる可能性がある、すべてのコンパイラ設定とその他の構成ファイルも含まれています。

 文字どおりの意味では、プロジェクトは自身に含まれるすべての項目へのパスを含む仮想フォルダー階層とすべてのビルド設定を定義する XML ファイル (*.vbproj、\*.csproj、\*.vcxproj) です。 Visual Studio では、プロジェクト ファイルはソリューション エクスプローラーでプロジェクトの内容と設定を表示するために使用されます。 プロジェクトをコンパイルすると、MSBuild エンジンがプロジェクト ファイルを使用して実行可能ファイルを作成します。 他の種類の出力を生成するように、プロジェクトをカスタマイズすることもできます。

 論理的にはファイル システム上、プロジェクトは *ソリューション*内に格納されています。ソリューションには、1 つ以上のプロジェクトがあり、ビルド情報、Visual Studio ウィンドウの設定、およびどのプロジェクトにも関連付けられていないその他のファイルが含まれています。 文字どおりの意味では、ソリューションは独自形式を持つテキスト ファイルであり、普通は手動での編集を意図していません。

 ソリューションには、プロジェクトで作業している各ユーザーの設定、ユーザー設定、および構成情報を格納する *.suo ファイルが関連付けられています。

 次の図は、プロジェクトとソリューションの関係、およびそれらに論理的に含まれる項目を示しています。

 ![Visual Studio のプロジェクトとソリューション](../ide/media/vs2015-project-diagram.png "vs2015_project_diagram")

 カスタム プロジェクトや項目テンプレートを作成することもできます。 詳細については、「[Creating Project and Item Templates](../ide/creating-project-and-item-templates.md)」 (プロジェクトと項目テンプレートの作成) をご覧ください。

## <a name="creating-new-projects"></a>プロジェクトの新規作成
 新しいプロジェクトを作成する最も簡単な方法は、最初に定義済みのプロジェクト テンプレートを使用することです。これらのテンプレートは、特定のプログラミング言語で特定の種類のアプリケーションや Web サイトを作成し始めるのに必要な、生成済みのコード ファイル、構成ファイル、資産、および設定の基本セットで構成されます。 これらのテンプレートは、メイン メニューの **[ファイル &#124; 新規作成 &#124; プロジェクト]** または **[ファイル &#124; 新規作成 &#124; Web サイト]** を選択して **[新しいプロジェクト]** ダイアログに移動したときに表示されます。 詳しくは、「 [Creating Solutions and Projects](../ide/creating-solutions-and-projects.md) 」および「  [NIB テンプレートからのプロジェクトの作成](https://msdn.microsoft.com/7c36d86a-6b79-4480-8228-0f925f1204b2)」をご覧ください。

## <a name="managing-projects-in-solution-explorer"></a>ソリューション エクスプローラーでのプロジェクトの管理
 新しいプロジェクトを作成した後は、 **ソリューション エクスプローラー** を使用して、プロジェクト、ソリューション、およびそれらの関連項目を表示して管理します。 次の図に、2 つのプロジェクトを含む C# ソリューションが表示されたサーバー エクスプローラーを示します。

 ![ソリューション エクスプローラー](../ide/media/vs2015-solution-explorer.png "vs2015_solution_explorer")

## <a name="in-this-section"></a>このセクションの内容

- [ソリューションとプロジェクトの作成](../ide/creating-solutions-and-projects.md)

- [プロジェクト項目の追加と削除](../ide/adding-and-removing-project-items.md)

- [プロジェクトおよびソリューションのプロパティの管理](../ide/managing-project-and-solution-properties.md)

- [プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)

- [アプリケーションのプロパティ](../ide/application-properties.md)

- [アセンブリおよびマニフェストへの署名の管理](../ide/managing-assembly-and-manifest-signing.md)

- [方法: アプリケーションアイコンを指定する (Visual Basic、C#)](../ide/how-to-specify-an-application-icon-visual-basic-csharp.md)

- [対象となる特定の .NET Framework バージョンの指定](../ide/targeting-a-specific-dotnet-framework-version.md)

- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

## <a name="see-also"></a>参照
 [Visual Studio IDE](../ide/visual-studio-ide.md)
