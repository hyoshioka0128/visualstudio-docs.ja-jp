---
title: ドキュメントの位置 |Microsoft Docs
description: Visual Studio のデバッグでドキュメントの位置を確認して、IDE で認識されているソースファイル内の位置を抽象化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: b59d739c-7572-427f-a70d-4e5df63d02c1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fef3debcbce3a178c4321114d69c87c627611a07
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915324"
---
# <a name="document-position"></a>ドキュメントの位置
デバッグでは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、 *ドキュメントの位置* は次のようになります。

- IDE で認識されているソースファイル内の位置の抽象化を提供します。 現在、ほとんどの言語では、ドキュメントの位置はソースファイル内の位置と考えることができます。

- ソースドキュメント内のデバッグエンジンへの位置を記述します。

- は、 [IDebugDocumentPosition2](../../extensibility/debugger/reference/idebugdocumentposition2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>関連項目
- [コードコンテキスト](../../extensibility/debugger/code-context.md)
- [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)
- [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md)
- [シンボルプロバイダーインターフェイス](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)
