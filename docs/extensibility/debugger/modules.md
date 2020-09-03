---
title: モジュール |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738351"
---
# <a name="modules"></a>モジュール
デバッガーアーキテクチャに関して、 *モジュール*は次のようになります。

- は、実行可能ファイルや DLL など、コードの物理的なコンテナーです。

- シンボルを再度読み込み、それ自体を記述できます。 モジュールの説明は、IDE の [モジュール] ウィンドウに表示されます。

- は、モジュールを記述するためにデバッグエンジンによって作成される [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
