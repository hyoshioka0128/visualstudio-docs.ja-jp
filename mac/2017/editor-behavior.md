---
title: コードのフォーマット
description: この記事では、Visual Studio for Mac のテキスト エディターの動作を変更できるさまざまなオプションについて説明します
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: 81EE4460-26EB-4BB0-9297-932E1F88E4B8
ms.openlocfilehash: dca21119a73c03b63a273f7b4c22d70ecdb2a583
ms.sourcegitcommit: 370cc7fd2e11ede6d8215c8d81963a8307614550
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74984683"
---
# <a name="editor-behavior"></a>エディターの動作

入力時にコードの書式が設定されるようにエディターの動作を設定することができます。 これらのアクションは、 **[Visual Studio] > [ユーザー設定] > [テキスト エディター] > [動作]** で設定します。よく使用される機能の一部を以下で説明します。

![エディターの [動作] オプション](media/source-editor-image9.png)

* 新しいクラス、メソッド、またはプロパティを作成するときに、対応する右波かっこをコードに自動的に追加することができます。 このオプションをオンにして `{` と入力すると、`}` が自動的に追加されます。
* セミコロンや波かっこなどの文字列を入力すると、実行時のコード書式設定がトリガーされ、設定されている書式設定が列挙されます。
* また、保存時にファイルの書式を選択することもできます。この機能を利用すると、好きなようにコードを作成し、既存のユーザー設定に従って IDE で自動的にコードの書式を設定することができます。
* [インデント] は、[なし]、[自動]、または [スマート] に設定できます。 機能は次のとおりです。
  * なし - カレットを次行の行頭に設定します
  * 自動 - カレットを次行の同じカラムに設定します
  * スマート - コードに基づいて次行にインデントを設定します
* 単語を区切る動作は、OS によって異なります。ナビゲーションのために、テキスト エディターは単語の開始位置と終了位置を認識している必要があります。 書式は Unix または Windows に設定できます。

また、XML、CSS、HTML、および JSON の書式設定規則も設定できます。

## <a name="see-also"></a>関連項目

- [コードのスタイル設定 (Windows の Visual Studio)](/visualstudio/ide/code-styles-and-quick-actions)
