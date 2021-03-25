---
title: 従来の言語サービスでの非表示テキストサポートの提供
description: エディターで制御されるか、クライアントが制御する隠しテキスト領域を追加することによって、従来の言語サービスで非表示テキストのサポートを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hidden text, supporting
- editors [Visual Studio SDK], hidden text
- language services, implementing hidden text regions
ms.assetid: 1c1dce9f-bbe2-4fc3-a736-5f78a237f4cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2bb6d9c3c4f01c0e84c6ab437e352a86bf00448f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078735"
---
# <a name="how-to-provide-hidden-text-support-in-a-legacy-language-service"></a>方法: 従来の言語サービスで非表示テキストのサポートを提供する
アウトライン領域だけでなく、非表示のテキスト領域を作成することもできます。 非表示のテキスト領域は、クライアントコントロールまたはエディターで制御でき、テキスト領域を完全に非表示にするために使用されます。 エディターでは、非表示領域が水平線として表示されます。 この例として、HTML エディターの **スクリプトのみ** のビューがあります。

## <a name="to-implement-a-hidden-text-region"></a>非表示のテキスト領域を実装するには

1. `QueryService`を呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> ます。

     これにより、へのポインターが返さ <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> れます。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>を呼び出し、特定のテキストバッファーへのポインターを渡します。 これにより、バッファーに対して非表示のテキストセッションが既に存在するかどうかが判断されます。

3. 既に存在する場合は、作成する必要はなく、既存のオブジェクトへのポインター <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> が返されます。 このポインターを使用して、非表示のテキスト領域を列挙および作成します。 それ以外の場合は、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> を呼び出して、バッファーの非表示テキストセッションを作成します。

     オブジェクトへのポインター <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> が返されます。

    > [!NOTE]
    > を呼び出すと `CreateHiddenTextSession` 、非表示のテキストクライアント (つまり、) を指定でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient> ます。 非表示のテキストまたはアウトラインがユーザーによって展開または折りたたまれている場合は、非表示のテキストクライアントによって通知されます。

4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>を呼び出し、() パラメーターで次の情報を指定して、一度に1つまたは複数の新しいアウトライン領域を追加し `reHidReg` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> ます。

    1. `hrtConcealed` `iType` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> アウトライン領域ではなく、非表示領域を作成することを示すには、構造体のメンバーにの値を指定します。

        > [!NOTE]
        > 非表示の領域が非表示になっている場合は、表示されていない領域の周囲を示す線が自動的に表示されます。

    2. 構造体のメンバーで、領域がクライアントによって制御されるか、またはエディターで制御されるかを指定し `dwBehavior` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> ます。 スマートアウトラインの実装には、エディターとクライアントによって制御されるアウトラインと非表示のテキスト領域を混在させることができます。
