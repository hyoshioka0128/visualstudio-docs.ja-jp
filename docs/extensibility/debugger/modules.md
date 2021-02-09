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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9aa0aaf7e82287c1dc2e35c524798a3480d2573e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99926330"
---
# <a name="modules"></a>モジュール
デバッガーアーキテクチャに関して、 *モジュール* は次のようになります。

- は、実行可能ファイルや DLL など、コードの物理的なコンテナーです。

- シンボルを再度読み込み、それ自体を記述できます。 モジュールの説明は、IDE の [モジュール] ウィンドウに表示されます。

- は、モジュールを記述するためにデバッグエンジンによって作成される [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
