---
title: '[オプション]、[テキスト エディター]、[C-C++]、[実験用] | Microsoft Docs'
ms.date: 11/15/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Experimental
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.Experimental
- VS.ToolsOptionsPages.Text_Editor.C\C++.Experimental
ms.assetid: b9e9dda2-350c-460d-b368-37d6c5342eee
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5979363f16f2e9d78a2f50ffbb6511d03146caaa
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297861"
---
# <a name="options-text-editor-cc-experimental"></a>[オプション]、[テキスト エディター]、[C/C++]、[実験用]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

これらのオプションを変更することによって、C または C++ でプログラミングを行うときに、IntelliSense に関連する動作と参照データベースを変更できます。

 このページを表示するには、左ウィンドウの **[オプション]** ダイアログ ボックスで、 **[テキスト エディター]** 、 **[C/C++]** を順に展開して、 **[実験用]** を選びます。

 これらの機能は、Visual Studio 2015 更新プログラム 1 RC のインストールで入手できます。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="browsingnavigation"></a>参照/ナビゲーション
 **新しいデータベースエンジンを有効にする**これにより、 **[定義へのジャンプ**] や **[すべての参照の検索]** などの操作で、データベースの作成が自動的に高速化され、すべてのデータベース操作が (精度を損なうことなく) 高速になります。 (変更を適用するにはソリューションを閉じてもう一度開くだけです。Visual Studio を再起動する必要はありません。)

## <a name="intellisense"></a>IntelliSense
 **メンバーリストのドットから矢印**メンバーリストに適用できる場合は、'. ' を '-> ' に置き換えます。

## <a name="refactoring"></a>リファクタリング
 **Extract 関数の有効化**選択したコードを独自の関数に抽出し、コードを新しい関数への呼び出しに置き換えます。 この機能にアクセスするには、選んだコードを右クリックして **[クイック アクション]** を選ぶか、単に Ctrl キーを押しながらドット キーを押すだけです (Ctrl+.、既定のショートカット)。

 **署名の変更を有効にする**関数のパラメーターを追加、並べ替え、および削除し、変更をすべての呼び出しサイトに反映します。 この機能にアクセスするには、関数の任意の使用法を右クリックして **[クイック アクション]** を選ぶか、Ctrl キーを押しながらドット キーを押すだけです (Ctrl+.、既定のショートカット)。

## <a name="text-editor"></a>テキスト エディター
 **スコープの展開を有効にする**有効にすると、テキストエディターに ' {' を入力することで、選択したテキストを中かっこで囲むことができます。

 **展開の優先順位を有効にする**有効にすると、テキストエディターに ' (' を入力することにより、選択したテキストをかっこで囲むことができます。

 Visual Studio ギャラリーのその他のテキスト エディター機能については、 [ここ](https://go.microsoft.com/fwlink/?LinkId=692016)の一覧をご覧ください。 例として、 [C++ Quick Fixes](https://visualstudiogallery.msdn.microsoft.com/be91feef-8dc3-4f7a-ac9f-f34e7ca5918f)があります。これは、次をサポートします。

- **不足している #include の追加** -コード内の不明なシンボルについて関連する #include を提案します

- **名前空間/完全修飾シンボルの使用を追加** - 前の項目と同様ですが、名前空間に機能します。

- **不足しているセミコロンの追加**

- **MSDN ヘルプ** - MSDN を検索して、エラー メッセージを調べます

  波線の上にカーソルを合わせて電球マークを表示させるか、Ctrl キーを押しながらドットを押すだけです (Ctrl+.、既定のキーボード ショートカット)。 キーボード ショートカットでは、キャレットを特定のエラーやトークンの位置に置く必要はありません。エラーが出た同じ行にカーソルがあれば、行の上の何らかのものに対して解決策が提示されます。

## <a name="see-also"></a>関連項目
 [言語固有のエディターオプションの設定](../../ide/reference/setting-language-specific-editor-options.md)[にC++関するリファクタリング (VC ブログ)](https://devblogs.microsoft.com/cppblog/all-about-c-refactoring-in-visual-studio-2015-preview/)
