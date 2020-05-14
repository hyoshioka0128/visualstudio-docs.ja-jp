---
title: ドキュメントコンテキスト |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738922"
---
# <a name="document-context"></a>ドキュメントのコンテキスト
デバッグ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、*ドキュメントコンテキスト*:

- ソース ファイル内の位置を表します。 ソース ファイルが存在しない言語では、ドキュメント コンテキストは、通常、実行時環境によって生成されるドキュメント内の位置を識別します。 たとえば、スクリプト エンジンはスクリプトからドキュメントを生成する場合があります。 詳細については、「[ドキュメントの位置」を](../../extensibility/debugger/document-position.md)参照してください。

- コード コンテキストに対応するソース ドキュメント内の位置を記述します。 シンボル ハンドラーは、コンパイラまたはインタプリタによって生成された情報を使用して、コード コンテキストをドキュメント コンテキストにマップします。

- インターフェイスによって実装されます。 [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md)

## <a name="see-also"></a>関連項目
- [コード コンテキスト](../../extensibility/debugger/code-context.md)
- [シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)
- [シンボル プロバイダー インターフェイス](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)
