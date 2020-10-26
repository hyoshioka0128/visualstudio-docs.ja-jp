---
title: Visual Studio デバッガーの機能拡張 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712506"
---
# <a name="visual-studio-debugger-extensibility"></a>Visual Studio デバッガーの機能拡張
Visual Studio には、完全にインタラクティブなソースコードデバッガーが含まれており、プログラムのバグを追跡するための強力で使いやすいツールを提供します。 デバッガーは、Visual Basic、C#、C/c + +、および JavaScript を完全にサポートしています。 ただし、 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=21835)から入手できるを使用すると、他のプログラミング言語を同じ豊富な機能を備えたデバッガーでサポートできます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッガーは、デバッグ対象の言語に固有の、デバッグコンポーネントへの共通のフロントエンド (つまり、ユーザーインターフェイス) です。 新しい言語では、デバッガーによるサポートに必要なの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、デバッグエンジン (DE) などの必要なバックエンドコンポーネントを作成することだけです。 この時点で、が [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 登場します。

 には、 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 新しい DE を作成するために必要なすべての要素への完全な参照が含まれています。 また、作業を開始するためのサンプルとチュートリアルも用意されています。

 デバッグをサポートする言語プロジェクトシステムの完全なサンプルについては、 [IronPython サンプル](https://www.microsoft.com/download/details.aspx?id=55984)を参照してください。

 次のセクションでは、を使用してデバッガーを拡張する方法について説明し [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ます。

## <a name="in-this-section"></a>このセクションの内容
 [はじめ](../../extensibility/debugger/getting-started-with-debugger-extensibility.md) に [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグの機能と SDK をインストールする方法について説明します。

 [カスタムデバッグエンジンを作成する](../../extensibility/debugger/creating-a-custom-debug-engine.md) De をデタッチするためのプログラムの準備から、カスタムの DE プロセスについて説明します。

 [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md) 式エバリュエーターを記述する必要があるかどうかについて説明します。

 [デバッグエンジンの実装方法を選択する](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md) DE を実装する方法について説明します。

 [参照](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md) デバッグ API について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

 [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md) 共通言語ランタイムの式エバリュエーターサンプルとデバッグエンジンサンプルへのリンクが含まれています。
