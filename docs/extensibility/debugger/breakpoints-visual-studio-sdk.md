---
title: ブレークポイント (Visual Studio SDK) |Microsoft Docs
description: ブレークポイントには、保留中、バインド、エラーの3種類があります。 この記事では、型を実装するために使用されるインターフェイスの一覧を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fa9f244ec60e336e9a7596ff839842211d516b7d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99930812"
---
# <a name="breakpoints-visual-studio-sdk"></a>ブレークポイント (Visual Studio SDK)
ブレークポイントには、保留中、バインド、エラーの3種類があります。

 **保留中のブレークポイント:**

- は、1つまたは複数のプログラムの1つ以上のコードコンテキストにブレークポイントをバインドするために必要なすべての情報を含む抽象化です。 デバッグ中のプログラムによってコードが読み込まれるたびに、デバッグエンジンはすべての保留中のブレークポイントをチェックし、バインドできるかどうかを確認します。

   保留中のブレークポイント自体はコードにバインドされるのではなく、によって収集され、生成されたすべてのバインドされたブレークポイントが含まれていると言います。

- は、 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスによって表されます。

  **バインドされたブレークポイント:**

- は、単一のコードコンテキストに関連付けられた、またはバインドされているブレークポイントの抽象化です。 各バインドされたブレークポイントは、保留中のブレークポイントに応答して生成されます。 ただし、保留中のブレークポイントは、複数のバインドされたブレークポイントを生成できます。

   コードがアンロードされると、バインドされたブレークポイントをバインド解除して破棄できます。

- は、 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) インターフェイスによって表されます。

  **エラーのブレークポイント:**

- は、保留中のブレークポイントをコードコンテキストにバインドしようとしたときに発生するエラーを記述するための抽象化です。 エラーブレークポイントは、位置またはブレークポイント式自体のエラーのいずれかを示します。 詳細については、「 [ブレークポイントのバインド](../../extensibility/debugger/binding-breakpoints.md)」を参照してください。

   ブレークポイントエラーには、エラーまたは警告のいずれかを指定できます。

- は、 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [コードコンテキスト](../../extensibility/debugger/code-context.md)
- [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
