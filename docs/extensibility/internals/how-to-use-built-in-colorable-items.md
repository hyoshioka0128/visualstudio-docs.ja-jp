---
title: '方法: 組み込みの装飾 Items | を使用するMicrosoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 762d1e53f7aafa11ed345859e68fc98766eec77d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85905215"
---
# <a name="how-to-use-built-in-colorable-items"></a>方法: 組み込みの装飾項目を使用する
組み込みの装飾項目を使用する前に、まず、独自のカスタム装飾項目 (この場合はオブジェクト) を提供しないことを統合開発環境 (IDE) に通知する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> ます。 これを行うには、言語サービスのレジストリエントリを設定します。

## <a name="to-use-built-in-colorable-items"></a>組み込みの装飾アイテムを使用するには

1. **HKEY_LOCAL_MACHINE \visualstudio \\<X.y> \languages\language Services \\<\> language Name**(はのバージョンで、は \<X.Y> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] \<Language Name> お使いの言語の名前です) で、 **requeststockcolors**という DWORD レジストリエントリの値を作成します。

2. **Requeststockcolors**レジストリエントリの値を*1*に設定します。

    レジストリエントリを作成した後は、その <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 列挙体のメンバーを使用して、 <xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS> エディターで使用する色属性の配列を入力できます。

   > [!NOTE]
   > カスタム装飾項目を指定する場合は、このレジストリエントリを設定しないでください。 詳細については、「 [Custom 装飾 items](../../extensibility/internals/custom-colorable-items.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [カスタムエディターでの構文の色分け](../../extensibility/syntax-coloring-in-custom-editors.md)
- [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [実装 (構文の色分けを)](../../extensibility/internals/implementing-syntax-coloring.md)
- [カスタム装飾項目](../../extensibility/internals/custom-colorable-items.md)
- [従来の言語サービスを登録する](../../extensibility/internals/registering-a-legacy-language-service2.md)
