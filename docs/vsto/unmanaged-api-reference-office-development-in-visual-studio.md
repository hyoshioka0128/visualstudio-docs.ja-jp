---
title: アンマネージ API リファレンス (Visual Studio での Office 開発)
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4c1616d24ae9b2c072df4e5708eb98e86611a83d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540986"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>アンマネージ API リファレンス (Visual Studio での Office 開発)

2007 Microsoft Office システム以降では、Office アプリケーションは[IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)インターフェイスを使用して、に含まれる VSTO アドインローダーコンポーネントを呼び出し [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 このコンポーネントは、読み込みマネージ VSTO アドインを支援するために使用されます。このインターフェイスを実装することで、独自の VSTO アドインローダーコンポーネントを作成できます。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>このセクションの内容

[IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)

Office アプリケーションでマネージド VSTO アドインの読み込みやアンロードを行うために実装できる COM インターフェイスです。
