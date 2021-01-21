---
title: スタックフレーム |Microsoft Docs
description: この記事では、Visual Studio のデバッガーアーキテクチャでのスタックフレームの定義とロールについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- stack frames, debugging
- debugging [Debugging SDK], stack frames
- stack frames
ms.assetid: b5e439d4-1e9d-4e13-9cad-bb8b136d4ca8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab2c891002ad90d767a4c5ca9efffd3f3d1d10ee
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845207"
---
# <a name="stack-frames"></a>スタックフレーム
デバッガーのアーキテクチャでは、 *スタックフレーム* は次のようになります。

- は、スレッドの実行コンテキストを提供するスタックの抽象化です。 スレッドは、常に関数内で実行されます。 スタックフレームには、関数のローカル変数とそれに対する引数が保持されます。 Visual Studio でデバッグするには、デバッグ対象の言語または環境でスタックフレームがサポートされている必要があります。

- は、自身を識別して記述することができ、関連付けられているスレッドを返すことができます。 スタックフレームは、現在の命令ポインターを表すコードコンテキストと、関連付けられているドキュメントおよび式の評価コンテキストを返すこともできます。

- には、ローカル変数と引数の名前、型、および値を記述するプロパティがあり、さまざまな IDE デバッグウィンドウに表示されます。

- は、スレッドを実行した結果としてデバッグエンジン (DE) または仮想マシンによって作成される [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [デバッグエンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)
