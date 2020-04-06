---
title: ブレークポイント (ビジュアル スタジオ SDK) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7c9d61c82886f237e8c9f544a59d8fe167548277
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739196"
---
# <a name="breakpoints-visual-studio-sdk"></a>ブレークポイント (Visual Studio SDK)
ブレークポイントには、保留、バインド、エラーの 3 種類があります。

 **保留中のブレークポイント:**

- 1 つ以上のプログラムで、ブレークポイントを 1 つ以上のコード コンテキストにバインドするために必要なすべての情報を含む抽象化です。 デバッグ中のプログラムがコードを読み込むたびに、デバッグ エンジンは、保留中のすべてのブレークポイントをチェックして、それらがバインドできるかどうかを確認します。

   保留中のブレークポイント自体は、コードにバインドされることはありませんが、収集され、生成されるすべてのバインドされたブレークポイントが含まれると言われます。

- [インターフェイス](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)によって表されます。

  **バインドされたブレークポイント:**

- 単一のコード コンテキストに関連付けられた、またはバインドされたブレークポイントの抽象化です。 保留中のブレークポイントに対する応答として、バインドされた各ブレークポイントが生成されます。 ただし、保留中のブレークポイントでは、複数のバインドされたブレークポイントを生成できます。

   コードがアンロードされると、バインドされたブレークポイントをバインド解除して破棄できます。

- [インターフェイス](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)によって表されます。

  **エラー ブレークポイント:**

- 保留中のブレークポイントをコード コンテキストにバインドしようとするエラーを記述するための抽象化です。 エラー ブレークポイントは、場所またはブレークポイント式自体のエラーを記述します。 詳細については、「[ブレークポイントのバインド](../../extensibility/debugger/binding-breakpoints.md)」を参照してください。

   ブレークポイント エラーは、エラーまたは警告のいずれかです。

- [インターフェイス](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)によって表されます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [コード コンテキスト](../../extensibility/debugger/code-context.md)
- [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
