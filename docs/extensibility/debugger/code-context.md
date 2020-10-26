---
title: コードコンテキスト |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739154"
---
# <a name="code-context"></a>コードコンテキスト
デバッグでは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、 **コードコンテキスト**は次のようになります。

- デバッグエンジン (DE) に知られているコード内の位置を抽象化します。 現在、ほとんどのランタイムアーキテクチャでは、コードコンテキストはプログラムの命令ストリームのアドレスと考えることができます。 コードが命令によって表されない nontraditional 言語の場合、コードコンテキストは他の方法で表すことができます。

- デバッグ中のプログラムの実行ストリーム内の現在の位置を記述します。

- プログラムがブレークポイントで停止した場合にのみ存在します。

- ドキュメントコンテキストが関連付けられています。

- は、 [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>関連項目
- [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)
- [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)
