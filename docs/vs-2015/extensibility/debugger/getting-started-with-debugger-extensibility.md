---
title: デバッガーの機能拡張によるはじめに |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d1c616c7cf8ed90ec3d76046892167b9b742a1b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152702"
---
# <a name="getting-started-with-debugger-extensibility"></a>デバッガーの機能拡張の開始
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

は、 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 環境内からプログラムをデバッグするために使用されるデバッガーコンポーネントを作成およびカスタマイズするために必要な情報を提供し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] デバッグには、以前のデバッガーで実行された広範なユーザビリティテストから得られた機能強化が加えられてい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]デバッグを使用すると、複数言語のアプリケーションをステップ実行できます。また、アプリケーションや多言語ソリューションをデバッグするときに、変数の編集時の編集を実装することもできます。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] デバッグはデバッグ中のプログラムを使用してプロセス外で実行されるため、アプリケーションのプロセス領域が少なくなります。 そのため、デバッグプログラムに影響を与えずに、デバッガーと対話するコンポーネントを簡単に記述できます。  
  
 を最適に使用するには、 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 次のことを理解している必要があります。  
  
- [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]統合開発環境 (IDE)  
  
- C++ プログラミング言語  
  
- ATL COM  
  
## <a name="in-this-section"></a>このセクションの内容  
 [デバッガーを拡張するためのロードマップ](../../extensibility/debugger/roadmap-for-extending-the-debugger.md)  
 コンパイラとその出力に応じて、製品にデバッグを実装するプロセスの概要を示します。  
  
 [デバッガーのコンポーネント](../../extensibility/debugger/debugger-components.md)  
 デバッグ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] エンジン (DE)、式エバリュエーター (EE)、およびシンボルハンドラー (SH) を含むデバッグコンポーネントの概要について説明します。  
  
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)  
 デバッグアーキテクチャの主要概念について説明します。  
  
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)  
 コード、ドキュメント、および式の評価コンテキスト内でデバッグエンジン (DE) を同時に動作させる方法について説明します。 3つのコンテキストのそれぞれについて、場所、位置、または評価に関連する評価について説明します。  
  
 [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)  
 プログラムの起動や式の評価など、さまざまなデバッグタスクへのリンクが含まれています。
