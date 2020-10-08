---
title: '方法: スレッド ビューでスレッドを検索する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- threads, searching
ms.assetid: 5609a9b3-c279-4426-9e2e-dd87896a6d6f
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d5974bc962faf439af8de5d50bf51bad3d824647
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "91838458"
---
# <a name="how-to-search-for-a-thread-in-threads-view"></a>方法: スレッド ビューでスレッドを検索する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

スレッド ID またはモジュール文字列を検索条件として使用することで、スレッド ビューで特定のスレッドを検索できます。 検索の最初の方向を指定することもできます。 ダイアログ ボックスのフィールドには、スレッド ツリー内の選択されたスレッドの属性が表示されます。  
  
### <a name="to-search-for-a-thread-in-threads-view"></a>スレッド ビューでスレッドを検索するには  
  
1. Spy++ およびアクティブな [[スレッド ビュー]](../debugger/threads-view.md) ウィンドウが表示されるように、ご利用のウィンドウを配置します。  
  
2. **[検索]** メニューから、 **[スレッドの検索]** を選択します。  
  
    [[スレッド検索] ダイアログ ボックス](../debugger/thread-search-dialog-box.md)が開きます。  
  
3. 検索条件として、スレッド ID またはモジュール文字列を入力します。  
  
4. 値を指定しないフィールドはいずれもクリアします。  
  
   > [!TIP]
   > モジュールによって所有されているすべてのスレッドを検索するには、 **[スレッド]** テキスト ボックスをクリアし、 **[モジュール]** ボックスにモジュール名を入力します。 その後、 **[次を検索]** を使用してスレッドの検索を続行します。  
  
5. 検索の最初の方向として、 **[上]** または **[下]** を選択します。  
  
6. **[OK]** をクリックします。  
  
   一致するスレッドが見つかった場合は、[スレッド ビュー] ウィンドウで強調表示されます。
