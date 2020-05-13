---
title: '方法 : 組み込みのカラーブルアイテムを使用する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34e07894c3306f544396e53001990f7b9a2df5a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707788"
---
# <a name="how-to-use-built-in-colorable-items"></a>方法: 組み込みのカラー化可能なアイテムを使用する
組み込みのカラー対応アイテムを使用する前に、まず、独自のカスタムの色付け可能な項目 (この場合はオブジェクト) を提供していないことを統合開発環境 (IDE) に通知する<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>必要があります。 これを行うには、言語サービスのレジストリ エントリを設定します。

## <a name="to-use-built-in-colorable-items"></a>組み込みのカラー設定可能なアイテムを使用するには

1. **[X.Y\\>\言語サービス\\<言語名\>HKEY_LOCAL_MACHINE\VisualStudio<** で\<、X.Y>は言語の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]バージョン\<であり、言語名は言語名 **>、RequestStockColors**という名前の DWORD レジストリ エントリ値を作成します。

2. **レジストリ**エントリ値を*1*に設定します。

    レジストリ エントリを作成した後、カラー化者の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>メソッドは<xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS>、エディターで使用する色属性の配列を入力する列挙のメンバーを使用できます。

   > [!NOTE]
   > ユーザー設定の色付け可能な項目を提供する場合は、このレジストリ エントリを設定しないでください。 詳細については、「[カスタムのカラー設定可能な項目](../../extensibility/internals/custom-colorable-items.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [カスタム エディターでの構文の色分け](../../extensibility/syntax-coloring-in-custom-editors.md)
- [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [構文の色分けの実装](../../extensibility/internals/implementing-syntax-coloring.md)
- [カスタムのカラー設定可能なアイテム](../../extensibility/internals/custom-colorable-items.md)
- [従来の言語サービスを登録する](../../extensibility/internals/registering-a-legacy-language-service2.md)
