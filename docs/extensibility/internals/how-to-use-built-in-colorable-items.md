---
title: '方法: Built-In 装飾 Items | を使用するMicrosoft Docs'
description: '言語サービス用の Visual Studio 統合開発環境 (IDE: integrated development environment) で組み込みの装飾項目を使用する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 253c108fe83eaf44f945f546bd64dd6529de1dd6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086080"
---
# <a name="how-to-use-built-in-colorable-items"></a>方法: 組み込みの装飾項目を使用する
組み込みの装飾項目を使用する前に、まず、独自のカスタム装飾項目 (この場合はオブジェクト) を提供しないことを統合開発環境 (IDE) に通知する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> ます。 これを行うには、言語サービスのレジストリエントリを設定します。

## <a name="to-use-built-in-colorable-items"></a>組み込みの装飾アイテムを使用するには

1. [ **HKEY_LOCAL_MACHINE\VisualStudio\\<[x.y]> [\languages\language Services \\<言語 \> 名**] (はのバージョンであり、は \<X.Y> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] \<Language Name> お使いの言語の名前) で、 **requeststockcolors** という DWORD レジストリエントリの値を作成します。

2. **Requeststockcolors** レジストリエントリの値を *1* に設定します。

    レジストリエントリを作成した後は、その <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 列挙体のメンバーを使用して、 <xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS> エディターで使用する色属性の配列を入力できます。

   > [!NOTE]
   > カスタム装飾項目を指定する場合は、このレジストリエントリを設定しないでください。 詳細については、「 [Custom 装飾 items](../../extensibility/internals/custom-colorable-items.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [カスタムエディターでの構文の色分け](../../extensibility/syntax-coloring-in-custom-editors.md)
- [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [実装 (構文の色分けを)](../../extensibility/internals/implementing-syntax-coloring.md)
- [カスタム装飾項目](../../extensibility/internals/custom-colorable-items.md)
- [従来の言語サービスを登録する](../../extensibility/internals/registering-a-legacy-language-service2.md)
