---
title: ビジュアル スタジオ デバッガーの機能拡張 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff4222b555fab73914776725fc79581f29fa5e53
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712506"
---
# <a name="visual-studio-debugger-extensibility"></a>デバッガーの機能拡張
Visual Studio には完全に対話的なソース コード デバッガが用意されており、プログラムのバグを追跡するための強力で使いやすいツールが提供されています。 デバッガーは、Visual Basic、C#、C/C++、および JavaScript を完全にサポートしています。 ただし、 Microsoft [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)][ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=21835)から入手できる を使用すると、同じ機能を備えた他のプログラミング言語をデバッガーでサポートできます。

 デバッガー[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、デバッグ対象の言語に固有のデバッグ コンポーネントに共通のフロント エンド (つまり、ユーザー インターフェイス) です。 新しい言語では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグ エンジン (DE) などの必要なバックエンド コンポーネントを作成する必要があるデバッガーで必要なすべてが必要です。 この点は、入[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]ってくるところです。

 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]には、新しい DE[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を作成するために必要なすべての要素への完全な参照が含まれています。 また、開始に役立つサンプルやチュートリアルもあります。

 デバッグをサポートする言語プロジェクト システムの完全なサンプルについては、 [IronPython のサンプル](https://www.microsoft.com/download/details.aspx?id=55984)を参照してください。

 以降のセクションでは、 を使用してデバッガーを拡張[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
 [はじめに](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)デバッグの提供[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]内容と SDK のインストール方法について説明します。

 [カスタム デバッグ エンジンを作成する](../../extensibility/debugger/creating-a-custom-debug-engine.md)DE のプログラムの準備から DE のデタッチまで、カスタム DE プロセスについて説明します。

 [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)式エバリュエーターを記述する必要があるかどうかを説明します。

 [デバッグ エンジン実装戦略を選択する](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)DE を実装する方法について説明します。

 [リファレンス](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)デバッグ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]API について説明します。

 [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md)共通言語ランタイム式エバリュエーターサンプルとデバッグ エンジンのサンプルへのリンクが含まれています。
