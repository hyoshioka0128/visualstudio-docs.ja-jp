---
title: 従来の言語サービスでのオートフォーマット |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709979"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>従来の言語サービスでのオートフォーマット
自動書式設定を使用すると、ユーザーが既知のコードコンストラクターの入力を開始したときに、言語サービスによってコードスニペットが自動的に挿入されます。

## <a name="automatic-formatting-behavior"></a>オートフォーマットの動作
 たとえば、 *if*と入力すると、言語サービスによって一致する中かっこが自動的に挿入されます。または、enter キーを押すと、新しい行の挿入ポイントは、前の行が新しいスコープを開いたかどうかによって、適切なインデントレベルに強制的に挿入されます。

 言語サービスの残りの部分に使用されるコマンドフィルターは、自動書式設定にも使用できます。 を呼び出して、対応する中かっこを強調表示することもでき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> ます。

## <a name="see-also"></a>関連項目
- [従来の言語サービスを開発する](../../extensibility/internals/developing-a-legacy-language-service.md)
