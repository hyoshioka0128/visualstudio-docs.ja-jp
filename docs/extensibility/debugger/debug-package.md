---
title: パッケージのデバッグ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: de6240ea5d938d02f8415009203962e124ff049e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739027"
---
# <a name="debug-package"></a>デバッグ パッケージ
デバッグ パッケージは Visual Studio シェルで実行され、すべての UI を処理します。 Visual Studio のデバッグ インターフェイスを使用し、セッション デバッグ マネージャー (SDM) と通信します。

 SDM を介して送信されたイベントを中断して、デバッガーを実行モードから中断モードに切り替え、中断が発生したプログラムにフォーカスを変更します。 デバッグ パッケージは、イベントによって送信された情報からスタック フレームとスレッドを追跡します。

 デバッグ パッケージには、言語またはランタイム環境の依存関係はありません。 デバッグ パッケージを実装または変更する必要はありません。

 デバッグ パッケージは*vsdebug.dll*によって実装されます。

## <a name="see-also"></a>関連項目
- [セッション デバッグ マネージャー](../../extensibility/debugger/session-debug-manager.md)
- [スタック フレーム](../../extensibility/debugger/stack-frames.md)
- [スレッド](../../extensibility/debugger/threads.md)
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
