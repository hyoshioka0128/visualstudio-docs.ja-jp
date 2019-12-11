---
title: Visual Studio for Mac の拡張
description: Visual Studio for Mac の機能は、拡張機能パッケージというモジュールを使用して拡張できます。 このガイドの最初の第 1 部では、ドキュメントに日時を挿入する単純な Visual Studio for Mac 拡張機能パッケージを作成します。 このガイドの第 2 部では、拡張機能パッケージ システムの基礎と、Visual Studio for Mac の基礎を形成するコア API の一部を紹介します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/07/2019
ms.technology: vs-ide-sdk
ms.assetid: D5245AB0-8404-426B-B538-F49125E672B2
ms.openlocfilehash: 76f8f4945542d1b2fd4dce230d750db4c965af76
ms.sourcegitcommit: 370cc7fd2e11ede6d8215c8d81963a8307614550
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74983270"
---
# <a name="extending-visual-studio-for-mac"></a>Visual Studio for Mac の拡張

Visual Studio for Mac は、*拡張機能パッケージ*というモジュール セットから構成されます。 拡張機能パッケージを使用して、追加言語や新しいプロジェクト テンプレートのサポートなど、新しい機能を Visual Studio for Mac に導入することができます。

拡張機能パッケージは、他の拡張機能パッケージの*拡張*ポイントから構築されます。 拡張ポイントとは、拡張できる領域のプレースホルダーです。たとえば、IDE コマンドのメニューやリストなどです。 拡張ポイントから拡張機能パッケージをビルドするには、新しいメニュー項目や新しいコマンドなど、拡張機能と呼ばれる構造化データのノードを登録します。 各拡張ポイントは、*Command*、*Pad*、*FileTemplate* など、特定の種類の拡張機能を受け入れています。 拡張ポイントを含むモジュールは、他の拡張機能パッケージで拡張できるので、*アドイン ホスト*と呼ばれます。

Visual Studio for Mac をカスタマイズするには、Visual Studio for Mac の既存のライブラリ内のアドインに含まれる拡張ポイントから構築する拡張機能パッケージを作成できます。

![アドイン アーキテクチャ](media/extending-visual-studio-mac-addin1.png)

Visual Studio for Mac から拡張機能パッケージを構築するには、Visual Studio for Mac IDE 内の既存の拡張ポイントから構築された拡張機能が必要です。 拡張機能パッケージが、アドイン ホストに定義されている拡張ポイントに依存している場合、その拡張機能パッケージに _依存関係_ があると考えられます。

このモジュール式設計の利点は、Visual Studio for Mac が拡張可能であり、カスタム拡張機能パッケージを使用して構築できる拡張ポイントが多数あります。 現在の拡張機能パッケージの例として、C# および F# のサポート、デバッガー ツール、プロジェクト テンプレートなどがあります。

