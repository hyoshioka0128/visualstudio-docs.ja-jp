---
title: デバッガコンテキスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 56825fe299147e60c5ed9dfcefa491a427ab59e4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738977"
---
# <a name="debugger-contexts"></a>デバッガーのコンテキスト
デバッグ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、デバッグ エンジン (DE) は、次のように、いくつかの異なるコンテキスト内で同時に動作します。

- プログラムの実行ストリーム内の現在の場所を記述するコード コンテキスト。

- ドキュメントのコンテキストまたは位置は、ソース ドキュメント内の現在の位置を記述します。

- 式の評価が行われるコンテキストを記述する式の評価コンテキスト。

## <a name="in-this-section"></a>このセクションの内容
 [コード コンテキスト](../../extensibility/debugger/code-context.md)今日の実行時アーキテクチャのプログラムの命令ストリームのアドレスとしてのコード コンテキストと、コードが命令で表されない場合がある非伝統的な言語について説明します。

 [ドキュメントの位置](../../extensibility/debugger/document-position.md)IDE に認識されているソース ファイル内の位置を抽象化して、Visual Studio のデバッグにおけるドキュメントの位置を定義します。

 [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)Visual Studio のデバッグで、ソース ファイルに関連してドキュメント コンテキストが表す内容について説明します。 シンボル ハンドラーがコード コンテキストをドキュメント コンテキストにマップする方法についても説明します。

 [式評価コンテキスト](../../extensibility/debugger/expression-evaluation-context.md)Visual Studio の式評価コンテキストに関する情報を提供します。 たとえば、スタック フレームに関連付けられた式評価コンテキストは、ローカル変数、メソッド パラメーター、およびクラス メンバーを評価するためのコンテキストを提供します。

## <a name="related-sections"></a>関連項目
 [デバッグの概念](../../extensibility/debugger/debugger-concepts.md)デバッグアーキテクチャの主要な概念について説明します。

 [コンポーネントのデバッグ](../../extensibility/debugger/debugger-components.md)デバッグ エンジン (DE)、式エバリュエーター (EE)、およびシンボル ハンドラー (SH) を含む Visual Studio のデバッグ コンポーネントの概要を説明します。

 [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)プログラムの起動や式の評価など、さまざまなデバッグ タスクへのリンクが含まれています。
