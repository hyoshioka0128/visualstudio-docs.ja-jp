---
title: クリーンプロジェクトソリューションのビルド
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.BuildProjectPicker
- vs.batchbuild
helpviewer_keywords:
- Clean Solution command
- builds [Visual Studio], managing
- solution build configurations, starting
- Build Solution command
- project build configurations, starting
- build configurations, starting
- project build configurations, dependencies
- Rebuild Solution command
- solution build configurations, build order
- builds [Visual Studio], preparing
ms.assetid: 710891fd-379e-42c2-a84b-44a7af694ca0
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 15f2817b6fd0aee312ff41af218d01ad80bc785e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72620562"
---
# <a name="building-and-cleaning-projects-and-solutions-in-visual-studio"></a>Visual Studio でのプロジェクトとソリューションのビルドおよびクリーン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの手順を使用して、ソリューション内のプロジェクトまたはプロジェクト項目のすべてまたは一部をビルド、リビルド、またはクリーンを行うことができます。 ステップバイステップチュートリアルについては、「 [チュートリアル: アプリケーションのビルド](../ide/walkthrough-building-an-application.md)」を参照してください。

> [!NOTE]
> ご使用の Visual Studio エディションの UI は、アクティブな設定によって、このトピックで説明する内容とは異なる場合があります。 設定を変更するには、**[ツール]** メニューを開き、**[設定のインポートとエクスポート]** を選択します。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="to-build-rebuild-or-clean-an-entire-solution"></a>ソリューション全体のビルド、リビルド、またはクリーン

1. **ソリューション エクスプローラー**で、ソリューションを選択するか開きます。

2. メニュー バーで、**[ビルド]** を選択し、次のコマンドのいずれかを選択します。

    - **[ビルド]** または **[ソリューションのビルド]** を選択すると、最新のビルド以降に変更されたプロジェクト ファイルとコンポーネントのみがコンパイルされます。

        > [!NOTE]
        > ソリューションに複数のプロジェクトが含まれている場合は、**[ビルド]** コマンドが **[ソリューションのビルド]** になります。

    - **[ソリューションのビルド]** を選択すると、ソリューションが "クリーン" されてから、すべてのプロジェクト ファイルとコンポーネントがビルドされます。

    - **[ソリューションのクリーン]** を選択すると、中間ファイルと出力ファイルがすべて削除されます。 その後、プロジェクト ファイルとコンポーネント ファイルのみを残して、中間ファイルと出力ファイルの新しいインスタンスをビルドできます。

## <a name="to-build-or-rebuild-a-single-project"></a>1 つのプロジェクトをビルドまたはリビルドするには

1. **ソリューション エクスプローラー**で、プロジェクトを選択するか開きます。

2. メニュー バーで、**[ビルド]** を選択してから、**[** _<プロジェクト名>_ のビルド] または **[** _<プロジェクト名>_ のリビルド] を選択します。

    - **[** _<プロジェクト名>_ のビルド] を選択すると、最新のビルド以降に変更されたプロジェクト コンポーネントのみがビルドされます。

    - **[** _<プロジェクト名>_ のリビルド] を選択すると、プロジェクトが "クリーン" されてから、プロジェクト ファイルとすべてのプロジェクト コンポーネントがビルドされます。

## <a name="to-build-only-the-startup-project-and-its-dependencies"></a>スタートアップ プロジェクトとその依存関係のみをビルドするには

1. メニューバーで、[ **ツール**]、[ **オプション**] の順に選択します。

2. **[オプション]** ダイアログ ボックスで、**[プロジェクトおよびソリューション]** ノードを展開してから、**[ビルド/実行]** ページを選択します。

    **[ビルド/実行] ([オプション] ダイアログ ボックス - [プロジェクトおよびソリューション]**) が開きます。

3. **[実行時に、スタートアップ プロジェクトおよび依存関係のみをビルドする]** チェック ボックスをオンにします。

    このチェック ボックスをオンにすると、以下のいずれかの手順を実行したときに、現在のスタートアップ プロジェクトとその依存関係のみがビルドされます。

   - メニューバーで、[**デバッグ**] [デバッグの開始] の順に選択し  >  **Start Debugging**ます (F5 キー)。

   - メニューバーで、[ビルド] [ソリューションのビルド] の順**に選択し**  >  **Build Solution**ます (CTRL + SHIFT + B)。

     このチェック ボックスをオフにすると、上記のいずれかのコマンドを実行した場合に、すべてのプロジェクト、依存関係、およびソリューション ファイルがビルドされます。 既定では、このチェック ボックスはオフです。

## <a name="to-build-only-the-selected-visual-c-project"></a>選択した Visual C++ プロジェクトのみをビルドするには

1. [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] プロジェクトを選択してから、メニュー バーで **[ビルド]**、**[プロジェクトのみ]** の順に選択し、以下のコマンドのいずれかを選択します。

   - **** *<プロジェクト名>* のみをビルド

   - **** *<プロジェクト名>* のみをリビルド

   - **** *<プロジェクト名>* のみをクリーン

   - **** *<プロジェクト名>* へのみリンク

     これらのコマンドは、選択されている [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] プロジェクトにのみ適用されます。プロジェクトの依存関係やソリューション ファイルのビルド、リビルド、クリーン、リンクは行われません。 使用している [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のバージョンに応じて、**[プロジェクトのみ]** のサブメニューに他のコマンドが含まれる場合があります。

## <a name="to-compile-multiple-c-project-items"></a>複数の C++ プロジェクト項目をコンパイルするには

1. **ソリューション エクスプローラー**で、有効なコンパイル アクションのある複数のファイルを選択し、それらのファイルのいずれかのショートカット メニューを開いてから **[コンパイル]** を選択します。

     ファイルに依存関係がある場合、依存関係の順序でコンパイルされます。 コンパイル時に使用できないプリコンパイル済みヘッダーがファイルで必要な場合、コンパイル操作は失敗します。 コンパイル操作では、現在のアクティブなソリューション構成が使用されます。

## <a name="to-stop-a-build"></a>ビルドを停止するには

1. 次のいずれかの操作を実行します。

    - メニュー バーで、**[ビルド]**、**[キャンセル]** の順に選択します。

    - Ctrl + Break キーを選択します。

## <a name="see-also"></a>関連項目
 [方法: ビルドログファイルを表示、保存、および構成](../ide/how-to-view-save-and-configure-build-log-files.md)するビルド[ログ](../msbuild/obtaining-build-logs-with-msbuild.md)[のコンパイルと](../ide/compiling-and-building-in-visual-studio.md)ビルドビルド[構成につい](../ide/understanding-build-configurations.md)[てプロジェクト構成のデバッグとリリース](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e) [C/c + + ビルドのリファレンス](https://msdn.microsoft.com/library/100b4ccf-572c-4d1f-970c-fa0bc0cc0d2d) [Devenv コマンドラインスイッチ](../ide/reference/devenv-command-line-switches.md)[ソリューションとプロジェクト](../ide/solutions-and-projects-in-visual-studio.md)
