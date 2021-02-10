---
title: セッションデバッグマネージャー |Microsoft Docs
description: セッションデバッグマネージャーについて説明します。このマネージャーでは、複数のプロセスにおける複数のデバッグエンジンデバッグプログラムを、任意の数のコンピューターで管理します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- session debug manager, unifying session views
- session debug manager, broadcasting
- debugging [Debugging SDK], session debug manager
- session debug manager
- session debug manager, debug engine multiplexing
- session debug manager, delegating
ms.assetid: fbb1928d-dddc-43d1-98a4-e23b0ecbae09
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d67716f78249bda5d316ffde175b80f4ef1c1e45
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960781"
---
# <a name="session-debug-manager"></a>セッションデバッグマネージャー
セッションデバッグマネージャー (SDM) は、任意の数のコンピューターで複数のプロセス内の任意の数のプログラムをデバッグする、任意の数のデバッグエンジン (DE) を管理します。 デバッグエンジンのマルチプレクサーに加えて、SDM はデバッグセッションを IDE に統合したビューを提供します。

## <a name="session-debug-manager-operation"></a>セッションデバッグマネージャーの操作
 セッションデバッグマネージャー (SDM) は、DE を管理します。 1台のコンピューターで複数のデバッグエンジンを同時に実行することもできます。 DEs を多重化するために、SDM は DEs から複数のインターフェイスをラップし、1つのインターフェイスとして IDE に公開します。

 パフォーマンスを向上させるために、一部のインターフェイスは多重化されていません。 代わりに、これらは DE から直接使用され、これらのインターフェイスへの呼び出しは SDM を通過しません。 たとえば、メモリ、コード、ドキュメントコンテキストで使用されるインターフェイスは多重化されません。これは、特定のプログラムによってデバッグされる特定の命令、メモリ、またはドキュメントを特定の DE によってデバッグするためです。 そのような通信レベルに他の DE を含める必要はありません。

 これは、すべてのコンテキストに当てはまるわけではありません。 式の評価コンテキストインターフェイスへの呼び出しは、SDM を経由します。 式の評価中に、SDM は IDE に与える [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスをラップします。これは、その式が評価されるときに、同じスレッドで実行されている場合と同じプロセスでプログラムをデバッグする複数の DEs が含まれる可能性があるためです。

 SDM は通常、委任メカニズムとして機能しますが、ブロードキャストメカニズムとして機能する場合があります。 たとえば、式の評価中、SDM は、指定されたスレッドでコードを実行できることをすべての DEs に通知するためのブロードキャストメカニズムとして機能します。 同様に、SDM が停止イベントを受け取ると、実行を停止するプログラムにブロードキャストされます。 ステップが呼び出されると、SDM は実行を継続できるプログラムにブロードキャストします。 ブレークポイントは、すべての DE にもブロードキャストされます。

 SDM は、現在のプログラム、スレッド、またはスタックフレームを追跡しません。 プロセス、プログラム、スレッドの情報は、特定のデバッグイベントと共に SDM に送信されます。

## <a name="see-also"></a>関連項目
- [デバッグエンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)
- [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)
