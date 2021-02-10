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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 685650e0e97c3f9851f051fdaa78f86252597ff8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99930721"
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
