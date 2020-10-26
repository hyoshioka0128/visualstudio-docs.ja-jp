---
title: Port Supplier | を実装するMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], implementing port suppliers
- port suppliers, implementing
ms.assetid: 6b8579df-58df-4c7f-8112-6015993e8765
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ffa6daa20c08bd236657c88e762b2f453554cb74
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152682"
---
# <a name="implementing-a-port-supplier"></a>ポートのサプライヤーの実装
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ポートサプライヤーは、セッションデバッグマネージャー (SDM) への要求時にポートを提供します。 DCOM 以外のコンピューターにデバッグする場合、または新しいデバイスをサポートする必要がある場合は、ポートサプライヤーを実装する必要があります。 たとえば、携帯電話にデバッグを提供するには、携帯電話に接続するポート (通常は IR またはセル接続) を提供し、電話で実行されているプロセスとプログラムを列挙するポート供給者を実装します。  
  
 Windows ベースのコンピューターでのデバッグプログラム (リモートデバッグを含む) の場合、Visual Studio にはネイティブおよび共通言語ランタイム (CLR) のプロセス用のポートサプライヤーが用意されているので、独自のポート供給業者を実装する必要はありません。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ポート サプライヤーの実装および登録](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md)  
 SDM がポートサプライヤーとポートを操作する方法について説明します。  
  
 [必須のポート サプライヤー インターフェイス](../../extensibility/debugger/required-port-supplier-interfaces.md)  
 ポートサプライヤーを取得するために実装する必要があるインターフェイスについて説明します。  
  
## <a name="related-sections"></a>関連項目  
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)  
 デバッグアーキテクチャの主要概念について説明します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio デバッガーの拡張性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
