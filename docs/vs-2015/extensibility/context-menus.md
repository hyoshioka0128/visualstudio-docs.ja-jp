---
title: コンテキストメニュー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - context menus
ms.assetid: 44fd9e6a-6d42-4aba-80ba-f37fa0070f1d
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9baab8ef64fa1952eff138165f608e25960c8cfd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184269"
---
# <a name="context-menus"></a>コンテキスト メニュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コンテキストメニューは、ユーザーがクライアント領域のアクティブな領域を右クリックし、マウスの右ボタンが離されたときに表示されます。  
  
## <a name="editor-context-menus"></a>エディター コンテキスト メニュー  
 言語サービスでは、インターセプトによって、 `ECMD_SHOWCONTEXTMENU` エディターに表示されるコンテキストメニューを制御できます。 独自のコンテキストメニューを表示するには、を呼び出して、に渡されたときにこのコマンドを処理し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> ます。 このコマンドを処理しない場合は、エディター用に用意されている標準のコンテキストメニューが IDE に表示されます。 また、マーカーごとにコンテキストメニューの内容を制御することもできます。 詳細については、「 [従来の API でのテキストマーカーの使用](../extensibility/using-text-markers-with-the-legacy-api.md) 」および「 [従来の言語サービスコマンドのインターセプト](../extensibility/internals/intercepting-legacy-language-service-commands.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [従来の言語サービスの開発](../extensibility/internals/developing-a-legacy-language-service.md)   
 [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
