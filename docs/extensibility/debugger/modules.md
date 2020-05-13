---
title: モジュール |マイクロソフトドキュメント
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
ms.openlocfilehash: abdf76c7f5f031d2ef7f3bcac2bae8a2c508b783
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738351"
---
# <a name="modules"></a>モジュール
デバッガアーキテクチャの観点から、*モジュール*:

- 実行可能ファイルや DLL などのコードの物理的なコンテナーです。

- シンボルを再読み込みし、それ自体を記述できます。 モジュールの説明は、IDE の「モジュール」ウィンドウに表示されます。

- モジュールを記述するデバッグ エンジンによって作成された[IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
