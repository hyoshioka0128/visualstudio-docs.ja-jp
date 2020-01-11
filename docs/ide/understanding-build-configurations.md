---
title: ビルド構成について
ms.date: 11/04/2016
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 21421776506868942e9dc562db4f456c2012fce7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592023"
---
# <a name="understand-build-configurations"></a>ビルド構成について

異なる種類のビルドに使用できるように、ソリューションおよびプロジェクト プロパティの異なる構成を保存することができます。 構成を作成、選択、変更、または削除するには、**構成マネージャー**を使用できます。 それを開くには、メニュー バーで、 **[ビルド]**  >  **[構成マネージャー]** を選択するか、検索ボックスに「**構成**」と入力します。 また、 **[標準]** ツール バーの **[ソリューション構成]** ボックスの一覧を使用して構成を選択することも、 **[構成マネージャー]** を開くこともできます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac でのビルド構成](/visualstudio/mac/configurations)に関するページを参照してください。

> [!NOTE]
> ツール バーでソリューション構成設定を見つけることができず、 **[構成マネージャー]** にアクセスできないときは、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 開発設定を適用できます。 詳細については、[Visual Basic 開発者設定が適用された構成を管理する](../ide/how-to-manage-build-configurations-with-visual-basic-developer-settings-applied.md)」を参照してください。

既定では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] テンプレートを使用して作成されたプロジェクトには、デバッグ構成とリリース構成が含まれます。 デバッグ構成ではアプリのデバッグがサポートされ、リリース構成では展開可能なバージョンのアプリがビルドされます。 詳細については、[デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)」を参照してください。 カスタム ソリューション構成とプロジェクト構成を作成することもできます。 詳細については、[構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)」を参照してください。

## <a name="solution-configurations"></a>ソリューション構成

ソリューション構成によって、ソリューション内のプロジェクトをビルドおよび配置する方法が指定されます。 ソリューション構成の変更または新しい構成の定義を行うには、**構成マネージャー**で、 **[アクティブ ソリューション構成]** の **[編集]** または **[新規作成]** を選択します。

ソリューション構成の **[プロジェクトのコンテキスト]** ボックスの各エントリは、ソリューション内のプロジェクトを表します。 **[アクティブ ソリューション構成]** と **[アクティブ ソリューション プラットフォーム]** の組み合わせごとに、各プロジェクトの使用形態を設定できます (ソリューション プラットフォームの詳細については、「[ビルド プラットフォームについて](../ide/understanding-build-platforms.md)」を参照してください)。

> [!NOTE]
> 新しいソリューション構成を定義して **[新しいプロジェクト構成を作成する]** チェック ボックスをオンにした場合、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、すべてのプロジェクトに新しい構成が自動的に割り当てられます。 同様に、新しいソリューション プラットフォームを定義して **[新しいプロジェクト プラットフォームを作成する]** チェック ボックスをオンにした場合、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、すべてのプロジェクトに新しいプラットフォームが自動的に割り当てられます。 また、新しいプラットフォームを対象とするプロジェクトを追加すると、Visual Studio により、そのプラットフォームがソリューション プラットフォームの一覧に追加され、すべてのプロジェクトに割り当てられます。
>
> その場合も、各プロジェクトの設定は変更できます。

アクティブなソリューション構成には、IDE 用にコンテキストを用意する役割もあります。 たとえば、プロジェクトでの作業中に、プロジェクトがモバイル デバイス用にビルドされるように構成で指定されていると、モバイル デバイス プロジェクトで使用できる項目のみが **[ツールボックス]** に表示されます。

## <a name="project-configurations"></a>プロジェクトの構成
プロジェクトが対象とする構成とプラット フォームは、プロジェクトのビルド時に使用されるプロパティを指定するために一緒に使用されます。 構成とプラットフォームの各組み合わせには、別々のプロパティ定義セットを設定することができます。 プロジェクトのプロパティを変更するには、そのプロジェクトのプロパティ ページを使用します (**ソリューション エクスプローラー**で、プロジェクトのショートカット メニューを開き、 **[プロパティ]** をクリックします)。

各プロジェクト構成について、構成依存のプロパティを必要に応じて定義できます。 たとえば、特定のビルドについて、含めるプロジェクト項目、作成する出力ファイルとその配置場所、ビルドの最適化方法などを設定できます。

それぞれのプロジェクト構成は、かなりの違いが生じる場合があります。 たとえば、構成のプロパティによって、出力ファイルを最適化して使用領域を最小限に抑えることも、実行可能ファイルが最大速度で実行されるように指定することもできます。

プロジェクト構成は、チームで共有できるように、ユーザー別ではなくソリューション別に格納されます。

プロジェクトの依存関係は構成に依存しませんが、アクティブなソリューション構成で指定されているプロジェクトだけがビルドされます。

## <a name="how-visual-studio-assigns-project-configurations"></a>Visual Studio によるプロジェクト構成の割り当て方法
既存の構成から設定をコピーせずに新しいソリューション構成を定義する場合、Visual Studio では、次の基準を使用して既定のプロジェクト構成が割り当てられます。 基準は、ここに示されている順序で評価されます。

1. プロジェクトに新しいソリューション構成の名前と完全に一致する構成名 ( *\<構成名> \<プラットフォーム名>* ) がある場合は、その構成が割り当てられます。 構成名では大文字と小文字が区別されません。

2. プロジェクトに、 の部分が新しいソリューション構成に一致する構成名がある場合は、 の部分が一致するかどうかに関係なく、その構成が割り当てられます。

3. これらが一致しない場合は、プロジェクトで設定されている最初の構成が割り当てられます。

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
- [Devenv コマンド ライン スイッチ](../ide/reference/devenv-command-line-switches.md)
- [ビルド構成 (Visual Studio for Mac)](/visualstudio/mac/configurations)
