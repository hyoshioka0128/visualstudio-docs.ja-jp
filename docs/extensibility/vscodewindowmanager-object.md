---
title: VSCodeWindowManager オブジェクト |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindowManager
helpviewer_keywords:
- VsCodeWindowManager object
- views [Visual Studio SDK], VSCodeWindowManager object
ms.assetid: e313add5-afdb-4d8d-abd1-764e1fc10c44
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17bc9462af55ec9621654bd39cd65a2091f3f73f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80740419"
---
# <a name="vscodewindowmanager-object"></a>VSCodeWindowManager オブジェクト

言語サービスはコードウィンドウマネージャーを実装し、修飾 (ドロップダウンバーなど) の管理を担当します。 詳細については、「 [従来の API を使用してコードウィンドウをカスタマイズする](/visualstudio/extensibility/customizing-code-windows-by-using-the-legacy-api?view=vs-2015)」を参照してください。

次の表は、オブジェクト内のインターフェイスを示して `VSCodeWindowManager` います。

|インターフェイス|説明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|コードウィンドウに対する修飾 (ドロップダウンバーなど) の追加または削除を許可します。|
