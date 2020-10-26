---
title: SDI サーバーアプリケーション |Microsoft Docs
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
- SDI server applications
- SDI server applications, debugging
ms.assetid: 09713718-1376-4753-b119-26f36639693e
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1296c0f43d0409df0081861095c5ec068932bbc1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148146"
---
# <a name="sdi-server-applications"></a>SDI サーバー アプリケーション
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

SDI サーバー アプリケーションをデバッグする場合は、C/C++、C#、または Visual Basic のプロジェクトの [*プロジェクト* プロパティ ページ] ダイアログ ボックスで、 **[コマンド ライン引数]** プロパティに `/Embedding` または `/Automation` を指定する必要があります。  
  
 デバッガーはこれらのコマンド ライン引数を利用して、コンテナーから起動されたようにサーバー アプリケーションを起動できます。 次に、プログラム マネージャーまたはファイル マネージャーからコンテナーを起動すると、コンテナーはデバッガー中で起動されたサーバーのインスタンスを使用できます。  
  
## <a name="finding-the-command-line-arguments-property"></a>[コマンド ライン引数] プロパティの表示  
 [*プロジェクト* プロパティ ページ] ダイアログ ボックスにアクセスするには、ソリューション エクスプローラーでプロジェクトを右クリックし、ショートカット メニューの [プロパティ] を選びます。 [コマンド ライン引数] プロパティを表示するには、[構成プロパティ] カテゴリを展開し、[デバッグ] ページをクリックします。  
  
## <a name="see-also"></a>参照  
 [COM および ActiveX のデバッグ](../debugger/com-and-activex-debugging.md)   
 [方法: COM サーバーをデバッグする](../debugger/how-to-debug-com-servers.md)
