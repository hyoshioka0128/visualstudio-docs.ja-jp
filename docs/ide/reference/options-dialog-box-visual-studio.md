---
title: '[オプション] ダイアログ'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.toolsoptionspages
helpviewer_keywords:
- Tools Options settings
- Options dialog box
- Options dialog box, development environment
- tools [Visual Studio], customizing
ms.assetid: 02b09877-1df1-4531-a0d1-a4ca17c7f857
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6c864a10af9ad15d47e2342bb148af464b8f2a0d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591503"
---
# <a name="options-dialog-box-visual-studio"></a>[オプション] ダイアログ ボックス (Visual Studio)

**[オプション]** ダイアログ ボックスでは、必要に応じて統合開発環境 (IDE) を構成することができます。 たとえば、プロジェクトの既定の保存場所の確立、ウィンドウの既定の外観や動作の変更、よく使用されるコマンドのショートカットの作成などを行うことができます。 開発言語やプラットフォームに固有のオプションもあります。 **[オプション]** には **[ツール]** メニューからアクセスできます。

## <a name="layout-of-the-options-dialog-box"></a>[オプション] ダイアログ ボックスのレイアウト

**[オプション]** ダイアログ ボックスは 2 つの部分 (左側のナビゲーション ウィンドウと右側の表示領域) に分かれています。 ナビゲーション ウィンドウのツリー コントロールには、[環境]、[テキスト エディター]、[プロジェクトおよびソリューション]、および [ソース管理] などのフォルダー ノードが含まれています。 任意のフォルダー ノードを展開すると、その中に含まれるオプションのページがリストされます。 特定のページのノードを選択すると、表示領域にそのオプションが表示されます。

IDE 機能のオプションは、この機能がメモリに読み込まれるまでは、ナビゲーション ウィンドウには表示されません。 したがって、前のセッションを終了したときに表示されていたオプションが、新規セッションを開始した時点では表示されない場合があります。 プロジェクトを作成するか、特定のアプリケーションを使用するコマンドを実行すると、関連するオプションのノードが [オプション] ダイアログ ボックスに追加されます。 追加されたこれらのオプションは、IDE 機能がメモリにある限り有効です。

> [!NOTE]
> 一部の設定コレクションでは、[オプション] ダイアログ ボックスのナビゲーション ウィンドウに表示されるページ数のスコープが設定されます。 **[すべての設定を表示]** を選択すると、使用可能なすべてのページを表示できます。

## <a name="how-options-are-applied"></a>オプションの適用方法

**[オプション]** ダイアログ ボックスで [OK] をクリックすると、すべてのページのすべての設定が保存されます。 任意のページで [キャンセル] をクリックすると、他の **[オプション]** ページで行ったものを含め、すべての変更要求がキャンセルされます。 [[フォントおよび色] ([オプション] ダイアログ ボックス - [環境])](../../ide/reference/fonts-and-colors-environment-options-dialog-box.md) での変更など、オプション設定に加えた一部の変更は、Visual Studio を閉じて再度開いたときに初めて有効になります。

### <a name="show-all-settings"></a>すべての設定を表示

**[すべての設定を表示]** のオンまたはオフの操作は、 **[OK]** をクリックしていなくても、 **[オプション]** ダイアログ ボックスで行ったすべての変更に適用されます。

## <a name="see-also"></a>関連項目

- [エディターのカスタマイズ](../how-to-change-text-case-in-the-editor.md)
