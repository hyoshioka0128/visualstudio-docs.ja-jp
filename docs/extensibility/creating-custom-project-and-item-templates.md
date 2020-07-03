---
title: カスタムプロジェクトテンプレートと項目テンプレートを作成する |Microsoft Docs
ms.date: 3/16/2019
ms.topic: overview
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c702aaaa51d86e2b8aac18a6b55201be03a635f
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903317"
---
# <a name="create-custom-project-and-item-templates"></a>カスタムプロジェクトと項目テンプレートの作成

Visual Studio SDK には、カスタムプロジェクトテンプレートとカスタム項目テンプレートを作成するプロジェクトテンプレートが含まれています。 これらのテンプレートには、いくつかの一般的なパラメーターの置換や、zip ファイルとしてのビルドが含まれます。 これらは自動的には展開されず、実験用インスタンスでは使用できません。 生成された zip ファイルをユーザーテンプレートディレクトリにコピーする必要があります。

テンプレート作成テンプレートを使用すると、より大きな拡張機能にテンプレートを含めることができます。 これにより、ソースファイルにバージョンコントロールを実装し、テンプレートプロジェクトのグループを1つの VSIX パッケージに組み込むことができます。

NuGet パッケージをインストールするようにテンプレートを構成することもできます。 詳細については、「 [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)」を参照してください。

テンプレートの基本的な作成シナリオでは、圧縮ファイルに出力する**テンプレートのエクスポート**ウィザードを使用する必要があります。 基本的なテンプレート作成の詳細については、「[プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)」を参照してください。

> [!NOTE]
> Visual Studio 2017 以降では、カスタムプロジェクトと項目テンプレートのスキャンは実行されなくなりました。 代わりに、拡張機能は、これらのテンプレートのインストール場所を記述するテンプレートマニフェストファイルを提供する必要があります。 Visual Studio 2017 を使用して、VSIX 拡張機能を更新できます。 MSI を使用して拡張機能を展開する場合は、テンプレートマニフェストファイルを手動で生成する必要があります。 詳細については、「 [Visual Studio 2017 のカスタムプロジェクトおよび項目テンプレートのアップグレード](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)」を参照してください。 テンプレートマニフェストスキーマは、「 [Visual Studio テンプレートマニフェストスキーマリファレンス](../extensibility/visual-studio-template-manifest-schema-reference.md)」に記載されています。

## <a name="create-a-project-template"></a>プロジェクト テンプレートを作成する

1. プロジェクトテンプレートプロジェクトを作成します。 [**新しいプロジェクト**] ダイアログで [プロジェクトテンプレート] を検索し、C# または Visual Basic バージョンのいずれかを選択することで、プロジェクトテンプレートを見つけることができます。

     このテンプレートは、クラスファイル、アイコン、 *.vstemplate*ファイル、 *projecttemplate .Vbproj*または*projecttemplate .csproj*という名前の編集可能なプロジェクトファイル、および他の種類のプロジェクト (*リソース .resx*ファイル、 *AssemblyInfo*ファイル、および*設定*ファイルなど) によって通常生成されるファイルを生成します。 各コードファイルには、必要に応じて共通のパラメーター置換が含まれています。

![プロジェクトテンプレートプロジェクトの選択](media/project-template-selection.png)

2. プロジェクトの必要に応じて、プロジェクトの項目を追加および削除します。 編集可能なプロジェクトファイル、 *AssemblyInfo*ファイル、または *.vstemplate*ファイルは削除しないでください。

3. 追加と削除を反映するように *.vstemplate*ファイルを更新します。 [プロジェクト](../extensibility/project-element-visual-studio-templates.md)要素には、テンプレートに含める各ファイルの[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)要素が含まれている必要があります。

4. コードファイルやその他のユーザー向けコンテンツを変更し、適切なパラメーター置換を追加します。

5. 生成されたコンテンツを必要に応じて変更します。

6. プロジェクトをビルドします。

     テンプレートを含む *.zip*ファイルが Visual Studio によって作成されます。 これはデプロイされておらず、実験用インスタンスでは使用できません。

## <a name="create-an-item-template"></a>項目テンプレートを作成する

1. 項目テンプレートプロジェクトを作成します。

     このテンプレートは、クラスファイル、アイコン、 *.vstemplate*ファイル、および*AssemblyInfo*ファイルを生成します。 クラスファイルには、一般的なパラメーターの置換がいくつか含まれています。

2. プロジェクトの必要に応じて、プロジェクトの項目を追加および削除します。

3. 追加と削除を反映するように *.vstemplate*ファイルを更新します。 [プロジェクト](../extensibility/project-element-visual-studio-templates.md)要素には、テンプレートに含める各ファイルの[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)要素が含まれている必要があります。

4. コードファイルやその他のユーザー向けコンテンツを変更し、適切なパラメーター置換を追加します。

5. 生成されたコンテンツを必要に応じて変更します。

6. プロジェクトをビルドします。

     Visual Studio によって、テンプレートを含む圧縮ファイルが作成されます。 これはデプロイされておらず、実験用インスタンスでは使用できません。

## <a name="deployment"></a>デプロイ

### <a name="to-deploy-the-project-or-item-template"></a>プロジェクトまたは項目テンプレートを配置するには

1. VSIX プロジェクトを作成する。 詳細については、「 [VSIX プロジェクトテンプレート](../extensibility/vsix-project-template.md)」を参照してください。

2. VSIX プロジェクトをスタートアッププロジェクトとして設定します。 **ソリューションエクスプローラー**で、[VSIX プロジェクト] ノードを選択し、右クリックし**て [スタートアッププロジェクトに設定**] を選択します。

3. プロジェクトテンプレートプロジェクトを VSIX プロジェクトのアセットとして設定します。 *Source.extension.vsixmanifest*ファイルを開きます。 [**アセット**] タブにアクセスし、[**新規**] をクリックします。

    1. [**種類**] フィールドを**VisualStudio**または**VisualStudio**に設定します。

    2. [ソース] で、[**現在のソリューション内のプロジェクト**] オプションを選択し、テンプレートが含まれているプロジェクトを選択します。

4. ソリューションをビルドし、 **F5**キーを押します。 実験用インスタンスが表示されます。

5. プロジェクトテンプレートプロジェクトの場合は、[**新しいプロジェクト**] ダイアログ ([**ファイル**] [  >  **新しい**  >  **プロジェクト**]) の [Visual C#] ノードまたは [Visual Basic] ノードにプロジェクトテンプレートが表示されます。 項目テンプレートプロジェクトの場合は、[**新しい項目の追加**] ダイアログボックスに項目テンプレートが表示されます。 [**新しい項目の追加**] ダイアログを表示するには、**ソリューションエクスプローラー**からプロジェクトノードを選択し、[新しい項目の**追加**] をクリックし  >  **New Item**ます。

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレートリファレンス](../ide/creating-project-and-item-templates.md)
- [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)
