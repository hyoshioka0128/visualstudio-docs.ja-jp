---
title: '方法: 従来の言語サービスでアウトラインをサポートする |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], collapse to definitions command
- language services, supporting Collapse to Definitions command
- hidden text, Collapse to Definitions command
ms.assetid: bb6e74c3-93e4-4ef7-afc7-1c9b342f083b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 28396d513c83ed83e2769e75a6020a98b10251b4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707915"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>方法: 従来の言語サービスでのアウトラインのサポート
アウトラインは、テキストのさまざまな領域を展開したり折りたたんだりするために使用されます。 アウトラインの使用方法は、言語によって異なる方法で定義できます。 詳細については、「[アウトライン](../../ide/outlining.md)」を参照してください。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 アウトラインを実装する新しい方法の詳細については、「 [チュートリアル: アウトライン](../../extensibility/walkthrough-outlining.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

 次に、このコマンドを言語サービスに対してサポートする方法を示します。

## <a name="to-support-outlining"></a>アウトラインをサポートするには

1. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage>言語サービスオブジェクトにを実装します。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>新しいアウトライン領域を追加するには、現在のアウトラインセッションオブジェクトでを呼び出します。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 ユーザーが**アウトライン**メニューの [**定義を折りたたむ] を**選択すると、IDE は <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A> 言語サービスでを呼び出します。

 このメソッドが呼び出されると、IDE は <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> ポインター (テキストバッファーへのポインター) と <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> (現在のアウトラインセッションへのポインター) を渡します。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>パラメーターでこれらの領域を指定することで、複数のアウトライン領域に対してメソッドを呼び出すことができ `rgOutlnReg` ます。 `rgOutlnReg`パラメーターは <xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion> 構造体です。 このプロセスでは、特定の領域が展開されているか折りたたまれているかなど、非表示領域のさまざまな特性を指定できます。

> [!NOTE]
> 改行文字の非表示については注意してください。 非表示のテキストは、最初の行の先頭からセクションの最後の行の最後の文字まで拡張する必要があり、最後の改行文字は表示されたままになります。

## <a name="see-also"></a>関連項目
- [方法: 従来の言語サービスで非表示テキストのサポートを提供する](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [方法: 従来の言語サービスで拡張されたアウトラインサポートを提供する](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)
