---
title: アンマネージ API リファレンス (Visual Studio での Office 開発)
description: アンマネージ API リファレンスは、読み込みマネージ VSTO アドインを支援するために使用されます。このインターフェイスを実装することで、独自の VSTO アドインローダーコンポーネントを作成することもできます。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/14/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, reference
- Office development in Visual Studio, unmanaged API reference
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cac9e2d01b47e0088543aeabcaeff30853314157
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908547"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>アンマネージ API リファレンス (Visual Studio での Office 開発)

2007 Microsoft Office システム以降では、Office アプリケーションは [IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md) インターフェイスを使用して、に含まれる VSTO アドインローダーコンポーネントを呼び出し [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 このコンポーネントは、読み込みマネージ VSTO アドインを支援するために使用されます。このインターフェイスを実装することで、独自の VSTO アドインローダーコンポーネントを作成できます。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>このセクションの内容

[IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)

Office アプリケーションでマネージド VSTO アドインの読み込みやアンロードを行うために実装できる COM インターフェイスです。
