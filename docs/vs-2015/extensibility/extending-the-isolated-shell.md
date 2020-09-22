---
title: 分離シェルの拡張 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode
ms.assetid: 9a641d8f-211e-4486-a1b1-4a89fafe7ee8
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ea55039de769598b26868727a93cfa11726e4838
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841645"
---
# <a name="extending-the-isolated-shell"></a>分離シェルの拡張
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage、Managed Extensibility Framework (MEF) コンポーネントパーツ、または汎用 VSIX プロジェクトを分離シェルアプリケーションに追加することで、Visual Studio 分離シェルを拡張できます。  
  
> [!NOTE]
> 次の手順では、Visual Studio Shell 分離プロジェクトテンプレートを使用して、基本的な分離シェルアプリケーションを作成したことを前提としています。 このプロジェクトテンプレートの詳細については、「 [チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio パッケージ プロジェクト テンプレートの場所  
 Visual Studio パッケージのプロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログの次の 3 つの場所にあります。  
  
1. **Visual Basic**、**拡張機能**の下。 プロジェクトの既定の言語は Visual Basic です。  
  
2. **Visual C#** の場合は、**機能拡張**です。 プロジェクトの既定の言語は C# です。  
  
3. [ **その他のプロジェクトの種類**] の [ **機能拡張**]。 プロジェクトの既定の言語は C++ です。  
  
## <a name="adding-a-vspackage"></a>VSPackage の追加  
 分離シェルアプリケーションに VSPackage を追加できます。 次の手順では、メニューコマンドを追加するものを作成する方法を示します。  
  
#### <a name="to-add-a-new-vspackage"></a>新しい VSPackage を追加するには  
  
1. という名前の Visual Studio パッケージプロジェクトを追加 `MenuCommandsPackage` します。  
  
2. ウィザードの [ **VSPackage の基本情報** ] ページで、[ **Company name** ] をに、 `Fabrikam` [ **VSPackage name** ] をに設定し `FabrikamMenuCommands` ます。 **[次へ]** ボタンをクリックします。  
  
3. 次のページで、[ **メニューコマンド** ] を選択し、[ **次へ**] をクリックします。  
  
4. 次のページで、[ **コマンド名** ] をに、[ `Fabrikam Command` **コマンド ID** ] をに設定し、 `cmdidFabrikamCommand` [ **次へ**] をクリックします。  
  
5. [ **テストプロジェクトオプションの選択** ] ページで、テストオプションをオフにし、[ **完了** ] をクリックします。  
  
6. ShellExtensionsVSIX プロジェクトで、source.extension.vsixmanifest ファイルを開きます。  
  
     **Assets**セクションには、VSShellStub.. boxpackage プロジェクトのエントリが含まれている必要があります。  
  
7. [ **新規** ] ボタンをクリックします。  
  
8. [ **新しい資産の追加** ] ウィンドウの [ **種類** ] ボックスの一覧で、[ **VisualStudio. VsPackage**] を選択します。  
  
9. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト** が選択されていることを確認します。 [ **プロジェクト** ] ボックスの一覧で [ **MenuCommandsPackage**] を選択します。  
  
10. ファイルを保存して閉じます。  
  
11. ソリューションをリビルドし、分離シェルのデバッグを開始します。  
  
12. メニューバーで、[ **ツール** ] メニュー、[ **Fabrikam コマンド**] の順に選択します。  
  
     メッセージボックスが表示されます。  
  
13. アプリケーションのデバッグを停止します。  
  
## <a name="adding-a-mef-component-part"></a>MEF コンポーネントパーツの追加  
 次の手順では、MEF コンポーネントパーツを分離シェルアプリケーションに追加する方法を示します。  
  
#### <a name="to-add-a-mef-component"></a>MEF コンポーネントを追加するには  
  
1. [ **新しいプロジェクトの追加** ] ダイアログボックスの [ **Visual C#**]、[ **拡張機能**] で、[ **エディターの余白** ] テンプレートを使用してプロジェクトを追加します。 これに `ShellEditorMargin` という名前を付けます。  
  
2. ShellExtensionsVSIX プロジェクトで、コードビューではなくデザインビューで source.extension.vsixmanifest ファイルを開きます。  
  
3. セクションで `Asset` 、[ **コンテンツの追加**] を選択します。  
  
4. [ **新しい資産の追加** ] ウィンドウの [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。  
  
5. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト** が選択されていることを確認します。 [ **プロジェクト** ] ボックスの一覧で [ **ShellEditorMargin**] を選択します。  
  
6. ファイルを保存して閉じます。  
  
7. ソリューションをリビルドし、分離シェルのデバッグを開始します。  
  
8. テキストファイルを開きます。  
  
     "Hello world!" という単語を含む緑色の余白 は、[テキストファイル] ウィンドウの下部に表示されます。  
  
9. アプリケーションのデバッグを停止します。  
  
## <a name="adding-a-generic-vsix-project"></a>汎用 VSIX プロジェクトの追加  
  
#### <a name="to-add-a-generic-vsix-project"></a>汎用 VSIX プロジェクトを追加するには  
  
1. [ **新しいプロジェクトの追加** ] ダイアログボックスの [ **Visual C#**]、[ **拡張機能**] で、 **VSIXProject** テンプレートを使用してプロジェクトを追加します。 これに `EmptyVSIX` という名前を付けます。  
  
2. ShellExtensionsVSIX プロジェクトで、コードビューではなくデザインビューで source.extension.vsixmanifest ファイルを開きます。  
  
3. セクションで `Assets` 、[ **新規**] を選択します。  
  
4. [ **新しい資産の追加** ] ウィンドウの [ **種類** ] ボックスの一覧で、追加するコンテンツの種類を選択します。  
  
5. [ **ソース**] で、[ **現在のソリューション内のプロジェクト** ] オプションが選択されていることを確認します。 リストボックスで、VSIX プロジェクトの名前を選択します。  
  
6. ファイルを保存して閉じます。  
  
7. このプロジェクトにコンパイル済みのコードが含まれている場合は、アセンブリが出力に含まれるようにプロジェクトを編集する必要があります。  
  
    1. VSIX プロジェクトをアンロードし、プロジェクトファイルを開きます。  
  
    2. 最初の `<PropertyGroup>` ブロックで、の値 `<CopyBuildOutputToOutputDirectory>` をに変更し `true` ます。  
  
    3. プロジェクトを保存して再読み込みします。  
  
8. ソリューションをビルドして実行します。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: 基本的な分離シェル アプリケーションを作成する](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)
