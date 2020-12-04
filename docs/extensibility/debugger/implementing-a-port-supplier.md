---
title: Port Supplier | を実装するMicrosoft Docs
description: ポートサプライヤーの実装について説明します。これは、DCOM 以外のコンピューターにデバッグする場合、または新しいデバイスでサポートが必要な場合に必要になります。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 72963660e4f50a72cdbc04bab4833b397d15fc27
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560669"
---
# <a name="implement-a-port-supplier"></a>ポートサプライヤーを実装する
ポートサプライヤーは、セッションデバッグマネージャー (SDM) への要求時にポートを提供します。 DCOM 以外のコンピューターにデバッグする場合、または新しいデバイスでサポートが必要な場合は、ポート供給元を実装する必要があります。 たとえば、携帯電話にデバッグを提供するには、携帯電話に接続するポート (通常は IR またはセル接続) に接続し、電話で実行されているプロセスとプログラムを列挙するポートサプライヤーを設定します。

 Windows ベースのコンピューターでのデバッグプログラム (リモートデバッグを含む) の場合、Visual Studio ではネイティブおよび共通言語ランタイム (CLR) のプロセス用にポートサプライヤーが提供されるため、独自のポート供給業者を設定する必要はありません。

## <a name="in-this-section"></a>このセクションの内容
 [ポートサプライヤーを実装して登録する](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md) SDM がポートサプライヤーとポートを操作する方法について説明します。

 [必要なポート供給業者インターフェイス](../../extensibility/debugger/required-port-supplier-interfaces.md) ポートサプライヤーを取得するために実装する必要があるインターフェイスについて説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md) 主要なデバッグ アーキテクチャの概念について説明します。

## <a name="see-also"></a>関連項目
 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
