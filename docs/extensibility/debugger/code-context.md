---
title: コード コンテキスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6424c1182f30b1bbfe6c166209b94afb7ec45549
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739154"
---
# <a name="code-context"></a>コード コンテキスト
デバッグ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、**コード コンテキスト**:

- デバッグ エンジン (DE) に既知のコード内の位置の抽象化を提供します。 今日のほとんどの実行時アーキテクチャでは、コード コンテキストはプログラムの命令ストリームのアドレスと考えることができます。 コードが命令で表されない非伝統的な言語の場合、コード コンテキストは他の方法で表される場合があります。

- デバッグ中のプログラムの実行ストリーム内の現在の位置を記述します。

- プログラムがブレークポイントで停止した場合にのみ存在します。

- 関連付けられたドキュメント コンテキストがあります。

- インターフェイスによって実装されます。 [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md)

## <a name="see-also"></a>関連項目
- [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)
- [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)
