---
title: コードコンテキスト |Microsoft Docs
description: Visual Studio のデバッグでのコードコンテキストについて説明します。これは、プログラムがブレークポイントで停止したときに存在するコード内の位置を記述します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 60eabaca8d39d40649e20e022b25ce1b02bd8faf
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914310"
---
# <a name="code-context"></a>コードコンテキスト
デバッグでは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、 **コードコンテキスト** は次のようになります。

- デバッグエンジン (DE) に知られているコード内の位置を抽象化します。 現在、ほとんどのランタイムアーキテクチャでは、コードコンテキストはプログラムの命令ストリームのアドレスと考えることができます。 コードが命令によって表されない nontraditional 言語の場合、コードコンテキストは他の方法で表すことができます。

- デバッグ中のプログラムの実行ストリーム内の現在の位置を記述します。

- プログラムがブレークポイントで停止した場合にのみ存在します。

- ドキュメントコンテキストが関連付けられています。

- は、 [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>関連項目
- [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)
- [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)
