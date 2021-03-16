---
description: コードに throw ステートメントを含めましたが、try ブロック内で囲まれていないか、エラーをトラップする関連する catch ブロックがありませんでした。
title: 例外がスローされ、キャッチされない |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: b8abcfced6dfe78dc18f4e31d2bd90d5e5a45a4a
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103570636"
---
# <a name="exception-thrown-and-not-caught"></a>例外がスローされ、キャッチされませんでした。
`throw`コードにステートメントを含めましたが、 **try** ブロック内で囲まれていないか、エラーをトラップする関連する **catch** ブロックがありませんでした。 例外は、 **throw** ステートメントを使用して **try** ブロック内からスローされ、 **catch** ステートメントを使用し **て try** ブロックの外側でキャッチされます。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- **Try** ブロックで例外をスローできるコードを囲み、対応する **catch** ブロックがあることを確認します。  
  
- Catch ステートメントで正しい形式の例外が想定されていることを確認してください。  
  
- 例外が再スローされた場合は、対応する別の catch ステートメントがあることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [Error オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error)   
 [throw ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/throw)   
 [お試しください...キャッチ...finally ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/try...catch)
