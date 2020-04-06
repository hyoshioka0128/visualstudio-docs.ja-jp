---
title: '方法 : 従来の言語サービスでアウトラインをサポートする |マイクロソフトドキュメント'
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707915"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>方法: 従来の言語サービスでアウトラインをサポートする
アウトラインは、テキストの異なる領域を展開または折りたたむために使用されます。 アウトライン表示の使用方法は、言語によって異なる方法で定義できます。 詳細については、「[アウトライン](../../ide/outlining.md)」を参照してください。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 アウトラインを実装する新しい方法の詳細については、「[チュートリアル: アウトライン](../../extensibility/walkthrough-outlining.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

 以下は、言語サービスでこのコマンドをサポートする方法を示しています。

## <a name="to-support-outlining"></a>アウトラインをサポートするには

1. 言語<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage>サービス オブジェクトに実装します。

2. 現在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>のアウトライン セッション オブジェクトを呼び出して、新しいアウトライン領域を追加します。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 ユーザーが **[アウトライン**] メニューの<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A>**[定義に折りたたむ**] を選択すると、IDE によって言語サービスが呼び出されます。

 このメソッドが呼び出されると、IDE は<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>ポインター (テキスト バッファーへのポインター) と<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>a (現在のアウトライン セッションへのポインター) を渡します。

 パラメーターでこれらの領域<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>を指定することで、複数のアウトライン領域のメソッドを`rgOutlnReg`呼び出すことができます。 パラメータ`rgOutlnReg`は構造です<xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion>。 このプロセスでは、特定の領域が展開されているか折りたたまれているかなど、非表示領域のさまざまな特性を指定できます。

> [!NOTE]
> 改行文字を非表示にする場合は注意してください。 隠し文字は、最初の行の先頭からセクションの最後の行の最後の文字まで拡張し、最後の改行文字は表示したままにします。

## <a name="see-also"></a>関連項目
- [方法: 従来の言語サービスで隠しテキストのサポートを提供する](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [方法: 従来の言語サービスで拡張アウトライン サポートを提供する](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)
