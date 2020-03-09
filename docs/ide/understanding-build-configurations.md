---
title: ビルド構成について
ms.date: 01/20/2020
ms.technology: vs-ide-compile
ms.topic: conceptual
f1_keywords:
- SolutionProperties.ActiveConfig
- vs.build.newprojectconfiguration
- vc.proj.configurationsctrl.multipleconfigs
- vs.build.editsolutionconfigurations
- vs.build.editprojectconfigurations
- vs.multipleconfigurations
- vs.build.newsolutionconfiguration
- VS.ConfigurationManager
- VS.MultipleConfig
helpviewer_keywords:
- solution build configurations, about build configurations
- build configurations
- project build configurations
- build configurations, advanced
- projects [Visual Studio], build configuration
- solutions [Visual Studio], build configuration
ms.assetid: 934c727d-3a22-429c-bd13-3552cecf2e24
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a37d4fa5dc92253b94dc64590c9df5fec7703ceb
ms.sourcegitcommit: b016ea260856264eee730ee8cbcab198314a7ece
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "77904166"
---
# <a name="understand-build-configurations"></a>ビルド構成について

異なる設定でプロジェクトをビルドする必要がある場合は、ビルド構成が必要です。 たとえば、 **[デバッグ]** や **[リリース]** は構成であり、それらをビルドするときにはそれぞれ異なるコンパイラ オプションが使用されます。  1 つの構成がアクティブになっており、IDE の上部にあるコマンド バーに表示されます。

![アクティブな構成](media/understanding-build-configurations/active-config.png)

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac でのビルド構成](/visualstudio/mac/configurations)に関するページを参照してください。

構成とプラットフォームによって、ビルドされた出力ファイルが格納される場所が制御されます。 通常、Visual Studio でプロジェクトをビルドすると、アクティブな構成で名前付けされたプロジェクトのサブフォルダー (例: *bin/Debug/x86*) に出力が配置されます。ただし、これは変更できます。

ソリューション レベルとプロジェクト レベルで独自のビルド構成を作成することができます。 ソリューション構成では、その構成がアクティブなときにビルドに含まれるプロジェクトが決定されます。 アクティブなソリューション構成で指定されているプロジェクトのみがビルドされます。 構成マネージャーで複数のターゲット プラットフォームが選択されている場合、そのプラットフォームに適用されるすべてのプロジェクトがビルドされます。 プロジェクト構成では、そのプロジェクトをビルドするときに使用されるビルド設定とコンパイラ オプションが決定されます。

構成を作成、選択、変更、または削除するには、**構成マネージャー**を使用できます。 それを開くには、メニュー バーで、 **[ビルド]**  >  **[構成マネージャー]** を選択するか、検索ボックスに「**構成**」と入力します。 また、 **[標準]** ツール バーの **[ソリューション構成]** ボックスの一覧を使用して構成を選択することも、 **[構成マネージャー]** を開くこともできます。

![Configuration Manager](media/understanding-build-configurations/config-manager.png)

> [!NOTE]
> ツール バーでソリューション構成設定を見つけることができず、 **[構成マネージャー]** にアクセスできないときは、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 開発設定を適用できます。 詳細については、[Visual Basic 開発者設定が適用された構成を管理する](../ide/how-to-manage-build-configurations-with-visual-basic-developer-settings-applied.md)」を参照してください。

既定では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] テンプレートを使用して作成されたプロジェクトには、 **[デバッグ]** 構成と **[リリース]** 構成が含められます。 **[デバッグ]** 構成ではアプリのデバッグがサポートされ、 **[リリース]** 構成では配置可能なバージョンのアプリがビルドされます。 詳細については、[デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)」を参照してください。 カスタム ソリューション構成とプロジェクト構成を作成することもできます。 詳細については、[構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)」を参照してください。

## <a name="solution-configurations"></a>ソリューション構成

ソリューション構成によって、ソリューション内のプロジェクトをビルドおよび配置する方法が指定されます。 ソリューション構成の変更または新しい構成の定義を行うには、**構成マネージャー**で、 **[アクティブ ソリューション構成]** の **[編集]** または **[新規作成]** を選択します。

ソリューション構成の **[プロジェクトのコンテキスト]** ボックスの各エントリは、ソリューション内のプロジェクトを表します。 **[アクティブ ソリューション構成]** と **[アクティブ ソリューション プラットフォーム]** の組み合わせごとに、各プロジェクトの使用形態を設定できます (ソリューション プラットフォームの詳細については、「[ビルド プラットフォームについて](../ide/understanding-build-platforms.md)」を参照してください)。

新しいソリューション構成を定義して **[新しいプロジェクト構成を作成する]** チェック ボックスをオンにした場合、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、すべてのプロジェクトに新しい構成が自動的に割り当てられます。 同様に、新しいソリューション プラットフォームを定義して **[新しいプロジェクト プラットフォームを作成する]** チェック ボックスをオンにした場合、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、すべてのプロジェクトに新しいプラットフォームが自動的に割り当てられます。 また、新しいプラットフォームを対象とするプロジェクトを追加すると、Visual Studio により、そのプラットフォームがソリューション プラットフォームの一覧に追加され、すべてのプロジェクトに割り当てられます。 その場合も、各プロジェクトの設定は変更できます。

