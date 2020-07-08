---
title: Visual Studio for Mac チュートリアルの拡張
author: heiligerdankgesang
ms.author: dominicn
ms.date: 04/14/2017
ms.technology: vs-ide-sdk
ms.assetid: 7D00512B-9688-4D8D-87A7-F04F207E3D02
ms.topic: how-to
ms.openlocfilehash: 8b0f1213d500563e9fa6f3574c6b622e3214e03a
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2020
ms.locfileid: "85939168"
---
# <a name="extending-visual-studio-for-mac-walkthrough"></a>Visual Studio for Mac チュートリアルの拡張

ここでは、[単純な拡張機能パッケージ](https://github.com/mjh4/AddIns/tree/master/DateInserter)を構築する手順について説明します。 この拡張機能パッケージを使用すると、Visual Studio for Mac の [編集] メニューに新しいコマンドが作成され、ユーザーは開いているテキスト ドキュメントに現在の日時を挿入できるようになります。

この例では、Add-in Maker を使用します。 Add-in Maker では、新しいプロジェクト テンプレートが作成され、カスタム拡張機能パッケージに必要なファイルが設定されます。

1. まず、Visual Studio for Mac をまだ開いていない場合は起動します。

   ![Visual Studio for Mac のスクリーンショット](media/extending-visual-studio-mac-addin3.png)

2. 拡張機能マネージャーを使用して _Add-in Maker 拡張機能パッケージ_をインストールします。 Visual Studio のメニューから **[拡張機能]** を選択します。

   ![アドイン マネージャー タブ](media/extending-visual-studio-mac-addin4.png)

3. [ギャラリー] タブに移動し、右上の検索バーに `Addin Maker` と入力します。 [Addin Development]\(アドインの開発\) カテゴリの [Addin Maker] を選択し、<kbd>[インストール]</kbd> をクリックします。 何も表示されない場合は、[更新] をクリックしてもう一度検索します。

   ![アドイン マネージャー](media/extending-visual-studio-mac-addin5.png)

4. Addin Maker がインストールされたら、拡張機能パッケージの構築を始めることができます。 まず新しいソリューションを作成します。

5. **[新しいソリューション]** ダイアログから、 **[その他] > [その他] > [全般] > [Xamarin Studio Addin] を選択し、C#** テンプレートを選択して、次の画面で新しいソリューションに `DateInserter` と名前を付けます。

   ![新しいソリューションの作成](media/extending-visual-studio-mac-addin7New.png)

6. Visual Studio for Mac で新しいソリューションが作成されます。

   ![作成されるソリューション](media/extending-visual-studio-mac-addin8.png)

7. `Manifest.addin.xml` のテンプレート コードを削除し、次のように置き換えます。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
      <ExtensionModel>
          <Extension path = "/MonoDevelop/Ide/Commands/Edit">
              <Command id = "DateInserter.DateInserterCommands.InsertDate"
                  _label = "Insert Date"
                  defaultHandler = "DateInserter.InsertDateHandler" />
          </Extension>

          <Extension path = "/MonoDevelop/Ide/MainMenu/Edit">
              <CommandItem id="DateInserter.DateInserterCommands.InsertDate" />
          </Extension>
      </ExtensionModel>
   ```

8. 次に、テキスト エディターへの日時の挿入を処理することになるファイルをセットアップする必要があります。 プロジェクト ノードを右クリックし、新しいファイルを追加します。 **[全般] > [空のクラス]** を選択し、新しいファイルに *InsertDateHandler* と名前を付けます。

   ![データ ハンドラーの挿入](media/extending-visual-studio-mac-addin9.png)

9. `InsertDateHandler.cs` からテンプレート コードを削除し、次のように置き換えます。

   ```cs
   using MonoDevelop.Components.Commands;
   using MonoDevelop.Ide;
   using MonoDevelop.Ide.Gui;
   using System;

   namespace DateInserter
   {
      class InsertDateHandler : CommandHandler
      {
          protected override void Run()
          {

          }

          protected override void Update(CommandInfo info)
          {

          }
      }
   }
   ```

   これら 2 つのプレースホルダー メソッドは後で拡張します。

10. **DateInserter** プロジェクトを右クリックし、 **[追加] > [新しいファイル]** を選択します。 **[全般] > [空の列挙型]** を選択し、新しいファイルに *DateInserterCommands* と名前を付けます。

    ![DateInserterCommands](media/extending-visual-studio-mac-addin10.png)

11. `InsertDate` コマンドを新しい列挙型として `DateInserterCommands.cs` ファイルに追加します。

    ``` cs
    using System;

    namespace DateInserter
    {
      public enum DateInserterCommands
      {
          InsertDate,
      }
    }
    ```

12. この時点で、動作する拡張機能パッケージができあがっています。 作業内容を保存し、アプリケーションを実行してテストすることができます。 IDE で、新しい拡張機能パッケージがインストールされた新しいインスタンスの Visual Studio for Mac が起動します。 **[編集] メニュー**を開くと、Visual Studio for Mac に次のスクリーンショットのように **[Insert Date]\(日付の挿入\)** という新しいオプションが表示されます。

    ![[Insert Date]\(日付の挿入\) コマンド](media/extending-visual-studio-mac-addin11.png)

    現在の実装にはプレースホルダー メソッドしかないため、メニューから [Insert Date]\(日付の挿入\) を選択しても何も実行されません。

13. 拡張機能パッケージのフレームワークはあるので、日付の挿入を動かすコードを記述しましょう。 まず、`InsertDateHandler.cs` の `Update` メソッドを次のコードで置き換えて、ユーザーがテキスト ファイルを開いたときに **[Insert Date]\(日付の挿入\) コマンド**のみが有効になることを確認します。

    ```cs
    protected override void Update(CommandInfo info)
    {
      info.Enabled = IdeApp.Workbench.ActiveDocument?.Editor != null;
    }
    ```

14. 日時を挿入するように、コマンドの `Run` メソッドを次のコードで置き換えます。

    ``` cs
    protected override void Run () {
      var editor = IdeApp.Workbench.ActiveDocument.Editor;
      var date = DateTime.Now.ToString ();
      editor.InsertAtCaret (date);

    }
    ```

15. 最後に、拡張機能パッケージを実行してテストします。 新しいインスタンスの Visual Studio for Mac で、 **[編集] > [Insert Date]\(日付の挿入\)** を選択します。 次のスクリーンショットのように、現在の日時がカレットに挿入されます。

    ![[Insert Date]\(日付の挿入\) のスクリーンショット](media/extending-visual-studio-mac-addin12.png)

## <a name="see-also"></a>参照

- [初めての拡張機能の作成 (Windows の Visual Studio)](/visualstudio/extensibility/extensibility-hello-world)