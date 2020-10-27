---
title: Visual Studio Tools for Unity のプログラミング | Microsoft Docs
description: Visual Studio Tools for Unity (VSTU) API を使用したプログラミングの例を確認します。 VSTU によって作成されたプロジェクト ファイルをカスタマイズします。 Unity のログ コールバックを VSTU と共有します。
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: a5758cb0-e73b-45f5-8cae-c0eb40491026
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 0372cfd110df77867a683b27b17f92cd70ba75aa
ms.sourcegitcommit: 01c1b040b12d9d43e3e8ccadee20d6282154faad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039886"
---
# <a name="program-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity をプログラミングする
このセクションでは、Visual Studio Tools for Unity API を使用するための例が示されています。

## <a name="examples"></a>例
 ここでは、Visual Studio Tools for Unity API の使用方法を示す例をいくつか示します。

### <a name="customize-project-files-created-by-vstu"></a>VSTU によって作成されたプロジェクト ファイルのカスタマイズ
 Visual Studio Tools for Unity は、プロジェクト ファイルの生成時に Unity スタイルのコールバックを提供します。 再生成のたびにプロジェクト ファイルを変更する方法については、「[例: プロジェクト ファイルの生成](../cross-platform/customize-project-files-created-by-vstu.md)」をご覧ください。

### <a name="share-the-unity-log-callback-with-vstu"></a>Unity のログ コールバックを VSTU と共有する
 Visual Studio Tools for Unity では、Unity コンソールを Visual Studio にストリーミングできるよう、Unity にログ コールバックを登録します。 エディターのスクリプトもログ コールバックを Unity に登録すると、VSTU コールバックがそれから影響を受けることがあります。 VSTU と Unity ログ コールバックを共有する方法については、「[例: ログ コールバック](../cross-platform/share-the-unity-log-callback-with-vstu.md)」をご覧ください。
