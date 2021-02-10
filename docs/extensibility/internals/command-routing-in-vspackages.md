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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d05612f9d15c3670411a7901157570fbb3e315a3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99939995"
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
