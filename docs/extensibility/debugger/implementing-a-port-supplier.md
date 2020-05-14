---
title: ポートサプライヤーの実装 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], implementing port suppliers
- port suppliers, implementing
ms.assetid: 6b8579df-58df-4c7f-8112-6015993e8765
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8218e372ad3aece922811bc20cfd7650f33296f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738554"
---
# <a name="implement-a-port-supplier"></a>ポート サプライヤーの実装
ポート サプライヤーは、要求に応じて、セッション デバッグ マネージャー (SDM) にポートを提供します。 ポート サプライヤーは、DCOM 以外のコンピューターにデバッグするとき、または新しいデバイスがサポートを必要とする場合に実装する必要があります。 たとえば、携帯電話にデバッグを提供するために、ポートを提供するポート サプライヤーを設定し、ポートを提供し、携帯電話に接続する (たとえば、IR またはセル接続を使用して) し、電話で実行されているプロセスとプログラムを列挙します。

 Windows ベースのコンピューターでプログラムをデバッグする場合 (リモート デバッグを含む)、Visual Studio はネイティブおよび共通言語ランタイム (CLR) プロセス用のポート サプライヤーを提供するため、そのような場合に独自のポート サプライヤーを設定する必要はありません。

## <a name="in-this-section"></a>このセクションの内容
 [ポート サプライヤーの実装と登録](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md)SDM がポート サプライヤとそのポートとどのように相互作用するかを説明します。

 [必要なポート サプライヤー インターフェイス](../../extensibility/debugger/required-port-supplier-interfaces.md)ポートサプライヤーを取得するために実装する必要があるインターフェイスについて説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)デバッグアーキテクチャの主要な概念について説明します。

## <a name="see-also"></a>関連項目
 [デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
