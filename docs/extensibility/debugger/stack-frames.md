---
title: スタック フレーム |マイクロソフトドキュメント
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
ms.openlocfilehash: 1ea79ad199e20afeb5d2bf1ca6a3cf881c6d51c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712843"
---
# <a name="stack-frames"></a>スタック フレーム
デバッガアーキテクチャでは、*スタックフレーム*:

- スレッドの実行コンテキストを提供するスタックの抽象化です。 スレッドは常に関数内で実行されます。 スタック フレームは、関数のローカル変数とそれに対する引数を保持します。 Visual Studio でデバッグするには、デバッグ中の言語または環境がスタック フレームをサポートしている必要があります。

- 自身を識別して記述でき、関連付けられたスレッドを返すことができます。 スタック フレームは、現在の命令ポインターと関連付けられているドキュメントと式の評価コンテキストを表すコード コンテキストを返すこともできます。

- ローカル変数と引数の名前、型、および値を記述し、さまざまな IDE デバッグ ウィンドウに表示されるプロパティがあります。

- 通常は、スレッドの実行の結果としてデバッグ エンジン (DE) または仮想マシンによって作成される[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)
