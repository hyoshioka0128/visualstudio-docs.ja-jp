---
title: '方法: パフォーマンス データの収集の開始と終了 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.wizard.summarypage
helpviewer_keywords:
- profiling tools, launching sessions
- performance sessions, launching
- performance sessions, ending
- profiling tools, ending sessions
ms.assetid: 9f6eb0d5-d9e9-4bec-b627-445065610bce
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 15c6d6c904bbab27bac541894ed6cd4f9e1f80f1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202681"
---
# <a name="how-to-start-and-end-performance-data-collection"></a>方法: パフォーマンス データの収集の開始と終了
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロファイリングを開始する前に、プロファイリング対象のバイナリをパフォーマンス セッションに追加する必要があります。 対象を追加するには、**パフォーマンス エクスプローラー**で **[ターゲット]** を右クリックし、 **[ターゲット バイナリの追加]** をクリックします。 **[ターゲット バイナリの追加]** ダイアログ ボックスで、ファイル名を選択して **[開く]** をクリックします。 新しいバイナリが追加されます。  
  
### <a name="to-start-profiling"></a>プロファイリングを開始するには  
  
1. **[パフォーマンス エクスプローラー]** ウィンドウでパフォーマンス セッションの名前を右クリックし、次のいずれかのオプションをクリックします。  
  
    - **[プロファイルを使用して起動]** - アプリケーションを開始し、プロファイリングを即座に開始します。  
  
    - **[プロファイルを一時停止して起動]** - アプリケーションを開始しますが、プロファイリングは開始しません。 プロファイリングを開始するには、 **[データ収集コントロール]** ウィンドウで **[収集の再開]** を選択します。 詳細については、「 [方法: パフォーマンスデータ収集の一時停止と再開](../profiling/how-to-pause-and-resume-performance-data-collection.md)」を参照してください。  
  
### <a name="to-end-profiling"></a>プロファイリングを終了するには  
  
- プロファイリング セッションを終了する最良の方法は、アプリケーションを終了することです。 プロファイリングをただちに終了するには、**パフォーマンス エクスプローラー**のツール バーで **[停止]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [データコレクションの制御](../profiling/controlling-data-collection.md)   
 [方法: パフォーマンスデータの収集を一時停止および再開する](../profiling/how-to-pause-and-resume-performance-data-collection.md)
