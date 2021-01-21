---
title: 従来の言語サービスでのオートフォーマット |Microsoft Docs
description: 既知のコードコンストラクターの入力を開始すると、コードのスニペットが自動的に挿入される、従来の言語サービスでのオートフォーマットについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 651cecb20604069c6e8ccc5a5c7b983ab43d7384
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96190058"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>従来の言語サービスでのオートフォーマット
自動書式設定を使用すると、ユーザーが既知のコードコンストラクターの入力を開始したときに、言語サービスによってコードスニペットが自動的に挿入されます。

## <a name="automatic-formatting-behavior"></a>オートフォーマットの動作
 たとえば、 *if* と入力すると、言語サービスによって一致する中かっこが自動的に挿入されます。または、enter キーを押すと、新しい行の挿入ポイントは、前の行が新しいスコープを開いたかどうかによって、適切なインデントレベルに強制的に挿入されます。

 言語サービスの残りの部分に使用されるコマンドフィルターは、自動書式設定にも使用できます。 を呼び出して、対応する中かっこを強調表示することもでき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> ます。

## <a name="see-also"></a>関連項目
- [従来の言語サービスを開発する](../../extensibility/internals/developing-a-legacy-language-service.md)
