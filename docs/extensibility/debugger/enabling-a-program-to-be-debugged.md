---
title: プログラムのデバッグを有効にする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], enabling for programs
ms.assetid: 61d24820-0cd9-48b6-8674-6813f7493237
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17c6218cd0b25c0cf0134351fd5efd7490b6a1f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738892"
---
# <a name="enable-a-program-to-be-debugged"></a>プログラムのデバッグを有効にする
デバッグ エンジン (DE) がプログラムをデバッグする前に、まず DE を起動するか、既存のプログラムにアタッチする必要があります。

## <a name="in-this-section"></a>このセクションの内容
 [ポートを取得する](../../extensibility/debugger/getting-a-port.md)プログラムのデバッグを有効にする最初の手順としてポートを取得する方法について説明します。

 [プログラムの登録](../../extensibility/debugger/registering-the-program.md)プログラムをデバッグできるようにする次の手順について説明します。 登録後は、アタッチのプロセスまたはジャスト イン タイム (JIT) デバッグのプロセスによってプログラムをデバッグできます。

 [プログラムにアタッチする](../../extensibility/debugger/attaching-to-the-program.md)次の手順について説明します。

 [起動ベースのアタッチ](../../extensibility/debugger/launch-based-attachment.md)SDM によって起動されると自動的に実行されるプログラムへの起動ベースの添付ファイルについて説明します。

 [必要なイベントを送信する](../../extensibility/debugger/sending-the-required-events.md)デバッグ エンジン (DE) を作成し、プログラムにアタッチするときに必要なイベントを手順を説明します。

## <a name="related-sections"></a>関連項目
 [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)デバッグ エンジン (DE) を定義し、DE インターフェイスを通じて実装されるサービスと、デバッガーが異なる操作モード間で遷移する方法について説明します。
