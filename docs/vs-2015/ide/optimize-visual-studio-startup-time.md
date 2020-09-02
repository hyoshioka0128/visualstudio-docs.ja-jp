---
title: 起動時間を最適化する |Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
helpviewer_keywords:
- startup time [Visual Studio]
- optimizing startup time [Visual Studio]
- speed up start time [Visual Studio]
ms.assetid: d1508121-8499-4084-8eb5-fa89fa7b17d3
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0f00bbc7741768852b5928b249dc7035bc440992
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670402"
---
# <a name="optimize-visual-studio-startup-time"></a>Visual Studio の起動時間の最適化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio は常に、可能な限り迅速に起動することが理想的です。 ただし、Visual Studio 拡張機能と開いているツール ウィンドウは、起動時に自動的に読み込まれるため、起動時間に悪影響を与える可能性があります。 **[Visual Studio のパフォーマンスの管理]** ウィンドウでは、Visual Studio の起動時間に影響する拡張機能と機能を確認できるだけでなく、読み込み動作を決定し、Visual Studio の起動速度について、より詳細に制御することもできます。

## <a name="control-startup-behavior"></a>起動の動作の制御

起動時間が長くならないように、Visual Studio 2017 以降では、オンデマンド読み込みの方法を使用して、起動時に拡張機能が読み込まれないようにします。 これは、Visual Studio の起動後すぐに拡張機能を開くのではなく、起動後、必要に応じて非同期に開くことを意味します。 また、前の Visual Studio セッションでツール ウィンドウが開いたままである場合、スタートアップ時間が長くなる可能性があるため、Visual Studio は起動時間に影響しないようにより合理的な方法でツール ウィンドウを開きます。

Visual Studio で起動の遅延が検出されると、ポップアップ メッセージが表示され、拡張機能またはツール ウィンドウが原因で遅延が発生していることを警告します。 メッセージには **[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスへのリンクも示されます。ダイアログ ボックスには、起動のパフォーマンスに影響している拡張機能とツール ウィンドウがリストされます。 このダイアログ ボックスでは、起動時のパフォーマンスを向上させるために拡張機能とツール ウィンドウの設定を変更することができます。

![Visual Studio のパフォーマンスの管理-ポップアップ](../ide/media/vside-perfdialog-popup.PNG "Visual Studio のパフォーマンスの管理-ポップアップ")

**[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスには、**[拡張機能]** と **[ツール ウィンドウ]** という 2 つのカテゴリがあります。

### <a name="control-extensions"></a>拡張機能の制御
拡張機能が Visual Studio の起動の遅延の原因となっている場合、いずれかの種類の拡張機能を選択したときに、**[Visual Studio のパフォーマンスを管理]** ダイアログ ボックスに拡張機能が表示されます。 起動時間への影響 (**[影響]** セクションにリストされている) が受け入れがたい場合には、**[無効にする]** ボタンを選び、起動時には常に拡張機能を無効にするよう選択することができます。 拡張機能マネージャーまたは [Visual Studio のパフォーマンスの管理] ダイアログ ボックスを使用して、今後のセッションで拡張機能を再度有効にすることができます。

![Visual Studio のパフォーマンスの管理-拡張機能](../ide/media/vside-perfdialog-extensions.PNG "Visual Studio のパフォーマンスの管理-拡張機能")

起動時だけでなく、ソリューションの読み込み時やユーザーの入力時に読み込まれる拡張機能を無効にすることもできます。 その場合は、該当するシナリオを選択して、関連する拡張機能のリストを表示するだけです。

### <a name="control-tool-windows"></a>ツール ウィンドウの制御
ツール ウィンドウが Visual Studio の起動の遅延の原因となっている場合、既定の動作のままにしておく (起動速度にメリットなし) か、次の 2 つの動作のいずれかを選択して、動作をオーバーライドすることができます。

- **起動時にウィンドウを表示しない:** このオプションを選択すると、Visual Studio を開いたときに指定されたツール ウィンドウが常に閉じられます。前のセッションで開いたままの場合でも同じです。 ツール ウィンドウはメニューから開くことができます。
- **起動時にウィンドウを自動的に隠す:** ツール ウィンドウが前のセッションで開いたままの場合、このオプションを選択すると、起動時にツール ウィンドウのグループが折りたたまれ、ツール ウィンドウが初期化されないようになります。 これは、ツール ウィンドウがまだ使用可能でも、Visual Studio の起動時間には悪影響しなくなるため、ツール ウィンドウを頻繁に使用する場合に適しています。

![Visual Studio のパフォーマンスの管理-ツールウィンドウ](../ide/media/vside-perfdialog-toolwindows.PNG "Visual Studio のパフォーマンスの管理-ツールウィンドウ")

後で気が変わった場合、**[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスでこれらのオプションを元に戻すことができます。 **[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスを開くには、メニュー バーで、**[ヘルプ]**、**[Visual Studio のパフォーマンスの管理]** の順に選択します。
