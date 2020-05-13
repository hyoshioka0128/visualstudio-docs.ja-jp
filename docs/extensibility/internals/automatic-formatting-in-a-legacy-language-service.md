---
title: レガシ言語サービスでの自動フォーマット |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, automatic formatting
ms.assetid: c210fc94-77bd-4694-b312-045087d8a549
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a11e9c1fdef60e71f46cee9986d925e876dcac35
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709979"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>従来の言語サービスでの自動書式設定
自動書式設定を使用すると、ユーザーが既知のコード コンストラクトを入力し始めると、言語サービスによってコードのスニペットが自動的に挿入されます。

## <a name="automatic-formatting-behavior"></a>自動書式設定の動作
 たとえば、*に*言語サービスが自動的に一致する中かっこを挿入する場合、または Enter キーを押すと、前の行が新しいスコープを開くかどうかに応じて、言語サービスによって新しい行の挿入ポイントが適切なインデント レベルに設定されます。

 言語サービスの残りの部分で使用されるコマンド フィルタは、自動書式設定にも使用できます。 また、 を呼び出<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A>して、一致する中かっこを強調表示することもできます。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
