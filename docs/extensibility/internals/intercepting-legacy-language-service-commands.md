---
title: レガシ言語サービスコマンドのインターセプト |Microsoft Docs
description: Visual Studio でコマンドフィルターを使用して、従来の言語サービスコマンドをインターセプトし、言語固有の動作を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8d7af9ff4a8f04382cff4999b8c57549f3da3db7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074679"
---
# <a name="intercepting-legacy-language-service-commands"></a>従来の言語サービスのコマンドの受信
では [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、テキストビューで処理されるような言語サービスをインターセプトすることができます。 これは、テキストビューでは管理されない言語固有の動作に便利です。 これらのコマンドを受け取るには、言語サービスからテキストビューに1つ以上のコマンドフィルターを追加します。

## <a name="getting-and-routing-the-command"></a>コマンドの取得とルーティング
 コマンドフィルターは、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 特定の文字シーケンスまたはキーコマンドを監視するオブジェクトです。 複数のコマンドフィルターを1つのテキストビューに関連付けることができます。 各テキストビューでは、コマンドフィルターのチェーンが保持されます。 新しいコマンドフィルターを作成したら、適切なテキストビューのチェーンにフィルターを追加します。

 でメソッドを呼び出して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> コマンドフィルターをチェーンに追加します。 を呼び出すと <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コマンドフィルターで処理されないコマンドを渡すことができる別のコマンドフィルターが返されます。

 コマンド処理には、次のオプションがあります。

- コマンドを処理し、チェーン内の次のコマンドフィルターにコマンドを渡します。

- コマンドを処理し、次のコマンドフィルターにコマンドを渡しません。

- コマンドを処理するのではなく、コマンドを次のコマンドフィルターに渡します。

- コマンドを無視します。 現在のフィルターでは処理せず、次のフィルターに渡すことはできません。

  言語サービスで処理する必要があるコマンドの詳細については、「 [言語サービスフィルターの重要なコマンド](../../extensibility/internals/important-commands-for-language-service-filters.md)」を参照してください。
