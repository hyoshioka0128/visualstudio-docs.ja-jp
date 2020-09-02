---
title: カスタム プロジェクト テンプレートと項目テンプレートの作成
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
caps.latest.revision: 11
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c6875e13baa83d349020f50a3fe448a87ec5fd30
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197402"
---
# <a name="creating-custom-project-and-item-templates"></a>カスタム プロジェクト テンプレートと項目テンプレートの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio SDK には、カスタムプロジェクトテンプレートとカスタム項目テンプレートを作成するプロジェクトテンプレートが含まれています。 これらのテンプレートには、いくつかの一般的なパラメーター置換や、zip ファイルとしてのビルドが含まれます。 自動的には展開されず、実験用インスタンスでは使用できません。 Zip ファイルを自分の場所にコピーします。

テンプレート作成テンプレートを使用すると、より大きな拡張機能にテンプレートを含めることができます。 拡張機能にテンプレートを含めると、ソースファイルにバージョンコントロールを実装し、テンプレートプロジェクトのグループを1つの VSIX パッケージに組み込むことができます。

基本的なテンプレート作成シナリオでは、**エクスポート テンプレート** ウィザードを使用して、圧縮ファイルに出力します。 基本的なテンプレート作成の詳細については、「 [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)」を参照してください。

Visual Studio 2017 以降では、カスタムプロジェクトと項目テンプレートのスキャンは実行されなくなりました。 代わりに、拡張機能で、これらのテンプレートのインストール場所を記述するテンプレート マニフェスト ファイルを提供する必要があります。 Preview 2 インストールを使用して、VSIX 拡張機能を更新できます。 MSI を使用して拡張機能を展開する場合は、テンプレート マニフェスト ファイルを手動で生成する必要があります。 詳細については、「 [Upgrade Custom Visual Studio のプロジェクトと項目テンプレート 2017](/visualstudio/extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017?view=vs-2015)」を参照してください。 テンプレートマニフェストスキーマは、「 [Visual Studio テンプレートマニフェストスキーマリファレンス](/visualstudio/extensibility/visual-studio-template-manifest-schema-reference)」に記載されています。

## <a name="create-a-project-template"></a>プロジェクトテンプレートを作成する

1. プロジェクト テンプレート プロジェクトを作成します。 プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログの [Visual Basic] または [Visual C# の **機能拡張** ] フォルダーで見つけることができます。

     このテンプレートでは、クラス ファイル、アイコン、 .vstemplate ファイル、ProjectTemplate.vbproj または ProjectTemplate.csproj という名前の編集可能なプロジェクト ファイル、そして通常は他のプロジェクトの種類によって生成されるファイル (resources.resx ファイル、AssemblyInfo ファイル、 .settings ファイルなど) が生成されます。 各コード ファイルには、必要に応じて一般的なパラメーター置換が含まれています。

2. プロジェクトの必要に応じて、プロジェクトの項目を追加および削除します。 編集可能なプロジェクトファイル、AssemblyInfo ファイル、または .vstemplate ファイルは削除しないでください。

3. 追加と削除が反映されるように .vstemplate ファイルを更新します。 [Project](../extensibility/project-element-visual-studio-templates.md) 要素には、テンプレートに含める各ファイルの [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) 要素が含まれている必要があります。

4. コード ファイルやその他のユーザー向けコンテンツを変更し、適切なパラメーター置換を追加します。

5. 生成されたコンテンツを必要に応じて変更します。

6. プロジェクトをビルドします。

     Visual Studio によって、テンプレートを含む .zip ファイルが作成されます。 これは展開されないため、実験用インスタンスでは使用できません。

## <a name="create-an-item-template"></a>項目テンプレートを作成する

1. 項目テンプレート プロジェクトを作成します。

     このテンプレートでは、クラス ファイル、アイコン、 .vstemplate ファイル、および AssemblyInfo ファイルが生成されます。 クラス ファイルには、一般的なパラメーター置換がいくつか含まれています。

2. プロジェクトの必要に応じて、プロジェクトの項目を追加および削除します。

3. 追加と削除が反映されるように .vstemplate ファイルを更新します。 [Project](../extensibility/project-element-visual-studio-templates.md) 要素には、テンプレートに含める各ファイルの [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) 要素が含まれている必要があります。

4. コード ファイルやその他のユーザー向けコンテンツを変更し、適切なパラメーター置換を追加します。

5. 生成されたコンテンツを必要に応じて変更します。

6. プロジェクトをビルドします。

     Visual Studio によって、テンプレートを含む圧縮ファイルが作成されます。 これは展開されないため、実験用インスタンスでは使用できません。

## <a name="deploy-the-project-or-item-template"></a>プロジェクトまたは項目テンプレートを配置する

1. VSIX プロジェクトを作成する。 詳細については、「 [VSIX プロジェクトテンプレート](../extensibility/vsix-project-template.md)」を参照してください。

2. VSIX プロジェクトをスタートアップ プロジェクトとして設定します。 **ソリューション エクスプローラー**で VSIX プロジェクト ノードを選択し、 **[スタートアップ プロジェクトに設定]** を選びます。

3. プロジェクト テンプレート プロジェクトを VSIX プロジェクトのアセットとして設定します。 .vsixmanifest ファイルを開きます。 [ **アセット** ] タブにアクセスし、[ **新規**] をクリックします。

    1. **[種類]** フィールドを **Microsoft.VisualStudio.ProjectTemplate** または **Microsoft.VisualStudio.ItemTemplate** に設定します。

    2. ソースに、 **[現在のソリューション内のプロジェクト]** オプションを選択し、テンプレートが含まれているプロジェクトを選択します。

4. ソリューションをビルドして、F5 キーを押します。 実験用インスタンスが表示されます。

5. プロジェクトテンプレートプロジェクトの場合は、[Visual C#] ノードまたは [Visual Basic] ノードの [ **新しいプロジェクト** ] ダイアログ ([ファイル]、[**新規作成**]、[プロジェクト]) にプロジェクトテンプレートが表示されます。 項目テンプレートプロジェクトの場合は、[新しい項目の追加] ダイアログボックスに項目テンプレートが表示されます ( **ソリューションエクスプローラー**で、プロジェクトノードを選択し、[追加]、[ **新しい項目**] の順にクリックします)。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio テンプレートリファレンス](../ide/visual-studio-template-reference.md)