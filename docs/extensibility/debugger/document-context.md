---
title: ドキュメントコンテキスト |Microsoft Docs
description: Visual Studio のデバッグでのドキュメントコンテキストについて説明します。これは、ソースファイル内の位置またはコードコンテキストのソースドキュメント内の位置を表します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: be2e5e168b232f120a22e7e4b39352008fee7418
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99840757"
---
# <a name="document-context"></a>ドキュメントのコンテキスト
デバッグでは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、 *ドキュメントコンテキスト* は次のようになります。

- ソースファイル内の位置を表します。 ソースファイルが存在しない可能性がある言語の場合、ドキュメントコンテキストは、通常、ランタイム環境によって生成されるドキュメント内の位置を識別します。 たとえば、スクリプトエンジンは、スクリプトからドキュメントを生成する場合があります。 詳細については、「 [ドキュメントの位置](../../extensibility/debugger/document-position.md)」を参照してください。

- コードコンテキストに対応するソースドキュメント内の位置を記述します。 シンボルハンドラーは、コンパイラまたはインタープリターによって生成された情報を使用して、コードコンテキストをドキュメントコンテキストにマップします。

- は、 [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>関連項目
- [コードコンテキスト](../../extensibility/debugger/code-context.md)
- [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md)
- [シンボルプロバイダーインターフェイス](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)
