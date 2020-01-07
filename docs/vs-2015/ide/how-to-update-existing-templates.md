---
title: '方法: 既存のテンプレートを更新する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- item templates, updating existing templates
- Visual Studio templates, updating existing templates
- project templates, updating existing templates
ms.assetid: d585e45b-7fe2-45fa-9cf3-7f2bc060f3c4
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4b56cf11057957b0eb99fc065ed26af10d8adfbd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670583"
---
# <a name="how-to-update-existing-templates"></a>方法 : 既存のテンプレートを更新する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テンプレートを作成し、複数のファイルを .zip ファイルに圧縮した後で、テンプレートを変更できます。 それには、テンプレートのファイルを手動で変更するか、テンプレートに基づいてプロジェクトから新しいテンプレートをエクスポートします。

## <a name="using-the-export-template-wizard-to-update-an-existing-template"></a>テンプレートのエクスポート ウィザードの使用による既存のテンプレートの更新
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] に用意されている**テンプレートのエクスポート** ウィザードを使用すると、既存のテンプレートを更新できます。

#### <a name="to-use-export-template-to-update-an-existing-template"></a>テンプレートのエクスポートを使用して既存のテンプレートを更新するには

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[新しいプロジェクト]** をクリックします。

2. 更新するテンプレートを選択し、一時プロジェクトの名前と場所を入力し、 **[OK]** をクリックします。

3. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でプロジェクトを変更します。

4. **[ファイル]** メニューの **[テンプレートのエクスポート]** をクリックし、**テンプレートのエクスポート** ウィザードを使用して新しいテンプレートを作成します。

5. 更新されたテンプレートが .zip ファイルに圧縮されたら、古いテンプレートの .zip ファイルを削除します。

## <a name="manually-updating-an-existing-template"></a>既存のテンプレートの手動での更新
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の外部で既存のテンプレートを更新するには、圧縮された .zip ファイル内のファイルを変更します。

#### <a name="to-manually-update-an-existing-template"></a>既存のテンプレートを手動で更新するには

1. テンプレートを含む .zip ファイルを探します。 既定では、このファイルは \My Documents\Visual Studio *Version*\My Exported Templates\\ にあります。

2. .zip ファイルを展開します。

3. 現在のテンプレート ファイルを変更または削除するか、テンプレートに新しいファイルを追加します。

4. .vstemplate XML ファイルを開いたり、変更したり、保存したりして、更新された動作または新しいファイルを処理します。 .vstemplate スキーマの詳細については、「[Visual Studio テンプレートのスキーマ参照](../extensibility/visual-studio-template-schema-reference.md)」を参照してください。 ソース ファイルでパラメーター化できる内容の詳細については、「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

5. テンプレート内のファイルを選択して右クリックし、 **[送信]** を選択し、 **[圧縮 (zip 形式) フォルダー]** をクリックします。 選択したファイルは .zip ファイルに圧縮されます。

6. 新しい .zip ファイルを古い .zip ファイルと同じディレクトリに配置します。

7. 抽出したテンプレート ファイルと古いテンプレート .zip ファイルを削除します。

8. ([スタート] メニューの **[Visual Studio 2010]、[Visual Studio Tools]、[開発者コマンド プロンプト]** から) 開発者コマンド プロンプトのインスタンスを (管理者として) 開きます。

9. 次のコマンドを実行します: `devenv /installvstemplates`

## <a name="see-also"></a>参照
 [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md)[プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md) [Visual Studio テンプレートスキーマ参照](../extensibility/visual-studio-template-schema-reference.md)[テンプレートパラメーター](../ide/template-parameters.md) [方法: スタートキットを作成する](../ide/how-to-create-starter-kits.md)
