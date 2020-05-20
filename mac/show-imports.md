---
title: インポート項目を表示する
description: Visual Studio for Mac で [Show Import Items] (インポート項目を表示) を使用して IntelliSense を展開します。
author: cobey
ms.author: cobey
ms.date: 03/29/2019
ms.assetid: C7782BF3-016F-4B41-8A81-85FC540A1A8F
ms.custom: video
ms.openlocfilehash: 964fbbf2f46e2495184b01c47cba888a93f24ea8
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "75439104"
---
# <a name="show-import-items"></a>インポート項目を表示する

Visual Studio for Mac では、IntelliSense の入力候補一覧に、使用可能なすべての型を、お使いのプロジェクトにインポートされていないものも含めて表示することができます。 インポートされていない項目を選択すると、正しい `using` ステートメントがソース ファイルに追加されます。

![[Show Import Items]\(インポート項目を表示\) の概要](media/importitems-overview.gif)

## <a name="how-to-enable"></a>有効にする方法

この機能を有効にするには、**[Visual Studio]** > **[ユーザー設定]** を使用して **[ユーザー設定]** を開き、**[テキスト エディター]** > **[IntelliSense]** に移動します。 **[Show Import Items]\(インポート項目を表示\)** ボックスをオンにして、IntelliSense で追加の項目を有効にします。

![[Show Import Items]\(インポート項目を表示\) のオプション](media/show-import-items.png)

## <a name="usage"></a>使用方法

**[Show Import Items]\(インポート項目を表示\)** を有効にしたら、この機能を使用して項目をインポートする手順は、IntelliSense の通常の操作に似ています。 コードを入力すると、有効な項目を含む入力候補一覧が作成されます。 これには、まだインポートされていない項目も含まれます。 インポートされていない項目には、項目の右側にその完全な名前空間が表示されます。これにより、プロジェクトに取り込まれるインポートを確認できます。

![[Show Import Items]\(インポート項目を表示\) の一覧](media/show-import-items-list.png)

IntelliSense の一覧では、現在 `using` ステートメントによって参照されていないメンバーの横に、名前空間が表示されます。 これらの項目のいずれかを一覧から選択すると、そのメンバーがコードに追加され、"_さらに_"、`using` ステートメントがファイルの先頭に追加されます。 コードで既に参照されている型のメンバーについては、IntelliSense で名前空間は表示されません。

## <a name="see-also"></a>関連項目

- [クイック アクション (Windows 上の Visual Studio)](/visualstudio/ide/quick-actions)
- [コードのリファクタリング (Windows 上の Visual Studio)](/visualstudio/ide/refactoring-in-visual-studio)
