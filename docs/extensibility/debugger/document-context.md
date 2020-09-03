---
title: ドキュメントコンテキスト |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 48fe651e69e5e2c97756788cc30e54454c26e51e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738922"
---
# <a name="document-context"></a>ドキュメントのコンテキスト
デバッグでは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、 *ドキュメントコンテキスト*は次のようになります。

- ソースファイル内の位置を表します。 ソースファイルが存在しない可能性がある言語の場合、ドキュメントコンテキストは、通常、ランタイム環境によって生成されるドキュメント内の位置を識別します。 たとえば、スクリプトエンジンは、スクリプトからドキュメントを生成する場合があります。 詳細については、「 [ドキュメントの位置](../../extensibility/debugger/document-position.md)」を参照してください。

- コードコンテキストに対応するソースドキュメント内の位置を記述します。 シンボルハンドラーは、コンパイラまたはインタープリターによって生成された情報を使用して、コードコンテキストをドキュメントコンテキストにマップします。

- は、 [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>関連項目
- [コードコンテキスト](../../extensibility/debugger/code-context.md)
- [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md)
- [シンボルプロバイダーインターフェイス](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)
