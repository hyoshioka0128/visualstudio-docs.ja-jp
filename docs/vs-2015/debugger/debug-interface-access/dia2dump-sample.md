---
title: Dia2dump サンプル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a817720c1ad73b666e0c9a586bb583120a2533c1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197592"
---
# <a name="dia2dump-sample"></a>Dia2dump サンプル
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Dia2dump サンプルは Visual Studio と共にインストールされ、Dia2dump ソースファイルが含まれています。 コンパイルされた実行可能ファイルは、コマンドラインから実行され、プログラムデータベース (.pdb) ファイル全体の内容を表示します。  
  
### <a name="to-install-the-sample"></a>サンプルをインストールするには  
  
1. Visual Studio セットアップの開始ページで説明されているすべてのセットアップ要件をシステムが満たしていることを確認します。  
  
2. Visual Studio をインストールし、含まれているサンプルのすべてのセットアップとインストール手順に従います。  
  
#### <a name="to-build-the-sample"></a>サンプルをビルドするには  
  
1. Visual Studio で Dia2dump ファイルを開きます。 (必要に応じて、Visual Studio は、Dia2dump プロジェクトをアップグレードするために最初に役立ちます)。  
  
2. プロジェクトのプロパティページの [ **C/c + +** &#124; **全般** &#124; **追加のインクルードディレクトリ** ] プロパティで、ディレクトリを指定し `..\DIA SDK\include` ます。 これにより、コンパイラが dia2 ファイルを見つけられることが保証されます。  
  
3. **[ビルド]** メニューで、 **[ソリューションのリビルド]** をクリックします。  
  
4. Visual Studio を閉じます。  
  
#### <a name="to-run-the-sample"></a>サンプルを実行するには  
  
1. コマンド プロンプトを開き、次のコマンドを入力します。  
  
    ```  
    dia2dump filename  
    ```  
  
## <a name="see-also"></a>参照  
 [Dia2dump ソースファイル](../../debugger/debug-interface-access/dia2dump-cpp-source-file.md)   
 [方法: Visual Studio プロジェクトのアップグレードが成功しなかった場合のトラブルシューティング](../../porting/how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades.md)
