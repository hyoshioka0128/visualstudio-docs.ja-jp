---
title: 従来の言語サービス コマンドをインターセプトする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5206bced8b4bfae32498434765e5c3f61801b386
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707452"
---
# <a name="intercepting-legacy-language-service-commands"></a>従来の言語サービスのコマンドの受信
では[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、テキスト ビューがそれ以外で処理する言語サービスのコマンドをインターセプトできます。 これは、テキスト ビューで管理されない言語固有の動作に役立ちます。 言語サービスからテキスト ビューに 1 つ以上のコマンド フィルターを追加することで、これらのコマンドをインターセプトできます。

## <a name="getting-and-routing-the-command"></a>コマンドの取得とルーティング
 コマンド・フィルターは、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>特定の文字シーケンスまたはキー・コマンドをモニターするオブジェクトです。 複数のコマンド フィルタを 1 つのテキスト ビューに関連付けることができます。 各テキスト ビューには、コマンド フィルタのチェーンが保持されます。 新しいコマンド フィルタを作成したら、該当するテキスト ビューのチェーンにフィルタを追加します。

 のメソッド<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>を呼び出して、コマンド フィルターをチェーンに追加します。 を呼び<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>出[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]すと、コマンド フィルタで処理できないコマンドを渡すことができる別のコマンド フィルタが返されます。

 コマンド処理には、次のオプションがあります。

- コマンドを処理し、チェーン内の次のコマンド フィルターにコマンドを渡します。

- コマンドを処理し、次のコマンド フィルターにコマンドを渡しません。

- コマンドを処理せず、次のコマンド フィルターにコマンドを渡します。

- コマンドを無視します。 現在のフィルタで処理せず、次のフィルタに渡しません。

  言語サービスで処理する必要があるコマンドについては、「言語サービス[フィルタの重要なコマンド](../../extensibility/internals/important-commands-for-language-service-filters.md)」を参照してください。
