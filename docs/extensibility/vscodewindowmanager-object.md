---
title: VSCodeWindowManager オブジェクト |Microsoft Docs
description: VSCodeWindowManager オブジェクトについて説明します。このオブジェクトは、表示要素の管理を担当します。たとえば、ドロップダウンバーなどです。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e353070c780f69ea05c1c67986f7a40f34d0659c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925839"
---
# <a name="vscodewindowmanager-object"></a>VSCodeWindowManager オブジェクト

言語サービスはコードウィンドウマネージャーを実装し、修飾 (ドロップダウンバーなど) の管理を担当します。 詳細については、「 [従来の API を使用してコードウィンドウをカスタマイズする](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015)」を参照してください。

次の表は、オブジェクト内のインターフェイスを示して `VSCodeWindowManager` います。

|インターフェイス|説明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|コードウィンドウに対する修飾 (ドロップダウンバーなど) の追加または削除を許可します。|