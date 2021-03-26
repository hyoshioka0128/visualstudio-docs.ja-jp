---
title: ドキュメントの位置 |Microsoft Docs
description: Visual Studio のデバッグでドキュメントの位置を確認して、IDE で認識されているソースファイル内の位置を抽象化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: b59d739c-7572-427f-a70d-4e5df63d02c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5d14f9619059735aaecabf72adef248c69ed247e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097254"
---
# <a name="document-position"></a>ドキュメントの位置
デバッグでは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、 *ドキュメントの位置* は次のようになります。

- IDE で認識されているソースファイル内の位置の抽象化を提供します。 現在、ほとんどの言語では、ドキュメントの位置はソースファイル内の位置と考えることができます。

- ソースドキュメント内のデバッグエンジンへの位置を記述します。

- は、 [IDebugDocumentPosition2](../../extensibility/debugger/reference/idebugdocumentposition2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>こちらもご覧ください
- [コードコンテキスト](../../extensibility/debugger/code-context.md)
- [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)
- [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md)
- [シンボルプロバイダーインターフェイス](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)
