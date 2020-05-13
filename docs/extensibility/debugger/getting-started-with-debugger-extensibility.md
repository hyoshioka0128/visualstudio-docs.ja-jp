---
title: デバッガー拡張機能の概要 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 153db8889c78890a31a2e8003e6aa95ed24a02eb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738593"
---
# <a name="get-started-with-debugger-extensibility"></a>デバッガーの機能拡張の概要
では[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]、環境内からプログラムをデバッグするために使用するデバッガ コンポーネントを作成およびカスタマイズするために必要[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]な情報を提供します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグは、以前[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のデバッガーで実行される広範なユーザビリティ テストから派生した改善を追加しました。 デバッグを使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]して、複数言語のアプリケーションをステップ実行したり、アプリケーションや多言語ソリューションのデバッグ中に変数のリアルタイムで編集を実装したりできます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグは、デバッグ中のプログラムでプロセス外で実行されるため、アプリケーションのプロセス空間での侵入が少なくなります。 したがって、デバッグ プログラムに影響を与えることなく、デバッガーと対話するコンポーネントを簡単に作成できます。

 を最大限に活用[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]するには、次の項目について理解している必要があります。

- 統合[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]開発環境 (IDE)

- C++ プログラミング言語

- ATL COM

## <a name="in-this-section"></a>このセクションの内容
 [デバッガーを拡張するためのロードマップ](../../extensibility/debugger/roadmap-for-extending-the-debugger.md)コンパイラとその出力に応じて、製品にデバッグを実装するプロセスについて説明します。

 [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグ エンジン (DE)、式エバリュエーター (EE)、およびシンボル ハンドラー (SH) を含むデバッグ コンポーネントの概要を提供します。

 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)デバッグアーキテクチャの主要な概念について説明します。

 [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)デバッグ エンジン (DE) がコード、ドキュメント、および式の評価コンテキスト内で同時に動作する方法について説明します。 3 つのコンテキストのそれぞれについて、そのコンテキストに関連する場所、位置、または評価について説明します。

 [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)プログラムの起動や式の評価など、さまざまなデバッグ タスクへのリンクが含まれています。
