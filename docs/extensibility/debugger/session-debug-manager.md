---
title: セッション デバッグ マネージャ |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 953b4e948ef5e21531a3e73bceed3a363ed3cec5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712878"
---
# <a name="session-debug-manager"></a>セッション デバッグ マネージャー
セッション デバッグ マネージャー (SDM) は、任意の数のコンピューターで複数のプロセスでプログラムをデバッグしているデバッグ エンジン (DE) の任意の数を管理します。 デバッグ エンジンマルチプレクサであることに加えて、SDM はデバッグ セッションの統一されたビューを IDE に提供します。

## <a name="session-debug-manager-operation"></a>セッション デバッグ マネージャー操作
 セッション デバッグ マネージャー (SDM) は、DE を管理します。 1 台のコンピューターで同時に実行されているデバッグ エンジンが複数存在する場合があります。 DEs を多重化するために、SDM は DEs から多数のインターフェイスをラップし、それらを IDE に単一のインターフェイスとして公開します。

 パフォーマンスを向上させるために、一部のインターフェイスは多重化されません。 代わりに、DE から直接使用され、これらのインターフェイスへの呼び出しは SDM を経由しません。 たとえば、メモリ、コード、およびドキュメントのコンテキストで使用されるインターフェイスは、特定の DE によってデバッグされた特定のプログラム内の特定の命令、メモリ、またはドキュメントを参照するため、多重化されません。 そのレベルの通信に他の DE を関与する必要はありません。

 これはすべてのコンテキストに当てはまるわけではありません。 式評価コンテキスト インターフェイスへの呼び出しは、SDM を経由します。 式の評価中に、SDM は、式が評価されると、同じスレッドで実行されている可能性のある同じプロセス内のプログラムをデバッグしている複数の DE を含む可能性があるため、IDE に与える[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスをラップします。

 SDM は通常、委任メカニズムとして機能しますが、ブロードキャスト メカニズムとして機能する場合があります。 たとえば、式の評価中に、SDM は、指定されたスレッドでコードを実行できることをすべての DE に通知するブロードキャスト メカニズムとして機能します。 同様に、SDM は停止イベントを受信すると、実行を停止する必要があるプログラムにブロードキャストします。 ステップが呼び出されると、SDM は、実行を継続できるプログラムにブロードキャストします。 ブレークポイントは、すべての DE にもブロードキャストされます。

 SDM は、現在のプログラム、スレッド、またはスタック フレームを追跡しません。 プロセス、プログラム、およびスレッドの情報は、特定のデバッグ イベントと共に SDM に送信されます。

## <a name="see-also"></a>関連項目
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
- [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)