アクティブなソリューション構成には、IDE 用にコンテキストを用意する役割もあります。 たとえば、プロジェクトでの作業中に、プロジェクトがモバイル デバイス用にビルドされるように構成で指定されていると、モバイル デバイス プロジェクトで使用できる項目のみが **[ツールボックス]** に表示されます。

## <a name="project-configurations"></a>プロジェクトの構成

プロジェクトが対象とする構成とプラットフォームは一緒に使用され、そのビルド時に使用されるビルド設定とコンパイラ オプションが指定されます。 プロジェクトは、構成とプラットフォームの組み合わせごとに、異なる設定を持つことができます。 プロジェクトのプロパティを変更するには、**ソリューション エクスプローラー**でそのソリューションのショートカット メニューを開き、 **[プロパティ]** を選択します。  プロジェクト デザイナーの **[ビルド]** タブの上部で、ビルド設定を編集するアクティブな構成を選択します。

![プロジェクト デザイナーの構成](media/understanding-build-configurations/project-designer-configuration.png)

## <a name="building-multiple-configurations"></a>複数の構成のビルド

**[ビルド]**  >  **[ソリューションのビルド]** コマンドを使用してソリューションをビルドする場合、Visual Studio ではアクティブな構成だけがビルドされます。 そのソリューション構成で指定されているすべてのプロジェクトがビルドされます。また、ビルドされるプロジェクト構成は、Visual Studio 内のツールバーに表示されるアクティブ ソリューション構成とアクティブ ソリューション プラットフォームで指定されているものだけです。 たとえば、**Debug** と **x86** です。 その他の定義済みの構成とプラットフォームは、ビルドされません。

1 回の操作で複数の構成とプラットフォームをビルドする場合は、Visual Studio で **[ビルド]**  >  **[バッチ ビルド]** オプションを使用できます。 この機能にアクセスするには、**Ctrl**+**Q** キーを押して検索ボックスを開き、「`Batch build`」と入力します。 バッチ ビルドは、すべてのプロジェクトの種類で使用できるわけではありません。 「[方法:複数の構成を同時にビルドする](how-to-build-multiple-configurations-simultaneously.md)」を参照してください。

## <a name="how-visual-studio-assigns-project-configurations"></a>Visual Studio によるプロジェクト構成の割り当て方法

既存の構成から設定をコピーせずに新しいソリューション構成を定義する場合、Visual Studio では、次の基準を使用して既定のプロジェクト構成が割り当てられます。 基準は、ここに示されている順序で評価されます。

1. プロジェクトに新しいソリューション構成の名前と完全に一致する構成名 ( *\<構成名> \<プラットフォーム名>* ) がある場合は、その構成が割り当てられます。 構成名では大文字と小文字が区別されません。

1. プロジェクトに、 の部分が新しいソリューション構成に一致する構成名がある場合は、 の部分が一致するかどうかに関係なく、その構成が割り当てられます。

1. これらが一致しない場合は、プロジェクトで設定されている最初の構成が割り当てられます。

## <a name="how-visual-studio-assigns-solution-configurations"></a>Visual Studio によるソリューション構成の割り当て方法

プロジェクト構成を作成 (**構成マネージャー**で、プロジェクトの **[構成]** 列のドロップダウン メニューで **[新規作成]** を選択) し、 **[新しいソリューション構成を作成する]** チェック ボックスをオンにした場合、Visual Studio は、サポートする各プラットフォームでプロジェクトをビルドするために、似た名前のソリューション構成を探します。 場合によっては、Visual Studio が既存のソリューション構成名を変更することも、新しいソリューション構成を作成することもあります。

Visual Studio では、次の基準を使用してソリューション構成が割り当てられます。

- プロジェクト構成でプラットフォームが指定されていない場合や、指定されているプラットフォームが 1 つのみの場合は、新しいプロジェクト構成名と一致する名前のソリューション構成が見つかればその構成が割り当てられ、見つからなければ追加されます。 このソリューション構成の既定の名前にはプラットフォーム名が含まれず、 *\<プロジェクトの構成名>* という形式になります。

- プロジェクトで複数のプラットフォームがサポートされる場合、サポートされている各プラットフォームについて、ソリューション構成が見つかればその構成が割り当てられ、見つからなければ追加されます。 各ソリューション構成の名前には、プロジェクト構成名とプラットフォーム名の両方が含まれ、 *\<プロジェクト構成名> \<プラットフォーム名>* という形式になります。

## <a name="see-also"></a>関連項目

- [チュートリアル: アプリケーションを構築する](../ide/walkthrough-building-an-application.md)
- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
- [ソリューションおよびプロジェクト](../ide/solutions-and-projects-in-visual-studio.md)
- [C/C++ ビルドのリファレンス](/cpp/build/reference/c-cpp-building-reference)
- [ビルド プラットフォームについて](understanding-build-platforms.md)
- [ビルド構成 (Visual Studio for Mac)](/visualstudio/mac/configurations)
