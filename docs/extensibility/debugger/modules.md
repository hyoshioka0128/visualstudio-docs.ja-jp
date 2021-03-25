---
title: モジュール |Microsoft Docs
description: この記事では、Visual Studio のデバッガーアーキテクチャにおけるモジュールの定義とロールについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- modules
- debugging [Debugging SDK], modules
ms.assetid: c4cf2809-dbdb-4e75-9273-b3d3d77b67d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f40cb7d0c65822fcb6ba4d4ca0132147f62d9286
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054765"
---
# <a name="modules"></a>モジュール
デバッガーアーキテクチャに関して、 *モジュール* は次のようになります。

- は、実行可能ファイルや DLL など、コードの物理的なコンテナーです。

- シンボルを再度読み込み、それ自体を記述できます。 モジュールの説明は、IDE の [モジュール] ウィンドウに表示されます。

- は、モジュールを記述するためにデバッグエンジンによって作成される [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) インターフェイスによって表されます。

## <a name="see-also"></a>こちらもご覧ください
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
