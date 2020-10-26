---
title: '方法: ドメイン固有言語を新しいバージョンに移行する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6a1ae073-443e-45ca-8bc9-9b944362b449
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 45f7b38f7dbb6ea470b2d9e186dc8e6bf4b33b1e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657329"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>方法: ドメイン固有言語を新バージョンに移行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs2010](../includes/vs2010-md.md)]で配布されたバージョンのから、ドメイン固有言語を定義して使用するプロジェクトを移行でき [!INCLUDE[dsl](../includes/dsl-md.md)] [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] ます。

 移行ツールは、の一部として提供されてい [!INCLUDE[vssdk_current_long](../includes/vssdk-current-long-md.md)] ます。 このツールで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、DSL ツールを使用または定義するプロジェクトとソリューションが変換されます。

 移行ツールは、でソリューションを開いたときに自動的に起動されるのではなく、明示的に実行する必要があり [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 ツールと詳細なガイダンスドキュメントは、次のパスにあります。

 **% Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>DSL プロジェクトを移行する前に
 移行ツールは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトファイル (**.csproj**) とソリューションファイル (**.sln**) を変更します。

#### <a name="to-prepare-projects-for-migration"></a>プロジェクトを移行用に準備する。

- **.Csproj**ファイルと **.sln**ファイルを書き込むことができることを確認します。 ソース管理されている場合は、チェックアウトされていることを確認します。

- 移行するフォルダーのコピーを作成します。

## <a name="migrating-a-collection-of-projects"></a>プロジェクトのコレクションの移行

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>DSL プロジェクトとソリューションを Visual Studio 2010 に移行するには

1. DSL 移行ツールを起動します。

   - エクスプローラー (またはエクスプローラー) でツールをダブルクリックするか、コマンドプロンプトからツールを起動できます。 ツールは次の場所にあります。

        **%ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. 変換するソリューションおよびプロジェクトが含まれているフォルダーを選択します。

   - ツールの上部にあるボックスにパスを入力するか、[ **参照**] をクリックします。

     移行ツールには、Dsl を定義または使用するプロジェクトのツリーが表示されます。 ツリーには、 **VisualStudio** または **texttemplating** アセンブリを使用するすべてのプロジェクトが含まれます。

3. プロジェクトのツリーを確認し、変換しないプロジェクトをオフにします。

   - プロジェクトまたはソリューションを選択すると、ツールによって行われる変更の一覧が表示されます。

       > [!NOTE]
       > フォルダー名の横に表示されるチェックボックスは無効です。 フォルダーを展開して、プロジェクトとソリューションを検査する必要があります。

4. プロジェクトを変換します。

   1. [ **変換**] をクリックします。

        各プロジェクトファイルが変換される前に、vs2008 のコピーが_プロジェクト_**. .csproj**として**保存さ**_れます。_

        各ソリューションのコピー _solution_**。 .sln**は**vs2008**として保存され_ます。_

   2. 報告された失敗した変換を調査します。

        エラーはテキストウィンドウに報告されます。 また、ツリービューでは、変換に失敗した各ノードに赤いフラグが表示されます。 ノードをクリックすると、そのエラーに関する詳細情報を取得できます。

5. 正常に変換されたプロジェクトを含むソリューション内の**すべてのテンプレートを変換**します。

   1. ソリューションを開きます。

   2. ソリューションエクスプローラーのヘッダーにある [ **すべてのテンプレートの変換** ] ボタンをクリックします。

       > [!NOTE]
       > この手順を不要にすることができます。 詳細については、「 [すべてのテンプレートの変換を自動化する方法](https://msdn.microsoft.com/b63cfe20-fe5e-47cc-9506-59b29bca768a)」を参照してください。

6. 変換されたプロジェクトのカスタムコードを更新します。

   - プロジェクトをビルドし、エラーを調査します。

   - デザイナーをテストします。

## <a name="see-also"></a>参照
 [Visualization and Modeling SDK の新機能](../misc/what-s-new-in-visualization-and-modeling-sdk.md)
