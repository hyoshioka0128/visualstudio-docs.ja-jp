---
title: コードのリファクタリング
description: Visual Studio for Mac およびクイック アクションを使用して、コードを調整します。
author: jmatthiesen
ms.author: jomatthi
ms.date: 07/03/2020
ms.assetid: C7782BF3-016F-4B41-8A81-85FC540A1A8F
ms.custom: video
ms.openlocfilehash: 3892117e5c84a71f258d4e019105fca0a8cf9c5b
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96189239"
---
# <a name="refactoring"></a>リファクタリング

コードのリファクタリングは、既存のコードの再配置、再構築、および明確化を行うための方法です。コードの動作全体が変わることはありません。

リファクタリングすると、より健全なコード ベースが生成されるので、自分またはコードを参照する可能性のある他の開発者やユーザーがより使いやすく、読みやすく、また保守しやすくなります。

Visual Studio for Mac と、Roslyn (Microsoft のオープンソースの .NET コンパイラ プラットフォーム) との統合により、より多くのリファクタリング操作が可能になります。

## <a name="renaming"></a>名前の変更

コード識別子 (クラス名やプロパティ名など) で *[名前の変更]* リファクタリング コマンドを使用して、その識別子のすべての出現箇所を検索し、変更することができます。 シンボルの名前を変更するには、次のように、そのシンボルを右クリックし、**[名前の変更...]** を選択するか、**Cmd (⌘) + R** キー バインドを使用します。

![[名前の変更] メニュー項目](media/refactoring-renaming1.png)

これでシンボルとその参照が強調表示されます。 新しい名前の入力を開始すると、コードのすべての参照が自動的に変更されます。次のように **Enter** キーを押すと、変更をコミットできます。

![名前の変更と識別子](media/refactoring-renaming2.png)

## <a name="quick-actions-and-refactorings"></a>クイック アクションとリファクタリング

クイック アクションとリファクタリングを使うと、コードのリファクタリング、生成、その他の変更を、1 つの操作で簡単に行うことができます。

クイック アクションを使用して、次の操作を実行できます。

* コード アナライザーの規則違反に対してコード修正を適用する
* コード アナライザーの規則違反を抑制する
* リファクタリングを適用する (例: 一時変数をインライン化する)
* コードを生成する (例: ローカル変数を導入する)

クイック アクションを適用するには、電球 ![電球アイコン](media/quick-actions-light-bulb-icon.png) またはねじ回し ![ねじ回しアイコン](media/quick-actions-screwdriver-icon.png) を使用するか、アクションがあるコード行にカーソルがあるときに **Option (⌥)** +**Enter** を押します。 エラーを示す赤い波線があり、Visual Studio にそのエラーに対処するために使用可能な解決策がある場合は、エラー電球 ![エラー電球アイコン](media/quick-actions-error-light-bulb-icon.png) が表示されます。

いずれの言語でも、サードパーティは、たとえば SDK の一部として、カスタマイズした診断や提案を表示できます。Visual Studio はそれらの規則に基づいて電球マークを表示します。

### <a name="quick-action-icons"></a>クイック アクション アイコン
クイック アクションが使用可能なときに表示されるアイコンは、使用可能な解決策またはリファクタリングの種類を示します。 *ねじ回し* ![ねじ回しアイコン](media/quick-actions-screwdriver-icon.png) アイコンは、コードを変更するのに使用可能なアクションがあることを示すだけで、必ずしもそれらを使用する必要はありません。 *黄色の電球* ![電球アイコン](media/quick-actions-light-bulb-icon.png) アイコンは、コードを改善するために実行する *必要がある* 使用可能なアクションがあることを示します。 *エラー電球* ![エラー電球アイコン](media/quick-actions-error-light-bulb-icon.png) アイコンは、コード内のエラーを修正するために使用可能なアクションがあることを示します。

### <a name="to-see-a-light-bulb-or-screwdriver"></a>電球やねじ回しを表示するには

- 解決策が使用可能な場合は、エラーの場所にマウス ポインターを置くと、電球が自動的に表示されます。

   ![電球でのマウス ホバー](media/refactoring-lightbulb-hover.png)

- キャレットをクイック アクションまたはリファクタリングが使用できるコード行に移動すると、エディターの左余白に電球とねじ回しが表示されます。

- 使用可能なクイック アクションとリファクタリングの一覧を表示するには、行の任意の場所で **Option (⌥)** +**Enter** を押します。

![コンテキスト項目を表示する](media/refactoring-context-action.png)

コンテキスト アクションのいずれかにカーソルを合わせると、コードで追加または削除する内容をプレビューすることができます。

![Option + Enter キーを使用した場合のコンテキスト項目](media/refactoring-image2a.png)

これらのオプションを有効にするには、オプションの **[Visual Studio for Mac]、[基本設定]、[テキスト エディター]、[ソースの解析]** の順に移動して、*[開いているファイルのソース解析を有効にする]* を選択する必要があります

![ソース解析の有効化](media/refactoring-options.png)

推奨される 100 を超える実行可能なアクションがあります。これらを有効または無効にする場合は、**[Visual Studio for Mac]、[基本設定]、[ソースの解析]、[C#]、[コード アクション]** の順に参照し、アクションの横にあるボックスをオンまたはオフにします。

![C# のソース解析アクション](media/refactoring-image3a.png)

### <a name="common-quick-actions"></a>共通のクイック アクション

共通のクイック アクションの詳細については、「[共通のクイック アクション](/visualstudio/ide/common-quick-actions)」の記事を参照してください。

## <a name="source-analysis"></a>ソース解析

ソース解析では、潜在的なエラーとスタイル違反に下線を引き、コンテキスト アクションとして自動修正を提供することで、コードをその場で解析します。

以下のように、テキスト エディターの右側にあるスクロール バーを表示することで、いつでも任意のファイルのソース解析の結果をすべて表示できます。

![ソース解析のサイドバー](media/refactoring-image4a.png)

上部の円をクリックすると、各候補を反復処理でき、最初に重大度が最も高い問題が示されます。 個々の結果または行にカーソルを合わせると、コンテキスト アクションで修正できる問題が表示されます。

![ソース解析項目](media/refactoring-image5.png)

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Refactoring-Code/player]

## <a name="see-also"></a>関連項目

- [クイック アクション (Windows 上の Visual Studio)](/visualstudio/ide/quick-actions)
- [コードのリファクタリング (Windows 上の Visual Studio)](/visualstudio/ide/refactoring-in-visual-studio)
