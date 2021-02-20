---
title: デバッガーコンテキスト |Microsoft Docs
description: Visual Studio デバッグエンジンが個別のコンテキスト内でどのように動作するかについて説明します。コードコンテキスト、ドキュメントコンテキストまたは位置、式評価コンテキスト。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 89d2da35fb7ffa81ec9f6a882e6b35d42fc8f00c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952435"
---
# <a name="debugger-contexts"></a>デバッガーコンテキスト
デバッグでは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグエンジン (DE) は、次のように複数の異なるコンテキスト内で同時に動作します。

- プログラムの実行ストリーム内の現在の位置を記述するコードコンテキスト。

- ドキュメントコンテキストまたは位置。ソースドキュメント内の現在位置を記述します。

- 式の評価コンテキスト。式の評価が行われるコンテキストを記述します。

## <a name="in-this-section"></a>このセクションの内容
 [コードコンテキスト](../../extensibility/debugger/code-context.md) コードコンテキストについては、今日の実行時アーキテクチャにおけるプログラムの命令ストリームのアドレスとして、また、コードが命令によって表されない場合がありますが、他の方法では nontraditional 言語について説明します。

 [ドキュメントの位置](../../extensibility/debugger/document-position.md) IDE で認識されているソースファイル内の位置を抽象化することによって、Visual Studio のデバッグでのドキュメントの位置を定義します。

 [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md) ソースファイルに関連して Visual Studio のデバッグで表現されるドキュメントコンテキストについて説明します。 また、シンボルハンドラーがコードコンテキストをドキュメントコンテキストにマップする方法についても説明します。

 [式の評価コンテキスト](../../extensibility/debugger/expression-evaluation-context.md) Visual Studio の式の評価コンテキストに関する情報を提供します。 たとえば、スタックフレームに関連付けられている式の評価コンテキストでは、ローカル変数、メソッドパラメーター、およびクラスメンバーを評価するためのコンテキストが提供されます。

## <a name="related-sections"></a>関連項目
 [デバッグの概念](../../extensibility/debugger/debugger-concepts.md) デバッグアーキテクチャの主要概念について説明します。

 [コンポーネントのデバッグ](../../extensibility/debugger/debugger-components.md) デバッグエンジン (DE)、式エバリュエーター (EE)、およびシンボルハンドラー (SH) など、Visual Studio のデバッグコンポーネントの概要について説明します。

 [デバッグタスク](../../extensibility/debugger/debugging-tasks.md) プログラムの起動や式の評価など、さまざまなデバッグタスクへのリンクが含まれています。
