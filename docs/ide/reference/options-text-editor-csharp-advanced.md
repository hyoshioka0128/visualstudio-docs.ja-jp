---
title: '[オプション]、[テキスト エディター]、[C#]、[詳細]'
ms.date: 01/16/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.CSharp.Advanced
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ff42473c6f56d69a56cfbd811f2687ba544c7c5e
ms.sourcegitcommit: 4d932000a0f7e79c9475fe66c02fe9addcd7e47a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86181067"
---
# <a name="options-text-editor-c-advanced"></a>[オプション]、[テキスト エディター]、[C#]、[詳細]

**[詳細]** オプションを使って、C# のエディターの書式設定、コードのリファクタリング、および XML ドキュメントのコメントの設定を変更します。 このオプション ページにアクセスするには、 **[ツール]**  >  **[オプション]** を選び、さらに **[テキスト エディター]**  >  **[C#]**  >  **[詳細]** の順に選びます。

> [!NOTE]
> ここには、すべてのオプションが一覧されていない可能性があります。

## <a name="analysis"></a>分析

- ライブ コード分析またはバックグラウンド分析スコープ

   マネージド コードのバックグラウンド分析スコープを構成します。 詳細については、「[方法:方法: マネージド コードのライブ コード分析スコープを構成する](../../code-quality/configure-live-code-analysis-scope-managed-code.md)」を参照してください。

## <a name="using-directives"></a>Using ディレクティブ

- using を並べ替える際に、'System' ディレクティブを先頭に配置する

   選択した場合、右クリック メニューの **[using の削除と並べ替え]** コマンドによって `using` ディレクティブが並べ替えられ、'System' 名前空間が一覧の先頭に置かれます。

   並べ替える前:

   ```csharp
   using AutoMapper;
   using FluentValidation;
   using System.Collections.Generic;
   using System.Linq;
   using Newtonsoft.Json;
   using System;
   ```

   並べ替えた後:

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using AutoMapper;
   using FluentValidation;
   using Newtonsoft.Json;
   ```

- ディレクティブ グループを使用して分離します

   選択した場合、右クリック メニューの **[using の削除と並べ替え]** コマンドによって、同じルート名前空間を持つディレクティブのグループの間に空の行を挿入することで、`using` ディレクティブが分離されます。

   並べ替える前:

   ```csharp
   using AutoMapper;
   using FluentValidation;
   using System.Collections.Generic;
   using System.Linq;
   using Newtonsoft.Json;
   using System;
   ```

   並べ替えた後:

   ```csharp
   using AutoMapper;

   using FluentValidation;

   using Newtonsoft.Json;

   using System;
   using System.Collections.Generic;
   using System.Linq;
   ```

::: moniker range=">=vs-2019"                                              
- .NET Framework アセンブリの型に using を提案する
::: moniker-end
                                         
::: moniker range="vs-2017"                                                
- 参照アセンブリの型に using を提案する
::: moniker-end                                                            

- NuGet パッケージの型に using を提案する

   これらのオプションを選択した場合、[クイック アクション](../quick-actions.md)を使用して NuGet パッケージをインストールし、参照されていない型の `using` ディレクティブを追加できます。

   ![Visual Studio に NuGet パッケージをインストールするためのクイック アクション](media/nuget-lightbulb.png)

## <a name="highlighting"></a>強調表示

- カーソルの下にあるシンボルへの参照をハイライトする

   シンボル内にカーソルを置いたり、シンボルをクリックしたりすると、コード ファイル内のそのシンボルのすべてのインスタンスが強調表示されます。

## <a name="outlining"></a>アウトライン

- ファイルが開かれたときにアウトライン モードを実行する

   選択すると、コードの折りたたみ可能なブロックを作成するコード ファイルが自動的にアウトラインになります。 初めてファイルが開かれると、#regions ブロックとアクティブでないコード ブロックが折りたたまれます。

- プロシージャ行の区切り記号を表示する

   テキスト エディターに、プロシージャのスコープが表示されます。 プロジェクトの *.cs* ソース ファイルで、次の表に示す場所に線が表示されます。

   |.cs ソース ファイル内の場所|線が表示される場所の例|
   |---------------------------------|------------------------------|
   |ブロック宣言構造の後|-   クラス、構造体、モジュール、インターフェイス、または列挙型の最後<br />-   プロパティ、関数、または sub の後<br />-   プロパティの get 句と set 句の間は対象外|
   |一連の単一行構造|-   import ステートメントの後、クラス ファイルの型定義の前<br />-   クラスで宣言されている変数の後、プロシージャの前|
   |単一行宣言|-   Import ステートメント、Inherits ステートメント、変数宣言、イベント宣言、デリゲート宣言、および DLL の Declare ステートメントの後|

## <a name="block-structure-guides"></a>ブロック構造のガイド

コードの中かっこ ( **{}** ) の間に垂直の点線を表示するには、このチェック ボックスをオンにします。 これで、宣言レベルとコード レベルのコンストラクト用のコード ブロックを簡単に確認できます。

## <a name="editor-help"></a>エディターのヘルプ

- /// が入力されたとき、XML ドキュメントのコメントを生成する

   オンにすると、`///` コメント イントロダクションを入力した後に、XML ドキュメント コメントの XML 要素が挿入されます。 XML ドキュメントの詳細については、「[XXML ドキュメント コメント (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: ドキュメント生成のための XML コメントを挿入する](../../ide/reference/generate-xml-documentation-comments.md)
- [XML ドキュメント コメント (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [XML コメントによるコードの文書化 (C# ガイド)](/dotnet/csharp/codedoc)
- [言語固有のエディター オプションの設定](../../ide/reference/setting-language-specific-editor-options.md)
- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
