---
title: エディター内のレガシインターフェイス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy
ms.assetid: 741d45f5-0ea3-4614-972a-8728fe054e07
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8483068ae03c9a57fc67b528393e5d6830c3ec33
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180288"
---
# <a name="legacy-interfaces-in-the-editor"></a>エディターのレガシ インターフェイス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

レガシインターフェイスから Visual Studio エディターにアクセスできます。 Visual Studio SDK には *shim*と呼ばれるアダプターが含まれています。これにより、これらのインターフェイスが新しいエディターと対話できるようになります。 ただし、新しいエディター API を使用するように、レガシコードを更新することをお勧めします。 コードのパフォーマンスが向上し、Windows Presentation Foundation (WPF) や Managed Extensibility Framework (MEF) などの新しいテクノロジを使用できるようになります。  
  
## <a name="related-topics"></a>関連トピック  
  
|Title|説明|  
|-----------|-----------------|  
|[レガシ コードをエディターに適合させる](../extensibility/adapting-legacy-code-to-the-editor.md)|新しいエディターにコードを適合させる方法について説明します。|  
|[エディター アダプターの新規または変更された動作](../extensibility/new-or-changed-behavior-with-editor-adapters.md)|エディターアダプターの動作が、以前のバージョンのエディターとどのように異なるかについて説明します。|  
|[コア エディターの内部](../extensibility/inside-the-core-editor.md)|以前のバージョンのエディターのさまざまなコンポーネントについて説明します。|  
|[レガシ API を使用するコア エディターのインスタンス化](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)|レガシ API を使用してコアエディターをインスタンス化する方法について説明します。|  
|[エディター ファクトリ](../extensibility/editor-factories.md)|従来の API でエディターファクトリを使用する方法について説明します。|  
|[方法: エディター ファイルの種類を登録する](../extensibility/how-to-register-editor-file-types.md)|ファイル名拡張子をエディターにリンクする方法について説明します。|  
|[チュートリアル: コア エディターの作成とエディター ファイルの種類の登録](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)|コアエディターを作成し、ファイル名拡張子をリンクする方法について説明します。|  
|[方法: エディター用のコンテキストを提供する](../extensibility/how-to-provide-context-for-editors.md)|エディターのコンテキストを指定する方法について説明します。|  
|[言語サービスとコア エディター](../extensibility/language-services-and-the-core-editor.md)|言語サービスとエディターの相互作用について説明します。|  
|[レガシ API を使用するテキスト バッファーへのアクセス](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)|レガシ API を使用してテキストバッファーにアクセスする方法について説明します。|  
|[レガシ API を使用するテキスト ビューへのアクセス](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)|レガシ API を使用してテキストビューにアクセスする方法について説明します。|  
|[レガシ API を使用するコード ウィンドウのカスタマイズ](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)|レガシ API を使用してコードウィンドウをカスタマイズする方法について説明します。|  
|[レガシ API を使用するテキスト レイヤーへのアクセス](../extensibility/accessing-text-layers-by-using-the-legacy-api.md)|レガシ API を使用して、さまざまなテキストレイヤーにアクセスする方法について説明します。|  
|[レガシ API でのテキスト マーカーの使用](../extensibility/using-text-markers-with-the-legacy-api.md)|レガシ API を使用してテキストマーカーを追加する方法について説明します。|  
|[レガシ API を使用するエディター コントロールおよびメニューのカスタマイズ](../extensibility/customizing-editor-controls-and-menus-by-using-the-legacy-api.md)|レガシ API を使用してエディターコントロールをカスタマイズする方法について説明します。|  
|[レガシ API を使用した元に戻すとやり直しの管理](../extensibility/managing-undo-and-redo-by-using-the-legacy-api.md)|従来の API を使用して、元に戻すとやり直しを管理する方法について説明します。|  
|[方法: 検索と置換のメカニズムを実装する](../extensibility/how-to-implement-the-find-and-replace-mechanism.md)|レガシ API を使用して検索と置換を管理する方法について説明します。|  
|[方法: ファイル変更通知を抑制する](../extensibility/how-to-suppress-file-change-notifications.md)|レガシ API を使用してファイル変更通知を抑制する方法について説明します。|  
|[カスタム エディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md)|カスタムエディターとデザイナーを作成する方法について説明します。|  
|[従来の言語サービスの開発](../extensibility/internals/developing-a-legacy-language-service.md)|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]言語サービスのサポートを追加することによって、コアエディターにカスタマイズ機能を提供する機能に関するドキュメントへのリンクを示します。|  
|[フォントと色の使用](../extensibility/using-fonts-and-colors.md)|レガシインターフェイスでフォントおよび色を使用する方法について説明します。|
