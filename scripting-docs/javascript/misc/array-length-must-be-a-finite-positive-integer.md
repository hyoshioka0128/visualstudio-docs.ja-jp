---
title: 配列の長さは、有限の正の整数でなければなりません |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5029
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1a467040-4702-4178-848f-418a5974e907
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fa8b9a85c0c7457cb06d36fd3cd849ce48484b46
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817087"
---
# <a name="array-length-must-be-a-finite-positive-integer"></a>配列の長さは、有限の正の整数でなければなりません。
整数ではない引数を使用して、**配列**コンストラクターを呼び出しています (0 と正の整数のセットで構成される整数)。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 新しいオブジェクトを作成する場合にのみ、正の整数を使用し `Array` ます。 整数ではない1つの要素を持つ配列を作成する場合は、2段階のプロセスで実行します。 まず、1つの要素を持つ配列を作成してから、最初の要素 (array [0]) に値を配置します。 このエラーを生成する例を次に示します。  
  
    ```JavaScript  
    var piArray = new Array(3.14159);  
    ```  
  
     次の例は、単一の数値要素を持つ配列を指定する正しい方法を示しています。  
  
    ```JavaScript  
    var piArray = new Array(1);  
    piArray [0] = 3.14159;  
    ```  
  
     配列のサイズの上限は、最大の整数値 (約 40億) を超えています。  
  
## <a name="see-also"></a>関連項目  
 [配列の使用](../../javascript/advanced/using-arrays-javascript.md)