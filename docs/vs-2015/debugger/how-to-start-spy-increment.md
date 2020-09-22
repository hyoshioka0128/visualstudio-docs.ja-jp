---
title: '方法: Spy++ の起動 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Spy++, starting
ms.assetid: 1d36813a-dc2a-4fda-9b3d-a38928a62ced
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 36555d9b00c9aff3f594ae2217afe8434bb41542
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842068"
---
# <a name="how-to-start-spy"></a>方法: Spy++ の起動
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Spy++ は、Visual Studio またはコマンド プロンプトから起動できます。  
  
 Spy + + を起動するときに、コンピューターに変更を加えるためのアクセス許可を求めるメッセージが表示されたら、[ **はい**] をクリックします。  
  
> [!NOTE]
> Spy++ のインスタンスは 1 つだけ実行できます。 別のインスタンスを実行しようとすると、現在実行中のインスタンスがフォーカスを取得するだけです。  
  
### <a name="to-start-spy-from-visual-studio"></a>Visual Studio から Spy + + を起動するには  
  
- [ **ツール** ] メニューの [ **Spy + +**] をクリックします。  
  
     Spy + + は独立して実行されるため、開始した後、Visual Studio を閉じることができます。  
  
    > [!NOTE]
    > Spy++ でメッセージをログに記録すると、オペレーティング システムのパフォーマンスが低下する可能性があります。  
  
### <a name="to-start-spy-at-a-command-prompt"></a>コマンドプロンプトで Spy + + を起動するには  
  
1. コマンド プロンプト ウィンドウで、ディレクトリを spyxx.exe が含まれるフォルダーに変更します。 通常、このフォルダーのパスは. です \\ 。*Visual Studio のインストールフォルダー*\Common7\Tools \\ 。  
  
2. 「 **spyxx.exe** 」と入力し、enter キーを押します。  
  
## <a name="see-also"></a>参照  
 [Spy + + の使用](../debugger/using-spy-increment.md)   
 [Spy + + ビュー](../debugger/spy-increment-views.md)   
 [Spy++ リファレンス](../debugger/spy-increment-reference.md)
