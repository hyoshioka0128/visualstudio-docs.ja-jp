---
title: '方法: スレッドに対するフラグの設定と解除 | Microsoft Docs'
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
- treads, switching [debugging]
ms.assetid: 952d579d-6911-413e-b3e5-54e7e797e70c
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b6d6a49dd9b90172686a90d92e6b630dd70b5cf0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189433"
---
# <a name="how-to-flag-and-unflag-threads"></a>方法 : スレッドに対するフラグの設定と設定解除を行う
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[ **スレッド**]、[ **並列スタック**]、[ **並列ウォッチ**]、[ **GPU スレッド** ] の各ウィンドウでアイコンを使用してマークすることにより、特に注意するスレッドにフラグを付けることができます。 このアイコンにより、フラグが設定されているスレッドをそれ以外のスレッドと簡単に区別できるようになります。  
  
 フラグが設定されたスレッドは、[デバッグの**場所**] ツールバーの**スレッド**の一覧でも特別な処理を行います。 この一覧では、すべてのスレッドを表示することも、フラグが設定されたスレッドのみを表示することもできます。 スレッドにフラグを設定すると、 **スレッド** の一覧は、フラグが設定されたスレッドのみを表示するように自動的に切り替わりますが、必要に応じてすべてのスレッドを表示するように切り替えることができます。  
  
### <a name="to-flag-or-unflag-a-thread-by-using-the-threads-window"></a>[スレッド] ウィンドウでスレッドに対するフラグを設定または解除するには  
  
- [ **スレッド** ] ウィンドウで、目的のスレッドを見つけ、フラグアイコンをクリックしてフラグをオンまたはオフにします。  
  
### <a name="to-unflag-all-threads"></a>すべてのスレッドのフラグを解除するには  
  
- **[スレッド]** ウィンドウで、いずれかのスレッドを右クリックし、 **[すべてのスレッドのフラグを解除]** をクリックします。  
  
### <a name="to-display-only-flagged-threads"></a>フラグが設定されたスレッドのみ表示するには  
  
- デバッグ ウィンドウでフラグ ボタンをクリックします。  
  
### <a name="to-flag-just-my-code"></a>マイ コードのみにフラグを設定するには  
  
1. **[スレッド]** ウィンドウの上部にあるツール バーで、フラグ アイコンをクリックします。  
  
2. ドロップダウン リストで、 **[マイ コードのみにフラグを設定]** をクリックします。  
  
### <a name="to-flag-threads-that-are-associated-with-selected-modules"></a>選択したモジュールに関連するスレッドにフラグを設定するには  
  
1. **[スレッド]** ウィンドウのツール バーで、フラグ アイコンをクリックします。  
  
2. ドロップダウン リストで、 **[カスタム モジュール選択にフラグを設定]** をクリックします。  
  
3. **[モジュールの選択]** ダイアログ ボックスで、目的のモジュールを選択します。  
  
4. (省略可能) **[検索]** ボックスに、特定のモジュールを検索するための文字列を入力します。  
  
5. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [マルチスレッドアプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [チュートリアル : マルチスレッド アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-multithreaded-application.md)
