---
title: アンマネージ API リファレンス (Visual Studio での Office 開発)
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 79f48e7771b3e62c0c58fbc59bd9f9b534069d71
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584426"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>アンマネージ API リファレンス (Visual Studio での Office 開発)

2007 Microsoft Office システム以降では、Office アプリケーションは [IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md) インターフェイスを使用して、に含まれる VSTO アドインローダーコンポーネントを呼び出し [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 このコンポーネントは、読み込みマネージ VSTO アドインを支援するために使用されます。このインターフェイスを実装することで、独自の VSTO アドインローダーコンポーネントを作成できます。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>このセクションの内容

[IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)

Office アプリケーションでマネージド VSTO アドインの読み込みやアンロードを行うために実装できる COM インターフェイスです。
