---
title: パッケージのデバッグ |Microsoft Docs
description: デバッグインターフェイスを使用してセッションデバッグマネージャーと通信することで、Visual Studio シェルでデバッグパッケージを実行し、UI を処理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0e5296a77e835ab291bce7a77e3f0cb09eb6bcf5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99840848"
---
# <a name="debug-package"></a>パッケージのデバッグ
デバッグパッケージは、Visual Studio シェルで実行され、すべての UI を処理します。 このメソッドは、Visual Studio のデバッグインターフェイスを使用し、セッションデバッグマネージャー (SDM) と通信します。

 SDM を介して送信されたイベントを中断するデバッガーを実行モードから中断モードに切り替え、中断が発生したプログラムにフォーカスを移動します。 デバッグパッケージは、イベントによって送信された情報から、スタックフレームとスレッドを追跡します。

 デバッグパッケージには、言語または実行時の環境依存関係はありません。 デバッグパッケージを実装または変更する必要はありません。

 デバッグパッケージは *vsdebug.dll* によって実装されます。

## <a name="see-also"></a>関連項目
- [セッションデバッグマネージャー](../../extensibility/debugger/session-debug-manager.md)
- [スタックフレーム](../../extensibility/debugger/stack-frames.md)
- [スレッド](../../extensibility/debugger/threads.md)
- [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)
