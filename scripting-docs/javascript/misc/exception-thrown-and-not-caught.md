---
title: 例外がスローされ、キャッチされない |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5022
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b5235490-a8e7-42e3-804e-d85235bc6f05
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 05a9e4f51d5daf7a9e1b1153acbbe8b76b539b72
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572858"
---
# <a name="exception-thrown-and-not-caught"></a>例外がスローされ、キャッチされませんでした。
含まれていること、`throw`内では、コード内のステートメントが囲まれていない、**try** ブロック、または関連付けられていませんが**catch** エラーをトラップするブロック。 内から例外がスローされた、**try** ブロックを使用して、**throw** ステートメントでは、外キャッチし、**try**でブロック、**catch** ステートメント。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 例外をスローするコードを囲む、**try**がありますが、対応することを確認して、ブロック**catch** ブロックします。  
  
- Catch ステートメントで正しい形式の例外が想定されていることを確認してください。  
  
- 例外が再スローされた場合は、対応する別の catch ステートメントがあることを確認します。  
  
## <a name="see-also"></a>参照  
 [エラーオブジェクト](../../javascript/reference/error-object-javascript.md)   
 [Throw ステートメント](../../javascript/reference/throw-statement-javascript.md)   
 [try… catch… finally ステートメント](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)