---
title: VS パッケージでのコマンド ルーティング |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing, Visual Studio SDK
ms.assetid: a9c7f9ae-3594-4557-a314-8cf76f5f8772
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 957ddcca46365a882609c15c96d666c2848ace6c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709552"
---
# <a name="command-routing-in-vspackages"></a>VS パッケージでのコマンド ルーティング
コマンドは、実行される[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]コンテキストに基づいてルーティングされます。 初期コンテキストからグローバル コンテキストにルーティングされます。

## <a name="in-this-section"></a>このセクションの内容
- [コマンドルーティングアルゴリズム](../../extensibility/internals/command-routing-algorithm.md)

 コマンド ルーティング解決の順序を記述します。

- [コマンドの可用性](../../extensibility/internals/command-availability.md)

 コマンド ルーティングについて説明します。

- [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 マネージ コードと COM 間のコマンドのルーティングに関する考慮事項について説明します。

## <a name="related-sections"></a>関連項目
- [選択コンテキストオブジェクト](../../extensibility/internals/selection-context-objects.md)

 ウィンドウでユーザーの選択コンテキストフォーカスを決定する方法のモデルについて説明します。

- [コマンド、メニュー、およびツールバー](../../extensibility/internals/commands-menus-and-toolbars.md)

 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。
