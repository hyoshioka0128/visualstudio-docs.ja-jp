---
title: カスタム プロジェクトテンプレートと項目テンプレートの作成 |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ae404004f2660048ef7581a661d8f785495ed95a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739456"
---
# <a name="create-custom-project-and-item-templates"></a>カスタム プロジェクトテンプレートと項目テンプレートを作成する

Visual Studio SDK には、カスタム プロジェクト テンプレートとカスタム項目テンプレートを作成するプロジェクト テンプレートが含まれています。 これらのテンプレートには、いくつかの一般的なパラメーター置換と、zip ファイルとしてのビルドが含まれています。 これらは自動的にデプロイされず、実験用インスタンスでは使用できません。 生成された zip ファイルをユーザーテンプレートディレクトリにコピーする必要があります。

テンプレート作成テンプレートを使用すると、より大きな拡張機能にテンプレートを含めることができます。 これにより、ソース ファイルにバージョン管理を実装し、テンプレート プロジェクトのグループを 1 つの VSIX パッケージにビルドできます。

NuGet パッケージをインストールするテンプレートを構成することもできます。 詳細については、「 [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)」を参照してください。

基本的なテンプレート作成シナリオでは、圧縮ファイルに出力する**テンプレートのエクスポート**ウィザードを使用する必要があります。 基本的なテンプレート作成の詳細については、「[プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)」を参照してください。

> [!NOTE]
> Visual Studio 2017 以降、カスタム プロジェクトと項目テンプレートのスキャンは実行されなくなります。 代わりに、拡張機能は、これらのテンプレートのインストール場所を記述するテンプレート マニフェスト ファイルを提供する必要があります。 Visual Studio 2017 を使用して、VSIX 拡張機能を更新できます。 MSI を使用して拡張機能を展開する場合は、テンプレート マニフェスト ファイルを手入力で生成する必要があります。 詳細については、「 [Visual Studio 2017 のカスタム プロジェクトテンプレートと項目テンプレートのアップグレード](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)」を参照してください。 テンプレート マニフェスト スキーマについては、「 [Visual Studio テンプレート マニフェスト スキーマ リファレンス](../extensibility/visual-studio-template-manifest-schema-reference.md)」に記載されています。

## <a name="create-a-project-template"></a>プロジェクト テンプレートを作成する

1. プロジェクト テンプレート プロジェクトを作成します。 プロジェクト テンプレートは、[**新しいプロジェクト**] ダイアログ で検索できます。

     テンプレートは、クラス ファイル、アイコン *、.vstemplate*ファイル *、ProjectTemplate.vbproj*または*ProjectTemplate.csproj*という名前の編集可能なプロジェクト ファイル、および他の種類のプロジェクトで通常生成されるいくつかのファイル *(resources.resx*ファイル *、AssemblyInfo*ファイル、*および .settings*ファイル) を生成します。 各コード ファイルには、必要に応じて共通のパラメーター置換が含まれています。

![プロジェクト テンプレート プロジェクトの選択](media/project-template-selection.png)

2. プロジェクトに必要な項目を追加および削除します。 編集可能なプロジェクト ファイル *、AssemblyInfo*ファイル、または *.vstemplate*ファイルは削除しないでください。

3. 追加および削除を反映するように *.vstemplate*ファイルを更新します。 [プロジェクト](../extensibility/project-element-visual-studio-templates.md)要素には、テンプレートに含める各ファイルの[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)要素が含まれている必要があります。

4. コード ファイルおよびその他のユーザー向けコンテンツを変更し、適切なパラメーター置換を追加します。

5. 必要に応じて、生成されたコンテンツを変更します。

6. プロジェクトをビルドします。

     テンプレートを含む *.zip*ファイルが作成されます。 これは展開されず、実験用インスタンスでは使用できません。

## <a name="create-an-item-template"></a>項目テンプレートを作成する

1. 項目テンプレート プロジェクトを作成します。

     テンプレートは、クラス ファイル、アイコン *、.vstemplate*ファイル、および*AssemblyInfo*ファイルを生成します。 クラス ファイルには、いくつかの一般的なパラメーター置換が含まれています。

2. プロジェクトに必要な項目を追加および削除します。

3. 追加および削除を反映するように *.vstemplate*ファイルを更新します。 [プロジェクト](../extensibility/project-element-visual-studio-templates.md)要素には、テンプレートに含める各ファイルの[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)要素が含まれている必要があります。

4. コード ファイルおよびその他のユーザー向けコンテンツを変更し、適切なパラメーター置換を追加します。

5. 生成されたコンテンツを必要に応じて変更します。

6. プロジェクトをビルドします。

     テンプレートを含む圧縮ファイルが作成されます。 これは展開されず、実験用インスタンスでは使用できません。

## <a name="deployment"></a>デプロイ

### <a name="to-deploy-the-project-or-item-template"></a>プロジェクトまたは項目テンプレートを配置するには

1. VSIX プロジェクトを作成する。 詳細については[、「VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

2. VSIX プロジェクトをスタートアップ プロジェクトとして設定します。 ソリューション**エクスプローラ**で、VSIX プロジェクト ノードを選択し、右クリックして **[スタートアップ プロジェクトに設定**] を選択します。

3. プロジェクト テンプレート プロジェクトを VSIX プロジェクトのアセットとして設定します。 *.vsixmanifest*ファイルを開きます。 [**資産**] タブに移動し、[**新規作成**] をクリックします。

    1. **フィールド**を**に設定します****。**

    2. [ソース] で 、[**現在のソリューションのプロジェクト**] オプションを選択し、テンプレートを含むプロジェクトを選択します。

4. ソリューションをビルドし **、F5**キーを押します。 実験用インスタンスが表示されます。

5. プロジェクト テンプレート プロジェクトの場合は、Visual C# または Visual Basic ノードに、プロジェクト テンプレートが **[新しいプロジェクト**] ダイアログ (**[ファイル]** > **[ 新しい** > **プロジェクト**] ) に表示されます。 項目テンプレート プロジェクトの場合は、[**新しい**項目の追加] ダイアログに項目テンプレートが一覧表示されます。 [**新しい項目の追加]** ダイアログを表示するには、**ソリューション エクスプローラ**でプロジェクト ノードを選択し、[**新しい項目**の**追加** > ] をクリックします。

## <a name="see-also"></a>関連項目

- [ビジュアル スタジオ テンプレート リファレンス](../ide/creating-project-and-item-templates.md)
- [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)
