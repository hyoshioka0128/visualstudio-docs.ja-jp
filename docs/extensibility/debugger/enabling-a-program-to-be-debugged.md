---
title: プログラムのデバッグを有効にする |Microsoft Docs
description: デバッグエンジンを起動する方法や、デバッグエンジンを既存のプログラムにアタッチしてプログラムをデバッグする方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: ac9a43a0ec539dd978710c23c9b44f27eac81799
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915259"
---
# <a name="enable-a-program-to-be-debugged"></a>プログラムのデバッグを有効にする
デバッグエンジン (DE) がプログラムをデバッグできるようにするには、まず、DE を起動するか、既存のプログラムにアタッチする必要があります。

## <a name="in-this-section"></a>このセクションの内容
 [ポートを取得する](../../extensibility/debugger/getting-a-port.md) プログラムのデバッグを有効にするための最初の手順として、ポートを取得する方法について説明します。

 [プログラムを登録する](../../extensibility/debugger/registering-the-program.md) プログラムのデバッグを有効にするための次の手順について説明します。ポートに登録します。 登録されると、プログラムは、アタッチまたは just-in-time (JIT) デバッグのプロセスによってデバッグできます。

 [プログラムにアタッチする](../../extensibility/debugger/attaching-to-the-program.md) プログラムへのデバッガーのアタッチに関する次の手順について説明します。

 [起動ベースのアタッチ](../../extensibility/debugger/launch-based-attachment.md) プログラムへの起動ベースの添付ファイルについて説明します。これは、SDM によって起動されたときに自動的に実行されます。

 [必要なイベントを送信する](../../extensibility/debugger/sending-the-required-events.md) デバッグエンジン (DE) を作成し、プログラムにアタッチするときに必要なイベントをステップごとに説明します。

## <a name="related-sections"></a>関連項目
 [カスタムデバッグエンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md) デバッグエンジン (DE) を定義し、DE インターフェイスを使用して実装されるサービスと、デバッガーが異なる動作モード間を切り替える方法について説明します。
