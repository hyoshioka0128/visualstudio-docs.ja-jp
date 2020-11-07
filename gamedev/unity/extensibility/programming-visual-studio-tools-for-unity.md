---
title: Visual Studio Tools for Unity のプログラミング | Microsoft Docs
description: Visual Studio Tools for Unity (VSTU) API を使用したプログラミングの例を確認します。 VSTU によって作成されたプロジェクト ファイルをカスタマイズします。 Unity のログ コールバックを VSTU と共有します。
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: conceptual
ms.assetid: a5758cb0-e73b-45f5-8cae-c0eb40491026
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: c98a3cdbcece87ad5e8fbe0e91ae76f677494477
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "94341329"
---
# <a name="program-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity をプログラミングする
このセクションでは、Visual Studio Tools for Unity API を使用するための例が示されています。

## <a name="examples"></a>例
 ここでは、Visual Studio Tools for Unity API の使用方法を示す例をいくつか示します。

### <a name="customize-project-files-created-by-vstu"></a>VSTU によって作成されたプロジェクト ファイルのカスタマイズ
 Visual Studio Tools for Unity は、プロジェクト ファイルの生成時に Unity スタイルのコールバックを提供します。 再生成のたびにプロジェクト ファイルを変更する方法については、「[例: プロジェクト ファイルの生成](./customize-project-files-created-by-vstu.md)」をご覧ください。

### <a name="share-the-unity-log-callback-with-vstu"></a>Unity のログ コールバックを VSTU と共有する
 Visual Studio Tools for Unity では、Unity コンソールを Visual Studio にストリーミングできるよう、Unity にログ コールバックを登録します。 エディターのスクリプトもログ コールバックを Unity に登録すると、VSTU コールバックがそれから影響を受けることがあります。 VSTU と Unity ログ コールバックを共有する方法については、「[例: ログ コールバック](./share-the-unity-log-callback-with-vstu.md)」をご覧ください。
