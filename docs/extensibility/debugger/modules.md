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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 57202231c1bbfc7712d322b8cc7a30e3f64c87af
ms.sourcegitcommit: 42981ace63c0f2b087de5703ca76b8dcdd93a719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2020
ms.locfileid: "96606646"
---
# <a name="modules"></a>モジュール
デバッガーアーキテクチャに関して、 *モジュール* は次のようになります。

- は、実行可能ファイルや DLL など、コードの物理的なコンテナーです。

- シンボルを再度読み込み、それ自体を記述できます。 モジュールの説明は、IDE の [モジュール] ウィンドウに表示されます。

- は、モジュールを記述するためにデバッグエンジンによって作成される [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
