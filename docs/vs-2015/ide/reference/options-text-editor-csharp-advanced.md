---
title: '[オプション]、[テキスト エディター]、[C#]、[詳細] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Advanced
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.CSharp.Advanced
helpviewer_keywords:
- XML comments
- XML documentation, generating
- outlining options [C#]
- outlining options [J#]
- XML documentation, creating
ms.assetid: 947f9d9a-b0f3-408d-9866-d82895bcee31
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4f2d11e78c2402a6541bc87748ed6ba348ba80fc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662319"
---
# <a name="options-text-editor-c-advanced"></a>[オプション]、[テキスト エディター]、[C#]、[詳細]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このダイアログ ボックスを使用して、Visual C# のエディターの書式設定、コードのリファクタリング、および XML ドキュメントのコメントの設定を変更します。 このダイアログ ボックスを表示するには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[テキスト エディター]** フォルダー、 **[C#]** を順に展開し、 **[詳細設定]** をクリックします。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="outlining"></a>アウトライン
 選択したときにファイルを開くときにアウトラインモードを開始すると、コードファイルのアウトラインが自動的に作成され、コードの折りたたみ可能なブロックが作成されます。 初めてファイルが開かれると、#regions ブロックとアクティブでないコード ブロックが折りたたまれます。

## <a name="editor-help"></a>エディターのヘルプ
 エディターのエラーに下線を引くと、コード内のビルドエラーが識別されます。 このオプションを選択すると、色付きの波線が表示されます。色にはそれぞれ特定の意味があります。

- 赤は解析エラーです。

- 青はビルド エラーです。

- 緑はビルドの警告です。

- 紫は無効な[エディット コンティニュ](../../debugger/edit-and-continue.md)の編集内容です。

  下線付きのコード セグメントの上にマウス ポインターを置いて、ヒントでエラーに関する情報を確認してください。

  [ライブセマンティックエラーの表示] では、明示的なコンパイルを行わずに特定のコンパイルエラーを識別します。たとえば、不明な型を宣言して使用したり、不明なプロパティを参照したりできます。

  カーソルがシンボル内に配置されている場合、またはシンボルをクリックしたときに、カーソルの下にあるシンボルへの参照を強調表示すると、コードファイル内のそのシンボルのすべてのインスタンスが強調表示されます。

## <a name="refactoring"></a>リファクタリング
 リファクタリングの結果を確認するビルドエラーを含むコードをリファクターしようとしたとき、またはリファクタリングによってコード参照が元のバインドとは異なるものにバインドされると、 **[検証結果]** ダイアログボックスが表示されます。

 [コンパイラで生成された参照を持つメンバーに警告する] コンパイラで生成された参照と同じ名前を持つメンバーをリファクターしようとすると、警告ダイアログが表示されます。

## <a name="xml-documentation-comments"></a>XML ドキュメントのコメント
 XML ドキュメントコメントを生成する///選択すると、///コメントの概要を入力した後に、XML ドキュメントコメントの開始タグと終了タグ > \<summary が挿入されます。 XML ドキュメントの詳細については、「[XML ドキュメント コメント](https://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)」を参照してください。

## <a name="implement-interface"></a>インターフェイスの実装
 生成されたコードを #region で囲むと、インターフェイスの実装またはインターフェイスの実装が明示的に使用されている場合に、メソッドの周囲に #region \<*インターフェイス名*> メンバーが挿入されます。

## <a name="organize-usings"></a>using の整理
 Using を並べ替えるときに ' System ' ディレクティブを最初に配置します。これを選択すると、他の using ディレクティブの前に `System` using ディレクティブが表示されます。 詳細については、「[using の並べ替え](../../misc/sort-usings.md)」を参照してください。

## <a name="see-also"></a>関連項目
 [XML ドキュメントのコメント](https://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)[言語固有のエディターオプションの設定](../../ide/reference/setting-language-specific-editor-options.md) [Visual C# IntelliSense](../../ide/visual-csharp-intellisense.md)