> [!NOTE]
> Add-in Maker 1.2 より前のバージョンで作成した Add-in Maker プロジェクトがある場合、[こちらの手順](https://mhut.ch/addinmaker/1.2)に従ってプロジェクトを移行する必要があります。

<!---The [Walkthrough](~/extending-visual-studio-mac-walkthrough.md) topic explains how to build an extension package that uses a *Command* to insert the date and time into an open text document.--->

このセクションでは、Add-in Maker で生成されるさまざまなファイルと、コマンド拡張機能に必要なデータについて説明します。

## <a name="attribute-files"></a>属性ファイル

拡張機能パッケージは、パッケージの名前、バージョン、依存関係などの情報に関するメタデータを C# 属性に格納します。 Add-in Maker では、この情報を格納して整理するために `AddinInfo.cs` と `AssemblyInfo.cs` という 2 つのファイルが作成されます。 拡張機能パッケージには、それらの " *`Addin` 属性*" に指定された一意の ID と名前空間が必要です。

```csharp
[assembly:Addin (
   "DateInserter",
   Namespace = "DateInserter",
   Version = "1.0"
)]
```

拡張機能パッケージでは、接続先の拡張ポイントを所有している拡張機能パッケージへの依存関係も宣言する必要があります。これらはビルド時に自動的に参照されます。

さらに、次の図のように、プロジェクトの Solution Pad でアドイン参照ノードを使用して新しい参照を追加することができます。

![[Insert Date]\(日付の挿入\) のスクリーンショット](media/extending-visual-studio-mac-addin13.png)

また、対応する `assembly:AddinDependency` 属性もビルド時に追加されています。 メタ データと依存関係の宣言を設定したら、拡張機能パッケージの重要な構成要素に集中できます。

## <a name="extensions-and-extension-points"></a>拡張機能と拡張ポイント

拡張ポイントは、データ構造 (型) を定義するプレースホルダーです。一方、拡張機能は、特定の拡張ポイントに指定されている構造に準拠するデータを定義します。 拡張ポイントは、受け入れることができる拡張機能の種類を宣言で指定します。 拡張機能は、型名または拡張機能パスを使用して宣言します。 必要な拡張ポイントを作成する詳細な説明については、[拡張ポイントのリファレンス](https://github.com/mono/mono-addins/wiki/Extension-Points)を参照してください。

拡張機能/拡張ポイント アーキテクチャでは、Visual Studio for Mac の開発の速度とモジュール式はそのまま利用できます。

<!--Since there are a large number of extension types, this article focuses on the ones used in the extension package that was built in the [Walkthrough](~/extending-visual-studio-mac-walkthrough.md).-->

### <a name="command-extensions"></a>コマンド拡張機能

<!--[Walkthrough](~/extending-visual-studio-mac-walkthrough.md) uses a Command Extension - an extension that points to methods that are called every time it is executed. -->

コマンド拡張機能とは、実行するたびに呼び出されるメソッドを示す拡張機能です。

コマンド拡張機能は、`/MonoDevelop/Ide/Commands` 拡張ポイントにエントリを追加して定義されます。 ここでは、次のコードを使用して `Manifest.addin.xml` に拡張機能を定義しました。

 ```xml
<Extension path="/MonoDevelop/Ide/Commands/Edit">
  <command id="DateInserter.DateInserterCommands.InsertDate"
            _label="Insert Date"
            _description="Insert the current date"
            defaulthandler="DateInserter.InsertDateHandler" />
</Extension>
```

拡張機能ノードには、接続先の拡張ポイントを指定するパス属性が含まれています。この場合は `/MonoDevelop/Ide/Commands/Edit` です。 また、コマンドの親ノードとして動作します。 コマンド ノードには、次の属性が含まれています。

* `id` - このコマンドの識別子を指定します。 コマンド識別子は、列挙型のメンバーとして宣言する必要があります。この識別子は、Commands を CommandItems に接続するために使用されます。
* `_label` - メニューに表示されるテキスト。
* `_description` - ツールバー ボタンのツールヒントとして表示されるテキスト。
* `defaultHandler` - コマンドを利用する `CommandHandler` クラスを指定します。

<!--To invoke the command from the Edit Menu, the walkthrough creates a CommandItem extension that plugs into the `/MonoDevelop/Ide/MainMenu/Edit` extension point:-->

CommandItem 拡張機能を `/MonoDevelop/Ide/MainMenu/Edit` 拡張ポイントに組み込む例を、次のコード スニペットで示します。

```xml
<Extension path="/MonoDevelop/Ide/MainMenu/Edit">
  <commanditem id="DateInserter.DateInserterCommands.InsertDate" />
</Extension>
```

CommandItem は、`id` 属性に指定されているコマンドをメニューに配置します。 この CommandItem によって `/MonoDevelop/Ide/MainMenu/Edit` 拡張ポイントが拡張され、 **[編集] メニュー**にコマンドのラベルが表示されます。 CommandItem の ID はコマンド ノード `InsertDate` の ID に対応することに注意してください。 CommandItem を削除すると、[編集] メニューに **[日付の挿入]** オプションが表示されなくなります。

### <a name="command-handlers"></a>コマンド ハンドラー

`InsertDateHandler` は `CommandHandler` クラスの拡張機能です。 `Update` と `Run` という 2 つのメソッドはオーバーライドされます。 コマンドがメニューに表示される場合、またはキー バインドで実行される場合は常に、`Update` メソッドが照会されます。 info オブジェクトを変更することで、コマンドを無効にしたり、非表示にしたり、配列コマンドを設定したりすることができます。 テキスト情報を挿入する *TextEditor* でアクティブな*ドキュメント*が見つからない場合、`Update` メソッドを使用すると、コマンドが無効になります。

```csharp
protected override void Update (CommandInfo info)
{
    info.Enabled = IdeApp.Workbench.ActiveDocument?.Editor != null;
}
```

コマンドを有効または非表示にする特殊なロジックがある場合は、`Update` メソッドをオーバーライドする必要があります。 `Run` メソッドは、ユーザーがコマンドを実行するたび (この例では、ユーザーが [編集] メニューからコマンドを選択したとき) に実行されます。 このメソッドを実行すると、テキスト エディターでカレット位置に日時が挿入されます。

```csharp
protected override void Run ()
{
  var editor = IdeApp.Workbench.ActiveDocument.Editor;
  var date = DateTime.Now.ToString ();
  editor.InsertAtCaret (date);
}
```

`DateInserterCommands` 内の列挙型メンバーとしてコマンドの型を宣言します。

```csharp
public enum DateInserterCommands
{
  InsertDate,
}
```

これで、コマンドと CommandItem が関連付けられます。CommandItem が **[編集] メニュー**から選択されたときに、CommandItem によってコマンドが呼び出されます。

## <a name="ide-apis"></a>IDE API

<!--The extension package detailed in the [Walkthrough](~/extending-visual-studio-mac-walkthrough.md) deals with the Text Editor in Visual Studio for Mac, but this is only one of many possible areas for customization. -->

開発に使用できる領域の範囲については、「[Extension Tree Reference](https://www.monodevelop.com/developers/articles/extension-tree-reference/)」(拡張機能ツリー リファレンス) と「[API Overview](https://www.monodevelop.com/developers/articles/api-overview/)」(API の概要) を参照してください。 高度な拡張機能パッケージを構築する場合は、[開発者向け](https://www.monodevelop.com/developers/articles/)の記事も参照してください。 カスタマイズ可能な領域の一部を次に示します。

* パッド
* キー バインド スキーム
* ポリシー
* コード フォーマッタ
* プロジェクト ファイルの形式
* ユーザー設定パネル
* オプション パネル
* デバッガー プロトコル
* デバッガー ビジュアライザー
* ワークスペースのレイアウト
* Solution Pad のツリー ノード
* ソース エディターの余白
* 単体テスト エンジン
* コード ジェネレーター
* コード スニペット
* ターゲット フレームワーク
* ターゲット ランタイム
* VCS バックエンド
* リファクタリング
* 実行ハンドラー
* 構文の強調表示

## <a name="extending-the-new-editor"></a>新しいエディターの拡張

Visual Studio for Mac には、Visual Studio on Windows と同じエディター レイヤーの上に構築された[新しいネイティブ Cocoa テキスト エディター UI が導入されています](https://aka.ms/vs/mac/editor/learn-more)。

Visual Studio と Visual Studio for Mac 間でのエディターの共有による多くのメリットの 1 つに、Visual Studio エディターをターゲットとするコードを Visual Studio for Mac で実行するように適応させることができるという点があります。

> [!NOTE]
> この新しいエディターでは、現時点では C# ファイルのみがサポートされています。 その他の言語とファイル形式は、レガシ エディターで開きます。 ただし、レガシ エディターでも、以下に示すいくつかの Visual Studio Editor API が実装されます。

### <a name="visual-studio-editor-overview"></a>Visual Studio エディターの概要

![Visual Studioエディターのアーキテクチャ](media/vs-editor-architecture.png)

Visual Studio for Mac に固有の拡張機能の詳細を説明する前に、共有エディターそのものをもっと理解しておくと役立ちます。 この理解を深めるのに役立ついくつかのリソースを次に示します。

* [Managed Extensibility Framework](/dotnet/framework/mef/index)
* [エディターでの MEF](/visualstudio/extensibility/managed-extensibility-framework-in-the-editor)
* [エディターの内部](/visualstudio/extensibility/inside-the-editor)
* [言語サービスとエディターの拡張ポイント](/visualstudio/extensibility/language-service-and-editor-extension-points)
* [エディターのアーキテクチャ紹介ビデオ](https://www.youtube.com/watch?v=PkYVztKjO9A)

これらのリソースを利用して理解しておく必要がある主要な概念は、[`ITextBuffer`](/dotnet/api/microsoft.visualstudio.text.itextbuffer) と [`ITextView`](/dotnet/api/microsoft.visualstudio.text.editor.itextview) です。

* `ITextBuffer` は、時間の経過と共に変更される可能性があるテキストのメモリ内表現です。 `ITextBuffer` の `CurrentSnapshot` プロパティは、バッファ内の現在のコンテンツの "*不変の*" 表現である `ITextSnapshot` インスタンスを返します。 バッファーで編集が行われると、CurrentSnapshot プロパティが最新のバージョンに更新されます。 アナライザーで任意のスレッドのテキスト スナップショットを検査して、その内容が変更されないことを保証できます。

* `ITextView` は、エディター コントロールの画面に `ITextBuffer` がどのようにレンダリングされるかの UI 表現です。 それは、`Caret`、`Selection`、およびその他の UI 関連の概念だけではなく、テキスト バッファーへの参照も持っています。

特定の [`MonoDevelop.Ide.Gui.Document`](http://source.monodevelop.com/#MonoDevelop.Ide/MonoDevelop.Ide.Gui/Document.cs,4e960d4735f089b5) については、関連付けられている基になる `ITextBuffer` と `ITextView` を、それぞれ `Document.GetContent<ITextBuffer>()` と `Document.GetContent<ITextView>()` 経由で取得できます。

## <a name="additional-information"></a>追加情報

> [!NOTE]
> 現在、Visual Studio for Mac の機能拡張シナリオを改善するために取り組んでいます。 拡張機能の作成中に追加のヘルプや情報が必要な場合、またはフィードバックを提供したい場合は、「[Visual Studio for Mac Extension Authoring (Visual Studio for Mac の拡張機能の作成)](https://aka.ms/vsmac-extensions-survey)」フォームに記入してお知らせください。

## <a name="see-also"></a>関連項目

- [Visual Studio 拡張機能の開発 (Windows)](/visualstudio/extensibility/starting-to-develop-visual-studio-extensions)
