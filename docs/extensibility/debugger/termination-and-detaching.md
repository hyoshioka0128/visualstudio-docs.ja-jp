---
title: 終了とデタッチ |Microsoft Docs
description: 通常の終了とは、デバッグ対象のプログラムが、ブレークポイント、例外、実行時エラー、または無限ループなしで完了するまで実行されることを意味します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 74ef32708374dd3fea4c181e85b9f67a239198ba
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995968"
---
# <a name="termination-and-detaching"></a>終了とデタッチ
次のセクションでは、通常の終了について説明します。

## <a name="discussion"></a>ディスカッション
 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)または[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)インターフェイスが続行されると、デバッグ対象のアプリケーションにブレークポイント、例外、実行時エラー、または無限ループがない場合は、デバッグ中のプログラムが完了するまで実行されます。 このプロセスは通常の終了です。

 通常の終了を実装するには、 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) を送信する必要があります。 通常の終了では、 [IDebugProgramDestroyEvent2:: GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md) メソッドを実行する必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [カスタムデバッグエンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
