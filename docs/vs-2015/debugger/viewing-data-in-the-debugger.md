---
title: デバッガーでのデータの表示 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], inspecting programs
- debugger, viewing data
ms.assetid: 13e1105f-f987-402e-9108-ec6ac12be042
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1ade6c38a8edd73c181a3f135dd5e967901bf63f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178922"
---
# <a name="viewing-data-in-the-debugger"></a>デバッガーでのデータ表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デバッガーには、プログラムの状態をチェックして変更できるように、さまざまなツールが用意されています。 ほとんどのツールは、中断モードだけで機能します。  
  
## <a name="datatips"></a>[DataTips] ポップアップ  
 DataTips は、デバッグ時、プログラムに含まれる変数とオブジェクトに関する情報を表示するときに、最も便利なツールの 1 つです。 デバッガーが中断モードの場合に、ソース ウィンドウ内の変数上にマウス ポインターを置くと、現在のスコープ内の変数値を表示できます。 詳細については、「[データ ヒントでのデータ値の表示](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)」を参照してください。  
  
## <a name="visualizers"></a>ビジュアライザー  
 ビジュアライザーは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デバッガーの新しいコンポーネントであり、オブジェクトや変数の内容をわかりやすく表示できるようにします。 たとえば、HTML ビジュアライザーを使用すると、HTML 文字列を解釈してブラウザーに表示した場合と同様に表示できます。 ビジュアライザーには、DataTips、 **[ウォッチ]** ウィンドウ、 **[自動変数]** ウィンドウ、 **[ローカル]** ウィンドウ、または **[クイック ウォッチ]** ダイアログ ボックスからアクセスできます。 詳細については、「 [カスタムビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [デバッガーの基本](../debugger/debugger-basics.md)   
 [コマンドウィンドウ](../ide/reference/command-window.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)
