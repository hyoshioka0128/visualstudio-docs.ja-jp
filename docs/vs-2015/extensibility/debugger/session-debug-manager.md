---
title: セッションデバッグマネージャー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- session debug manager, unifying session views
- session debug manager, broadcasting
- debugging [Debugging SDK], session debug manager
- session debug manager
- session debug manager, debug engine multiplexing
- session debug manager, delegating
ms.assetid: fbb1928d-dddc-43d1-98a4-e23b0ecbae09
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9fd7c7555c19f850a15161f6fba00b1184621a9e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157830"
---
# <a name="session-debug-manager"></a>セッション デバッグ マネージャー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

セッションデバッグマネージャー (SDM) は、任意の数のコンピューター上の複数のプロセスで任意の数のプログラムをデバッグする、任意の数のデバッグエンジン (DE) を管理します。 デバッグエンジンのマルチプレクサーに加えて、SDM はデバッグセッションを IDE に統合したビューを提供します。  
  
## <a name="session-debug-manager-operation"></a>セッションデバッグマネージャーの操作  
 セッションデバッグマネージャー (SDM) は、DE を管理します。 1台のコンピューターで複数のデバッグエンジンが同時に実行されている可能性があります。 DEs を多重化するために、SDM は DEs から複数のインターフェイスをラップし、1つのインターフェイスとして IDE に公開します。  
  
 パフォーマンスを向上させるために、一部のインターフェイスは多重化されません。 代わりに、これらは DE から直接使用され、これらのインターフェイスへの呼び出しは SDM を通過しません。 たとえば、メモリ、コード、ドキュメントコンテキストで使用されるインターフェイスは多重化されません。これは、特定のプログラムによってデバッグされる特定の命令、メモリ、またはドキュメントを特定の DE によってデバッグするためです。 そのような通信レベルに他の DE を含める必要はありません。  
  
 これは、すべてのコンテキストに当てはまるわけではありません。 式の評価コンテキストインターフェイスへの呼び出しは、SDM を経由します。 式の評価中に、SDM は IDE に与える [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスをラップします。これは、その式が評価されるときに、同じスレッドで実行されている場合と同じプロセスでプログラムをデバッグする複数の DEs が含まれる可能性があるためです。  
  
 SDM は通常、委任メカニズムとして機能しますが、ブロードキャストメカニズムとして機能する場合があります。 たとえば、式の評価中、SDM は、指定されたスレッドでコードを実行できることをすべての DEs に通知するためのブロードキャストメカニズムとして機能します。 同様に、SDM が停止イベントを受け取ると、実行を停止するすべてのプログラムにブロードキャストされます。 ステップが呼び出されると、SDM は、実行を継続できるすべてのプログラムにブロードキャストします。 ブレークポイントは、すべての DE にもブロードキャストされます。  
  
 SDM は、現在のプログラム、スレッド、またはスタックフレームを追跡しません。 プロセス、プログラム、スレッドの情報は、特定のデバッグイベントと共に SDM に送信されます。  
  
## <a name="see-also"></a>参照  
 [デバッグエンジン](../../extensibility/debugger/debug-engine.md)   
 [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)   
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
