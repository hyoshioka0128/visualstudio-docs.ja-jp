---
title: Vspackage | のコマンドルーティングMicrosoft Docs
description: Vspackage のコマンドルーティングと、Visual Studio で実行されるコンテキストに基づいてコマンドがどのようにルーティングされるかについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 8168fbe3ad5ba9b1b332aebc4675ecd8e752ee7e
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305218"
---
# <a name="command-routing-in-vspackages"></a>Vspackage でのコマンドルーティング
コマンドは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 実行されたコンテキストに基づいてルーティングされます。 初期コンテキストからグローバルコンテキストにルーティングされます。

## <a name="in-this-section"></a>このセクションの内容
- [コマンドルーティングアルゴリズム](../../extensibility/internals/command-routing-algorithm.md)

 コマンドルーティングの解決順序について説明します。

- [コマンドの可用性](../../extensibility/internals/command-availability.md)

 コマンドルーティングについて説明します。

- [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 マネージコードと COM 間のコマンドのルーティングに関する考慮事項について説明します。

## <a name="related-sections"></a>関連項目
- [選択コンテキストオブジェクト](../../extensibility/internals/selection-context-objects.md)

 ウィンドウに対するユーザーの選択コンテキストフォーカスを判断する方法のモデルについて説明します。

- [コマンド、メニュー、およびツールバー](../../extensibility/internals/commands-menus-and-toolbars.md)

 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。
