---
title: '方法: ASP.NET の例外をデバッグする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], ASP.NET exceptions
- ASP.NET, exceptions
- exceptions, ASP.NET
ms.assetid: 1810096e-de8c-435e-be3d-f365d0cd0a6a
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1ccd8c399bd92bd98307d44aff913c30390033c7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205424"
---
# <a name="how-to-debug-aspnet-exceptions"></a>方法: ASP.NET の例外をデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

例外のデバッグは、堅牢な [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションの開発において重要な部分です。 例外をデバッグする方法に関する一般的な情報については、「[デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)」を参照してください。  
  
 ハンドルされない [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 例外をデバッグする場合、その例外でデバッガーが停止していることを確認する必要があります。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ランタイムにはトップレベルの例外ハンドラーがあります。 そのため、デバッガーは既定では、ハンドルされない例外で実行を中断することはありません。 例外がスローされたときにデバッガーを中断するには、特定の例外に対して **[例外が次の場合に中断する: スローされたとき]** ( **[例外]** ダイアログ ボックス内) を選択する必要があります。  
  
 [マイ コードのみ] を有効にしていると、**[例外が次の場合に中断する: スローされるとき]** を選択しても、.NET Framework メソッドや他のシステム コード内で例外がスローされた場合に、デバッガーはすぐには中断されません。 デバッガーがシステム コード以外のコードをヒットするまで実行は継続され、ヒットした時点でデバッガーは中断されます。 つまり、例外が発生したときにシステム コードをステップ実行する必要はありません。  
  
 [マイ コードのみ] には、さらに便利な別のオプションがあります: **[例外が次の場合に中断する: ユーザーによって処理されない]** 。 例外にこの設定を選択すると、ユーザー コードで例外が取得され、処理された場合にのみ、デバッガーによってユーザー コードの実行が中断されます。 この設定では、トップレベルの [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 例外ハンドラーの効果が無視されます。この例外ハンドラーがユーザー コードではないためです。  
  
### <a name="to-enable-debugging-of-aspnet-exceptions-with-just-my-code"></a>[マイ コードのみ] で ASP.NET 例外を有効にするには  
  
1. **[デバッグ]** メニューの **[例外]** をクリックします。  
  
     **[例外]** ダイアログ ボックスが表示されます。  
  
2. **[Common Language Runtime Exceptions]** 行の **[スローされるとき]** または **[ユーザーにハンドルされていないとき]** チェック ボックスをオンにします。  
  
     **[ユーザーにハンドルされていないとき]** 設定を使用するには、 **[マイ コードのみ]** を有効にする必要があります。  
  
### <a name="to-use-best-practices-for-aspnet-exception-handling"></a>ASP.NET の例外処理で推奨される手順を使用するには  
  
- 予測でき、処理方法がわかる例外をスローできるコードを、`try … catch` ブロックで囲みます。 たとえば、アプリケーションが XML Web サービスを呼び出したり、SQL Server に直接呼び出したりする場合、そのコードは [try...] **catch** ブロック。発生する可能性のある例外は多数あります。
