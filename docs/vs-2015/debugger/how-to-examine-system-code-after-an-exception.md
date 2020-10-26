---
title: '方法: 例外の後にシステムコードを調べる |Microsoft Docs'
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
- debugging, exceptions
- exceptions, debugging
ms.assetid: a38ad49b-7cf3-483d-91c4-eb3116eba50c
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5c34b2fdf2b6400ffe88f9e9ff08cbe6e4b41daa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155577"
---
# <a name="how-to-examine-system-code-after-an-exception"></a>方法: 例外の後にシステム コードを調べる
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

例外が発生した場合、システム コール内のコードを調べて、例外の原因を判断する必要がある場合があります。 システム コードのシンボルが読み込まれていない場合、または [マイ コードのみ] が有効な場合にこの操作を行う方法を次の手順に示します。  
  
### <a name="to-examine-system-code-following-an-exception"></a>例外の後にシステム コードを調べるには  
  
1. **[呼び出し履歴]** ウィンドウを右クリックし、 **[外部コードの表示]** をクリックします。  
  
     [マイ コードのみ] が有効でない場合、ショートカット メニューにこのオプションは表示されず、既定でシステム コードが表示されます。  
  
2. **[呼び出し履歴]** ウィンドウに表示される外部コード フレームを右クリックします。  
  
3. **[シンボルの読み込み元]** をポイントし、 **[Microsoft シンボル サーバー]** をクリックします。  
  
    1. [マイ コードのみ] が有効な場合、ダイアログ ボックスが表示されます。 [マイ コードのみ] が無効になったことが示されます。 これは、システム コールにステップ インするために必要です。  
  
    2. **[パブリック シンボルをダウンロードしています]** ダイアログ ボックスが表示されます。 このダイアログ ボックスは、ダウンロードが終了すると消えます。  
  
4. **[呼び出し履歴]** ウィンドウおよび他のウィンドウで、システム コードを調べることができるようになります。 たとえば、呼び出し履歴のフレームをダブルクリックすると、ソースや **[逆アセンブル]** ウィンドウ内のコードを表示できます。  
  
## <a name="see-also"></a>参照  
 [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)
