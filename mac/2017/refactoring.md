---
title: コードのリファクタリング
description: Visual Studio for Mac でのコードの再編成は、ソース解析を使用して簡単に行うことができます。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: C7782BF3-016F-4B41-8A81-85FC540A1A8F
ms.custom: video
ms.openlocfilehash: 7b11f09d8fb70612d4496987f69583b2ac691275
ms.sourcegitcommit: 370cc7fd2e11ede6d8215c8d81963a8307614550
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74985239"
---
# <a name="refactoring"></a>リファクタリング

コードのリファクタリングは、既存のコードの再配置、再構築、および明確化を行うための方法です。コードの動作全体が変わることはありません。

リファクタリングすると、より健全なコード ベースが生成されるので、自分またはコードを参照する可能性のある他の開発者やユーザーがより使いやすく、読みやすく、また保守しやすくなります。

Visual Studio for Mac と、Roslyn (Microsoft のオープンソースの .NET コンパイラ プラットフォーム) との統合により、より多くのリファクタリング操作が可能になります。

## <a name="renaming"></a>名前の変更

コード識別子 (クラス名やプロパティ名など) で *[名前の変更]* リファクタリング コマンドを使用して、その識別子のすべての出現箇所を検索し、変更することができます。 シンボルの名前を変更するには、次のように、そのシンボルを右クリックし、 **[リファクター]、[名前の変更]** の順に選択するか、**Command + R** キー バインドを使用します。

![[名前の変更] メニュー項目](media/refactoring-renaming1.png)

これでシンボルとその参照が強調表示されます。 新しい名前の入力を開始すると、コードのすべての参照が自動的に変更され、**Enter** キーを押して、名前の変更が完了したことを示すことができます。

![名前の変更と識別子](media/refactoring-renaming2.png)

## <a name="context-actions"></a>コンテキスト アクション

コンテキスト アクションでは、C# コードを検査して、使用可能なすべてのリファクタリング オプションを表示することができます。

**[解決]** と **[リファクター]** コンテキスト項目は、1 つの *[クイック修正...]* 項目に結合され、使用可能なコンテキスト アクションがすべて提供されます。

![コンテキスト項目を表示する](media/refactoring-context-action.png)

コンテキスト アクションのいずれかにカーソルを合わせると、コードで追加または削除する内容をプレビューすることができます。

また、コードの任意の場所で **Option + Enter** キーを押すこともできます。

![Option + Enter キーを使用した場合のコンテキスト項目](media/refactoring-image2a.png)

これらのオプションを有効にするには、オプションの **[Visual Studio for Mac]、[基本設定]、[テキスト エディター]、[ソースの解析]** の順に移動して、 *[開いているファイルのソース解析を有効にする]* を選択する必要があります

![ソース解析の有効化](media/refactoring-options.png)

推奨される 100 を超える実行可能なアクションがあります。これらを有効または無効にする場合は、 **[Visual Studio for Mac]、[基本設定]、[ソースの解析]、[C#]、[コード アクション]** の順に参照し、アクションの横にあるボックスをオンまたはオフにします。

![C# のソース解析アクション](media/refactoring-image3a.png)

### <a name="common-context-actions"></a>一般的なコンテキスト アクション

一般的に使用されるコンテキスト アクションのいくつかを以下で説明します。

#### <a name="extract-method"></a>メソッドの抽出

メソッドの抽出リファクタリング操作では、既存のメンバーの選択したコードを抽出することで新しいメソッドを作成することができます。 このアクションでは以下の 2 つの処理を行います。

* 選択したコードを含む新しいメソッドを作成する。
* 選択したコードがあった場所で新しいメソッドを呼び出す。

##### <a name="example"></a>例

1. 次のコードを追加します。

```csharp
    class MainClass
    {

        double CalculatePyramidVolume(double baseArea, double height)
        {

            double volume = (baseArea * height) / 3;

            return volume;
        }
    }
```

2. `double volume = (baseArea * height) / 3;` という行を強調表示し、それを右クリックして、 **[リファクター]、[メソッドの抽出]** の順に選択します。

3. 方向キーを使用して、コードで新しいメソッドを配置する場所を選択します。

#### <a name="encapsulate-field"></a>フィールドのカプセル化

フィールドのカプセル化操作では、既存のフィールドからプロパティを作成することができ、新しく作成されたプロパティを参照するためにコードが更新されます。 フィールドをカプセル化するプロパティを作成しすることで、パブリック フィールドへの直接アクセスを禁止します。これは、他のオブジェクトで変更できなくなることを意味します。

このアクションでは次の処理を行います。

* アクセス修飾子をプライベートに変更する。
* フィールドのゲッターとセッターを生成する (フィールドが読み取り専用である場合を除く。読み取り専用の場合はゲッターのみが作成されます)。

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