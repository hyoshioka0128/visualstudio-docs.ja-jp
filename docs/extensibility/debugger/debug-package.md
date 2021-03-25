---
title: パッケージのデバッグ |Microsoft Docs
description: デバッグインターフェイスを使用してセッションデバッグマネージャーと通信することで、Visual Studio シェルでデバッグパッケージを実行し、UI を処理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 90c4c82895f7a30d4df9126a280c6c9ffa7ffa76
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067908"
---
# <a name="debug-package"></a>パッケージのデバッグ
デバッグパッケージは、Visual Studio シェルで実行され、すべての UI を処理します。 このメソッドは、Visual Studio のデバッグインターフェイスを使用し、セッションデバッグマネージャー (SDM) と通信します。

 SDM を介して送信されたイベントを中断するデバッガーを実行モードから中断モードに切り替え、中断が発生したプログラムにフォーカスを移動します。 デバッグパッケージは、イベントによって送信された情報から、スタックフレームとスレッドを追跡します。

 デバッグパッケージには、言語または実行時の環境依存関係はありません。 デバッグパッケージを実装または変更する必要はありません。

 デバッグパッケージは *vsdebug.dll* によって実装されます。

## <a name="see-also"></a>こちらもご覧ください
- [セッションデバッグマネージャー](../../extensibility/debugger/session-debug-manager.md)
- [スタックフレーム](../../extensibility/debugger/stack-frames.md)
- [スレッド](../../extensibility/debugger/threads.md)
- [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)
