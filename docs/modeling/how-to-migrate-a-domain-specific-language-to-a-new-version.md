---
title: '方法: ドメイン固有言語を新バージョンに移行する'
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8bdaea1267d0bf69078aec5739291e72db8dfda
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532612"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>方法: ドメイン固有言語を新バージョンに移行する
[!INCLUDE[vs2010](../misc/includes/vs2010_md.md)]で配布されたバージョンのから、ドメイン固有言語を定義して使用するプロジェクトを移行でき [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] ます。

 移行ツールは、の一部として提供されてい [!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)] ます。 このツールでは、DSL ツールを使用または定義する Visual Studio プロジェクトとソリューションが変換されます。

 移行ツールは、Visual Studio でソリューションを開いたときに自動的に起動されない、明示的に実行する必要があります。 ツールと詳細なガイダンスドキュメントは、次のパスにあります。

 **% Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>DSL プロジェクトを移行する前に
 移行ツールによって、Visual Studio のプロジェクトファイル (**.csproj**) とソリューションファイル (**.sln**) が変更されます。

#### <a name="to-prepare-projects-for-migration"></a>プロジェクトを移行用に準備する。

- **.Csproj**ファイルと **.sln**ファイルを書き込むことができることを確認します。 ソース管理されている場合は、チェックアウトされていることを確認します。

- 移行するフォルダーのコピーを作成します。

## <a name="migrating-a-collection-of-projects"></a>プロジェクトのコレクションの移行

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>DSL プロジェクトとソリューションを Visual Studio 2010 に移行するには

1. DSL 移行ツールを起動します。

   - エクスプローラー (またはエクスプローラー) でツールをダブルクリックするか、コマンドプロンプトからツールを起動できます。 ツールは次の場所にあります。

        **%ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. 変換するソリューションおよびプロジェクトが含まれているフォルダーを選択します。

   - ツールの上部にあるボックスにパスを入力するか、[**参照**] をクリックします。

     移行ツールには、Dsl を定義または使用するプロジェクトのツリーが表示されます。 ツリーには、 **VisualStudio**または**texttemplating**アセンブリを使用するすべてのプロジェクトが含まれます。

3. プロジェクトのツリーを確認し、変換しないプロジェクトをオフにします。

   - プロジェクトまたはソリューションを選択すると、ツールによって行われる変更の一覧が表示されます。

       > [!NOTE]
       > フォルダー名の横に表示されるチェックボックスは無効です。 フォルダーを展開して、プロジェクトとソリューションを検査する必要があります。

4. プロジェクトを変換します。

   1. [**変換**] をクリックします。

        各プロジェクトファイルが変換される前に、vs2008 のコピーが_プロジェクト_**. .csproj**として**保存さ**_れます。_

        各ソリューションのコピー _solution_**。 .sln**は**vs2008**として保存され_ます。_

   2. 報告された失敗した変換を調査します。

        エラーはテキストウィンドウに報告されます。 また、ツリービューでは、変換に失敗した各ノードに赤いフラグが表示されます。 ノードをクリックすると、そのエラーに関する詳細情報を取得できます。

5. 正常に変換されたプロジェクトを含むソリューション内の**すべてのテンプレートを変換**します。

   1. ソリューションを開きます。

   2. ソリューションエクスプローラーのヘッダーにある [**すべてのテンプレートの変換**] ボタンをクリックします。

       > [!NOTE]
       > この手順を不要にすることができます。 詳細については、「[すべてのテンプレートの変換を自動化する方法](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))」を参照してください。

6. 変換されたプロジェクトのカスタムコードを更新します。

   - プロジェクトをビルドし、エラーを調査します。

   - デザイナーをテストします。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>関連項目

- [関連するブログ記事](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)