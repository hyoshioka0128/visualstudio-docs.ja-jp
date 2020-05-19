---
title: '方法: プロセス ビューでプロセスを検索する | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Processes view
- processes, searching for
ms.assetid: 7cb97b37-4a95-4f1b-9eee-4910aa9c115b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2a6b57226b14963759bb4d78afff3beb5559a63e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "64798984"
---
# <a name="how-to-search-for-a-process-in-processes-view"></a>方法: プロセス ビューでプロセスを検索する
プロセス ID またはモジュール文字列を検索条件として使用することで、プロセス ビューで特定のプロセスを検索できます。 検索の最初の方向を指定することもできます。 ダイアログ ボックスのフィールドには、プロセス ツリー内の選択されたプロセスの属性が表示されます。

### <a name="to-search-for-a-process-in-processes-view"></a>プロセス ビューでプロセスを検索するには

1. Spy++ およびアクティブな [[プロセス ビュー]](../debugger/processes-view.md) ウィンドウが表示されるように、ご利用のウィンドウを配置します。

2. **[検索]** メニューから、 **[プロセスの検索]** を選択します

    [[プロセス検索] ダイアログ ボックス](../debugger/process-search-dialog-box.md)が開きます。

3. 検索条件として、プロセス ID またはモジュール文字列を入力します。

4. 値を指定しないフィールドはいずれもクリアします。

   > [!TIP]
   > モジュールによって所有されているすべてのプロセスを検索するには、 **[プロセス]** ボックスをクリアし、 **[モジュール]** ボックスにモジュール名を入力します。 その後、 **[次を検索]** を使用してプロセスの検索を続行します。

5. 検索の最初の方向として、 **[上]** または **[下]** を選択します。

6. **[OK]** をクリックします。

   一致するプロセスが見つかった場合は、 **[プロセス ビュー]** ウィンドウで強調表示されます。