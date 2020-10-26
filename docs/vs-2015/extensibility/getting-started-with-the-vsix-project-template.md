---
title: VSIX プロジェクトテンプレートを使用してはじめに |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, VSIX project template
ms.assetid: 89fac33e-9380-4723-9b45-048a6e16f0ed
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cc3f461c9e7dbdea1fd8481594292a0a247d2173
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204297"
---
# <a name="getting-started-with-the-vsix-project-template"></a>VSIX プロジェクト テンプレートの概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSIX プロジェクトテンプレートを使用して、拡張機能を作成したり、配置のための既存の拡張機能をパッケージ化したりできます。 VSIX プロジェクトテンプレートには Visual Basic と Visual C# の両方のバージョンがあり、Visual Studio SDK の一部としてインストールされます。  
  
 VSIX プロジェクトテンプレートは、source.extension.vsixmanifest ファイルで構成されています。このファイルには、拡張機能とそれに付属する資産に関する情報が含まれています。  
  
 VSIX プロジェクトテンプレートを見つけるには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。  
  
## <a name="deploying-a-custom-project-template-using-the-vsix-project-template"></a>VSIX プロジェクトテンプレートを使用したカスタムプロジェクトテンプレートの配置  
 次の手順では、VSIX プロジェクトを使用して、他の開発者と共有したり、Visual Studio ギャラリーにアップロードしたりできるプロジェクトテンプレートをパッケージ化する方法について説明します。  
  
1. プロジェクトテンプレートを作成します。  
  
    1. テンプレートを作成するプロジェクトを開きます。 このプロジェクトは、任意の種類のプロジェクトにすることができます。  
  
    2. **[ファイル]** メニューの **[テンプレートのエクスポート]** をクリックします。 ウィザードの手順を完了します。  
  
         %USERPROFILE%\My Documents\Visual Studio \My にエクスポートされたテンプレートに .zip ファイルが作成されます。 *\<version>* \\  
  
2. 空の VSIX プロジェクトを作成します。  
  
     **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。 **Visual Basic**または**Visual C#** のいずれかを選択します。 選択したノードの下で [ **機能拡張**] を選択し、[ **VSIX プロジェクト**] を選択します。  
  
3. プロジェクトに .zip ファイルを追加します。 " **出力ディレクトリにコピー** " プロパティをに設定 `Copy Always` します。  
  
4. **ソリューションエクスプローラー**で、ファイルをダブルクリックし `source.extension.vsixmanifest` て**VSIX マニフェストデザイナー**で開き、次のように変更します。  
  
    - [ **製品名** ] フィールドを **[マイプロジェクトテンプレート**] に設定します。  
  
    - [ **PRODUCT ID** ] フィールドを **myprojecttemplate-1**に設定します。  
  
    - [ **作成者** ] フィールドを **Fabrikam**に設定します。  
  
    - [ **説明** ] フィールドを **[マイプロジェクトテンプレート**] に設定します。  
  
    - [ **Assets** ] セクションで、 **VisualStudio** 型を追加し、そのパスを .zip ファイルの名前に設定します。  
  
5. Source.extension.vsixmanifest ファイルを保存して閉じます。  
  
6. プロジェクトをビルドします。  
  
7. 出力ディレクトリで、.vsix ファイルをダブルクリックします。  
  
8. **VSIX インストーラー**のメッセージボックスが表示されます。 指示に従って拡張機能をインストールします。  
  
9. Visual Studio を閉じてから、再度開きます。  
  
10. [**ツール**] メニューの [**拡張機能と更新プログラム**] を選択し、[**テンプレート**] カテゴリを選択します。 使用可能な拡張機能の1つは、 **自分のプロジェクトテンプレート**です。  
  
11. 新しいプロジェクトテンプレートは、元のプロジェクトテンプレートと同じ場所にある [ **新しいプロジェクト** ] ダイアログに表示されます。 たとえば、Visual Basic コンソールアプリケーションから **Vb コンソール** という名前のテンプレートを作成した場合、 **vb コンソール** は、Visual Basic **コンソールアプリケーション** テンプレートと同じウィンドウに表示されます。  
  
#### <a name="to-specify-the-location-of-the-template-in-the-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログボックスでテンプレートの場所を指定するには  
  
1. テンプレートフォルダーは、 *Visual studio のインストールパス*\Common7\IDE\ProjectTemplates と *Visual studio インストールパス*\Common7\IDE\ItemTemplates ディレクトリにあります。 [新しいプロジェクト] ダイアログボックスの最上位レベルのセクションの名前は、テンプレートフォルダーの名前と完全には一致しません。 違いがある場合は、テンプレートフォルダーの名前を使用します。  
  
     .Vsix ファイル拡張子を .zip に変更し、ファイルを開きます。  
  
2. [新しいプロジェクト] ダイアログボックスのセクションと同じ名前の新しいフォルダーを作成します。  
  
3. テンプレートがサブセクションに表示される場合は、同じ名前のサブフォルダーを作成します。  
  
4. テンプレートの .zip ファイルを新しいフォルダーに移動します。  
  
5. .Zip 拡張子を .vsix に変更します。  
  
6. VSIX マニフェストを開きます。  
  
7. VSIX マニフェストで、テンプレートファイルを含むディレクトリツリーのルートを指すように、テンプレートの **アセット** パスを更新します。 たとえば、テンプレートが \CSharp\Windows 内にある場合、参照は \CSharp. を指す必要があります。
