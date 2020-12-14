---
title: プロジェクトと項目のカスタム テンプレートの作成 | Microsoft Docs
description: Visual Studio SDK のテンプレート作成テンプレートを使用して、テンプレートをより大きな拡張機能に含める方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: overview
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 78770c74e5b866ad6791db01a448d46231edfd2a
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915623"
---
# <a name="create-custom-project-and-item-templates"></a>プロジェクトと項目のカスタム テンプレートを作成する

Visual Studio SDK には、カスタム プロジェクト テンプレートとカスタム項目テンプレートを作成するプロジェクト テンプレートが含まれています。 これらのテンプレートには、いくつかの一般的なパラメーター置換や、zip ファイルとしてのビルドが含まれます。 自動的には展開されず、実験用インスタンスでは使用できません。 生成された zip ファイルをユーザー テンプレート ディレクトリにコピーする必要があります。

テンプレート作成テンプレートを使用すると、より大きな拡張機能にテンプレートを含めることができます。 これにより、ソース ファイルにバージョン コントロールを実装し、テンプレート プロジェクトのグループを 1 つの VSIX パッケージに組み込むことができます。

NuGet パッケージをインストールするようにテンプレートを構成することもできます。 詳細については、[Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)に関する記事を参照してください。

基本的なテンプレート作成シナリオでは、**エクスポート テンプレート** ウィザードを使用して、圧縮ファイルに出力します。 基本的なテンプレート作成の詳細については、[プロジェクトと項目のテンプレートの作成](../ide/creating-project-and-item-templates.md)に関する記事を参照してください。

> [!NOTE]
> Visual Studio 2017 以降では、プロジェクトと項目のカスタム テンプレートのスキャンは実行されなくなりました。 代わりに、拡張機能で、これらのテンプレートのインストール場所を記述するテンプレート マニフェスト ファイルを提供する必要があります。 Visual Studio 2017 を使用して VSIX 拡張機能を更新できます。 MSI を使用して拡張機能を展開する場合は、テンプレート マニフェスト ファイルを手動で生成する必要があります。 詳細については、[プロジェクトおよび項目のカスタム テンプレートの Visual Studio 2017 へのアップグレード](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)に関する記事を参照してください。 テンプレート マニフェスト スキーマについては、「[Visual Studio テンプレート マニフェスト スキーマ リファレンス](../extensibility/visual-studio-template-manifest-schema-reference.md)」で説明されています。

## <a name="create-a-project-template"></a>プロジェクト テンプレートを作成する

1. プロジェクト テンプレート プロジェクトを作成します。 プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「プロジェクト テンプレート」と検索し、C# または Visual Basic のバージョンを選択すると検索できます。

     このテンプレートでは、クラス ファイル、アイコン、 *.vstemplate* ファイル、*ProjectTemplate.vbproj* または *ProjectTemplate.csproj* という名前の編集可能なプロジェクト ファイル、そして通常は他のプロジェクトの種類によって生成されるファイル (*resources.resx* ファイル、*AssemblyInfo* ファイル、 *.settings* ファイルなど) が生成されます。 各コード ファイルには、必要に応じて一般的なパラメーター置換が含まれています。

![プロジェクト テンプレート プロジェクトの選択](media/project-template-selection.png)

2. プロジェクトの必要に応じて、プロジェクトの項目を追加および削除します。 編集可能なプロジェクトファイル、*AssemblyInfo* ファイル、または *.vstemplate* ファイルは削除しないでください。

3. 追加と削除が反映されるように *.vstemplate* ファイルを更新します。 [Project](../extensibility/project-element-visual-studio-templates.md) 要素には、テンプレートに含める各ファイルの [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) 要素が含まれている必要があります。

4. コード ファイルやその他のユーザー向けコンテンツを変更し、適切なパラメーター置換を追加します。

5. 生成されたコンテンツを必要に応じて変更します。

6. プロジェクトをビルドします。

     Visual Studio によって、テンプレートを含む *.zip* ファイルが作成されます。 これは展開されないため、実験用インスタンスでは使用できません。

## <a name="create-an-item-template"></a>項目テンプレートを作成する

1. 項目テンプレート プロジェクトを作成します。

     このテンプレートでは、クラス ファイル、アイコン、 *.vstemplate* ファイル、および *AssemblyInfo* ファイルが生成されます。 クラス ファイルには、一般的なパラメーター置換がいくつか含まれています。

2. プロジェクトの必要に応じて、プロジェクトの項目を追加および削除します。

3. 追加と削除が反映されるように *.vstemplate* ファイルを更新します。 [Project](../extensibility/project-element-visual-studio-templates.md) 要素には、テンプレートに含める各ファイルの [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) 要素が含まれている必要があります。

4. コード ファイルやその他のユーザー向けコンテンツを変更し、適切なパラメーター置換を追加します。

5. 生成されたコンテンツを必要に応じて変更します。

6. プロジェクトをビルドします。

     Visual Studio によって、テンプレートを含む圧縮ファイルが作成されます。 これは展開されないため、実験用インスタンスでは使用できません。

## <a name="deployment"></a>デプロイ

### <a name="to-deploy-the-project-or-item-template"></a>プロジェクトまたは項目テンプレートを配置するには

1. VSIX プロジェクトを作成する。 詳細については、「[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

2. VSIX プロジェクトをスタートアップ プロジェクトとして設定します。 **ソリューション エクスプローラー** で VSIX プロジェクト ノードを選択し、 **[スタートアップ プロジェクトに設定]** を選びます。

3. プロジェクト テンプレート プロジェクトを VSIX プロジェクトのアセットとして設定します。 *.vsixmanifest* ファイルを開きます。 **[アセット]** タブに移動して、 **[新規]** を選択します。

    1. **[種類]** フィールドを **Microsoft.VisualStudio.ProjectTemplate** または **Microsoft.VisualStudio.ItemTemplate** に設定します。

    2. ソースに、 **[現在のソリューション内のプロジェクト]** オプションを選択し、テンプレートが含まれているプロジェクトを選択します。

4. ソリューションをビルドして、**F5** キーを押します。 実験用インスタンスが表示されます。

5. プロジェクト テンプレート プロジェクトの場合、 **[新しいプロジェクト]** ダイアログ ( **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** ) の Visual C# または Visual Basic ノードにプロジェクト テンプレートが一覧表示されます。 項目テンプレート プロジェクトの場合は、項目テンプレートが **[新しい項目の追加]** ダイアログに一覧表示されます。 **[新しい項目の追加]** ダイアログを表示するには、**ソリューション エクスプローラー** からプロジェクト ノードを選択し、 **[追加]**  >  **[新しい項目]** を選択します。

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート参照](../ide/creating-project-and-item-templates.md)
- [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)
