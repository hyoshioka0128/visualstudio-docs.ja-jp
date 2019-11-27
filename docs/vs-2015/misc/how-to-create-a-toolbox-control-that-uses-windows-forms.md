---
title: '方法: Windows フォームを使用するツールボックスコントロールを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- Toolbox control
- winforms
- toolbox
ms.assetid: abbd3c3c-3a6e-4539-bd6c-a5891dead234
caps.latest.revision: 12
manager: jillfra
ms.openlocfilehash: 8436b8eee0193715e4ae886db18f91f7148dcb3b
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300424"
---
# <a name="how-to-create-a-toolbox-control-that-uses-windows-forms"></a>方法: Windows フォームを使用するツールボックス コントロールを作成する
[!INCLUDE[vssdk_dev11_long](../includes/vssdk-dev11-long-md.md)] に含まれている Windows フォームのツールボックス コントロール テンプレートを使用すると、この拡張機能のインストール時に **[ツールボックス]** に自動的に追加される Windows フォーム コントロールを作成できます。 このトピックでは、他のユーザーに配布できる **ツールボックス** コントロールを、テンプレートを使用して作成する方法について説明します。  
  
> [!NOTE]
> Visual Studio SDK をダウンロードする方法については、MSDN Web サイトの [Visual Studio 機能拡張ディベロッパー センター](https://go.microsoft.com/fwlink/?linkid=121964) をご覧ください。  
  
## <a name="creating-a-toolbox-control"></a>ツールボックス コントロールの作成  
 Windows フォームのツールボックス コントロール テンプレートを使用してプロジェクトを作成し、デザイナーでユーザー インターフェイス (UI) を作成します。  
  
#### <a name="to-create-a-windows-forms-toolbox-control-project"></a>Windows フォームのツールボックス コントロール プロジェクトを作成するには  
  
1. **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。  
  
2. **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Studio にインストールされたテンプレート]** で、使用するプログラミング言語のノードをクリックして、 **[拡張機能]** をクリックします。 プロジェクトの種類の一覧で、 **[Windows フォーム ツールボックス コントロール]** を選びます。  
  
3. **[名前]** ボックスに、プロジェクトの名前を入力します。 **[OK]** をクリックすると、  
  
     Visual Studio は、ユーザー コントロール、 **[ツールボックス]** にコントロールを配置する属性、展開用の VSIX マニフェストを含むソリューションを作成します。  
  
#### <a name="to-build-the-control-ui"></a>コントロール UI を作成するには  
  
1. **[ソリューション エクスプローラー]** で ToolboxControl.cs をダブル クリックします。ToolboxControl.cs がデザイナーで開きます。  
  
2. **[ツールボックス]** から必要なコントロールをデザイン画面にドラッグし、希望するデザインに応じて配置します。  
  
3. **[プロパティ]** ウィンドウで、ユーザー コントロールと子コントロールのパブリック プロパティを設定します。  
  
## <a name="coding-the-control"></a>コントロールのコーディング  
 既定でコントロールは **[ツールボックス]** で、ソリューションと同じ名前の **[ツールボックス]** 項目グループの **ToolboxControl1** として表示されます。 これらの名前は ToolboxControl.cs ファイルで変更できます。  
  
#### <a name="to-code-the-control"></a>コントロールをコーディングするには  
  
1. **[ソリューション エクスプローラー]** で ToolboxControl.cs を右クリックし、 **[コードの表示]** をクリックしてコード ビューでファイルを開きます。  
  
2. コントロールを実装する部分クラスの定義でクラス名を右クリックし、 **[リファクター]** 、 **[名前の変更]** の順にクリックします。 クラスの名前を、コントロールがインストールされるときに **[ツールボックス]** で表示される名前に変更します。  
  
3. クラス定義のすぐ上の `ProvideToolboxControl` 属性宣言で、最初のパラメーターの値を、 **[ツールボックス]** のコントロールをホストする項目グループの名前に変更します。  
  
     次の例では、 `ProvideToolboxControl` 属性と、 `Counter` 項目グループの `General` という名前のコントロールの調整されたクラス定義を示しています。  
  
     [!code-csharp[ToolboxControlWinForms#07](../snippets/csharp/VS_Snippets_VSSDK/toolboxcontrolwinforms/cs/toolboxcontrol.cs#07)]  
  
4. コントロールのプロパティ、メソッド、イベントを実装します。  
  
## <a name="building-testing-and-deployment"></a>ビルド、テスト、展開  
 F5 を押すと、プロジェクト (.vsix 展開ファイルが含まれる) がビルドされ、 **[ツールボックス]** にコントロールがインストールされた Visual Studio の 2 番目のインスタンスが開きます。  
  
#### <a name="to-build-and-test-the-control"></a>コントロールをビルドおよびテストするには  
  
1. F5 キーを押します。  
  
2. Visual Studio の新しいインスタンスで、Windows フォーム アプリケーション プロジェクトを作成します。  
  
3. **[ツールボックス]** で対象のコントロールを見つけて、デザイン画面にドラッグします。  
  
4. **[プロパティ]** ウィンドウで、プロパティが予期したとおりに表示されることを確認します。  
  
5. メソッドとイベントをテストするために必要なコードやその他のコントロールを追加します。  
  
6. F5 キーを押して、Windows フォーム アプリケーションを開きます。  
  
7. コントロールのプロパティ、メソッド、イベントが想定したとおりに動作することを確認します。  
  
#### <a name="to-deploy-the-control"></a>コントロールを配置するには  
  
1. テスト対象のプロジェクトをビルドした後、エクスプローラーでプロジェクトの \bin\debug\ フォルダーを開き、.vsix ファイルを探します。  
  
2. .vsix ファイルをネットワークまたは Web サイトにアップロードします。  
  
     ファイルを[Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードした場合、他のユーザーは Visual Studio の**拡張機能マネージャー**を使用してコントロールを検索してインストールできます。  
  
## <a name="see-also"></a>関連項目  
 [WPF ツールボックス コントロールの作成](../extensibility/creating-a-wpf-toolbox-control.md)