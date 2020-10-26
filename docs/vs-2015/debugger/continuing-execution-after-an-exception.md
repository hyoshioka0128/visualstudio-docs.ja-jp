---
title: 例外後の実行の継続 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
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
- managed exceptions, continuing execution after
- exceptions, continuing execution after
- debugger, exceptions
- managed code, exception handling
- exception handling, continuing execution after
- execution, continuing after an exception
- program execution
- threading [Visual Studio], continuing execution after exceptions
- Exceptions dialog box
- programs, executing
ms.assetid: 6fe97aac-2131-4615-bd92-d3afee741558
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6ae74c51f0f738bc596fbe5c789011630927707c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702267"
---
# <a name="continuing-execution-after-an-exception"></a>例外後の実行の継続
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

例外が発生してデバッガーによる実行が中断されると、ダイアログ ボックスが表示されます。 Visual Basic または C# の場合は、既定で [ [例外処理アシスタント](https://msdn.microsoft.com/library/992892ac-9d52-44cc-bf09-b44bfc5befeb) ] ダイアログボックスが表示されます。 C++ の場合は、[古い **例外** ] ダイアログボックスが表示されます。 Visual Basic または C# を使用していても、[**オプション**] ダイアログボックスで**例外処理アシスタント**が無効になっている場合は、[**例外**] ダイアログボックスが表示されます。  
  
 [ **例外処理アシスタント** ] または [ **例外** ] ダイアログボックスが表示されたら、例外の原因となった問題の修正を試みることができます。  
  
## <a name="managed-code"></a>マネージド コード  
 マネージド コードでは、未処理の例外の後に同じスレッドで実行を継続できます。 **例外処理アシスタント**は、例外がスローされた時点までコールスタックを戻します。  
  
## <a name="native-code"></a>ネイティブ コード  
 ネイティブ C/C++ では、2 つのオプションがあります。  
  
- [ **中断** ] をクリックして、問題を解決することができます。 中断モードでは、[ **呼び出し履歴** ] ウィンドウでフレームを右クリックし、ショートカットメニューの [ **このフレームへのアンワインド** ] を選択して、呼び出し履歴をアンワインドできます。 デバッグを続行すると、問題が修正されていない場合は、[ **例外** ] ダイアログボックスが再び表示されます。 それ以外の場合、[ **例外** ] ダイアログボックスは表示されません。  
  
- [ **続行** ] をクリックすると、問題を解決せずに実行を続行できます。 [ **例外** ] ダイアログボックスが再び表示されます。  
  
## <a name="mixed-code"></a>混合コード  
 ネイティブ コードとマネージド コードが混在するコードをデバッグしているときに、ハンドルされていない例外が発生した場合、オペレーティング システムの制約により、呼び出し履歴のアンワインドが抑制されます。 ショートカット メニューを使用して呼び出し履歴をさかのぼろうとすると、混合コードのデバッグ中は、ハンドルされていない例外からアンワインドすることはできないという内容のエラー メッセージが表示されます。  
  
## <a name="see-also"></a>参照  
 [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)
