---
title: ファイルとフォルダーの信頼の設定
description: Visual Studio を安全に保護するファイルとフォルダーの信頼設定を変更する方法について説明します。
author: 2percentsilk
ms.author: allisb
ms.date: 09/05/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.PathTrustOptions
helpviewer_keywords:
- file security
- folder security
- mark of the web
- trusted files
- trusted folders
ms.openlocfilehash: 492a94962d255a9d18dcabdababf7fa6a540ada1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88197387"
---
# <a name="configure-trust-settings-for-files-and-folders"></a>ファイルとフォルダーの信頼設定の構成

Visual Studio では、[Mark of the Web](/previous-versions/windows/internet-explorer/ie-developer/compatibility/ms537628(v=vs.85)) を持つプロジェクトを開く前に、ユーザーの承認が求められます。 セキュリティ強化のため、Mark of the Web 属性を持つ、または*信頼済み*と指定されていない任意のファイルまたはフォルダーを開く前に、ユーザーの承認を求めるように Visual Studio を構成することもできます。 ファイルとフォルダーのチェックは、既定で無効になっています。

> [!WARNING]
> それでも、承認する前に、ファイル、フォルダー、またはソリューションが信頼できる人または信頼できる場所から提供されたものであることを確認する必要があります。

## <a name="configure-trust-settings"></a>信頼設定の構成

信頼設定を変更するには、次の手順を行います。

1. **[ツール]**  >  **[オプション]**  >  **[信頼の設定]** を開き、右側のウィンドウで **[信頼設定の構成]** リンクを選択します。

2. ファイルとフォルダーのチェックのレベルを選択します。 それぞれに異なるチェック レベルを選択できます。 オプションは次のとおりです。

   * **[No verification]\(確認しない\)** : Visual Studio でチェックは実行されません。

   * **[Verify mark of the web attribute]\(Mark of the Web 属性を確認する\)** : ファイルまたはフォルダーに Mark of the Web 属性がある場合、Visual Studio によってブロックされ、開くためのアクセス許可が求められます。

   * **[Verify path is trusted]\(パスが信頼されていることを確認する\)** : ファイルまたはフォルダーが **[信頼されているパス]** リストにない場合、Visual Studio によってブロックされ、開くためのアクセス許可が求められます。

   ![信頼の確認オプション](media/trust-settings.png)

## <a name="add-trusted-paths"></a>信頼されているパスの追加

信頼されているパスを追加するには、次の手順を行います。

1. **[ツール]**  >  **[オプション]**  >  **[信頼の設定]** を開き、右側のウィンドウで **[信頼設定の構成]** リンクを選択します。

2. **[信頼の設定]** ダイアログ内の **[追加]** をクリックして、 **[ファイル]** または **[フォルダー]** を選択します。

3. 信頼済みリストに追加するファイルまたはフォルダーに移動して選択します。

   ファイルまたはフォルダーのパスが **[信頼されているパス]** リストに表示されます。

   ![追加された信頼されているパス](media/trusted-paths.png)

## <a name="remove-trusted-paths"></a>信頼されているパスの削除

信頼されているパスを削除するには、次の手順を行います。

1. **[ツール]**  >  **[オプション]**  >  **[信頼の設定]** を開き、右側のウィンドウで **[信頼設定の構成]** リンクを選択します。

2. **[信頼されているパス]** リストで削除するパスを選択し、 **[削除]** をクリックします。

   > [!TIP]
   > 複数のエントリを選択するには、**Shift** キーを押しながらパスを選択します。

   選択したパスが **[信頼されているパス]** リストから削除されます。
