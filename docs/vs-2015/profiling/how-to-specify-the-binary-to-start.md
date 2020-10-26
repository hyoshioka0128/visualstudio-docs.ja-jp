---
title: '方法: 開始するバイナリを指定する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.itemlaunch
helpviewer_keywords:
- profiling tools, launching
- performance tools, launching
- performance sessions, launching
ms.assetid: ba77fcf4-8d78-49f1-b8f3-7dd0acf84306
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 919e84393cf4aef929a504aadbefe905afe24bfb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203433"
---
# <a name="how-to-specify-the-binary-to-start"></a>方法 : 開始するバイナリを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DLL などのバイナリをプロファイルするには、 **[\<Target> プロパティ ページ]** ダイアログ ボックスに情報を入力する必要があります。 この情報は、DLL プロジェクトの呼び出し元アプリケーションの場所を示します。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
### <a name="to-specify-the-executable-to-start"></a>開始する実行可能ファイルを指定するには  
  
1. **パフォーマンス エクスプローラー**で、対象のバイナリを右クリックし、 **[プロパティ]** をクリックします。  
  
2. **[プロパティ ページ]** ダイアログ ボックスで、 **[起動]** プロパティをクリックします。  
  
3. **[プロジェクト プロパティのオーバーライド]** チェック ボックスを選択します。  
  
4. **[起動する実行可能ファイル]** テキスト ボックスで、ファイルの場所を指定します。  
  
5. **[引数]** テキスト ボックスで、アプリケーションを起動するのに必要な引数を指定します。  
  
6. **[作業ディレクトリ]** テキスト ボックスで、ディレクトリの場所を指定します。  
  
7. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [パフォーマンスセッションの構成](../profiling/configuring-performance-sessions.md)
