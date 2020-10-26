---
title: '方法: 高パフォーマンス クラスター上でデバッグする | Microsoft Docs'
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
- cluster debugging
- high-performance debugging
ms.assetid: a2f0eb07-840e-4f95-a1b1-9509217e5b8f
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f4487b168c3d405b2449bcfb9515e60f0ea67ed1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702691"
---
# <a name="how-to-debug-on-a-high-performance-cluster"></a>方法 : 高パフォーマンス クラスター上でデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

高パフォーマンス クラスター上でのマルチプロセス プログラムのデバッグは、リモート コンピューター上での通常のプログラムのデバッグと似ています。 ただし、追加の考慮事項がいくつかあります。 一般的なリモート セットアップ要件については、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。  
  
 高パフォーマンス クラスター上でデバッグするときは、リモート デバッグに使用できる [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のデバッグ ウィンドウとデバッグ手法をすべて使用できます。 ただし、リモートでデバッグするため、外部のコンソール ウィンドウは使用できません。  
  
 **[スレッド]** ウィンドウと **[プロセス]** ウィンドウは、並列アプリケーションをデバッグする際に特に役立ちます。 これらのウィンドウの使用方法に関するヒントについては、「 [方法: [プロセス] ウィンドウを使用](https://msdn.microsoft.com/0207ce2f-8ceb-4fe7-b2b5-4dd35b035ed7) する」および「 [方法: [スレッド] ウィンドウ](../debugger/how-to-use-the-threads-window.md)を使用する」を参照してください。  
  
 以下の手順では、高パフォーマンス クラスター上でのデバッグに特に役立つ手法を示します。  
  
 並列アプリケーションをデバッグするときは、特定のスレッド、プロセス、またはコンピューターにブレークポイントを設定することが必要になる場合があります。 これを行うには、通常のブレークポイントを作成してから、ブレークポイント フィルターを追加します。  
  
### <a name="to-open-the-breakpoint-filter-dialog-box"></a>[ブレークポイントのフィルター] ダイアログ ボックスを開くには  
  
1. ソース ウィンドウ、 **[逆アセンブル]** ウィンドウ、 **[呼び出し履歴]** ウィンドウ、または **[ブレークポイント]** ウィンドウでブレークポイント グリフを右クリックします。  
  
2. ショートカット メニューの **[フィルター]** をクリックします。 このオプションは、最上位レベルまたは **[ブレークポイント]** のサブメニューとして表示されます。  
  
### <a name="to-set-a-breakpoint-on-a-specific-computer"></a>特定のコンピューターにブレークポイントを設定するには  
  
1. **[プロセス]** ウィンドウでコンピューター名を確認します。  
  
2. ブレークポイントを選択し、前記の手順に従って **[ブレークポイントのフィルター]** ダイアログ ボックスを開きます。  
  
3. **[ブレークポイントのフィルター]** ダイアログ ボックスに次の文字列を入力します。  
  
     MachineName =*yourmachinename*  
  
     より複雑なフィルターを作成する場合は、AND 演算子 (`&`)、OR 演算子 (`||`)、NOT 演算子 (`!`)、およびかっこを使って句を結合できます。  
  
4. **[OK]** をクリックします。  
  
### <a name="to-set-a-breakpoint-on-a-specific-process"></a>特定のプロセスにブレークポイントを設定するには  
  
1. **[プロセス]** ウィンドウで、プロセス名またはプロセス ID 番号を取得します。  
  
2. ブレークポイントを選択し、最初の手順に従って **[ブレークポイントのフィルター]** ダイアログ ボックスを開きます。  
  
3. **[ブレークポイントのフィルター]** ダイアログ ボックスに次の文字列を入力します。  
  
     `ProcessName =`  *yourprocessname*  
  
     または  
  
     `ProcessID =` *yourprocessIDnumber*  
  
     より複雑なフィルターを作成する場合は、AND 演算子 (`&`)、OR 演算子 (`||`)、NOT 演算子 (`!`)、およびかっこを使って句を結合できます。  
  
4. **[OK]** をクリックします。  
  
### <a name="to-set-a-breakpoint-on-a-specific-thread"></a>特定のスレッドにブレークポイントを設定するには  
  
1. **[スレッド]** ウィンドウで、スレッド名またはスレッド ID 番号を取得します。  
  
2. ブレークポイントを選択し、最初の手順に従って **[ブレークポイントのフィルター]** ダイアログ ボックスを開きます。  
  
3. **[ブレークポイントのフィルター]** ダイアログ ボックスに次の文字列を入力します。  
  
     `ThreadName =` *yourthreadname*  
  
     または  
  
     `ThreadID =` *yourthreadIDnumber*  
  
     より複雑なフィルターを作成する場合は、AND 演算子 (`&`)、OR 演算子 (`||`)、NOT 演算子 (`!`)、およびかっこを使って句を結合できます。  
  
4. **[OK]** をクリックします。  
  
## <a name="example"></a>例  
 次の例は、`marvin` というコンピューターと `fourier1` というスレッドを対象とするブレークポイントのフィルターを作成する方法を示しています。  
  
```  
(MachineName = marvin) & (ThreadName = fourier1)  
```  
  
## <a name="see-also"></a>参照  
 [マルチスレッドアプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [リモートデバッグ](../debugger/remote-debugging.md)   
 [方法: [プロセス] ウィンドウを使用する](https://msdn.microsoft.com/0207ce2f-8ceb-4fe7-b2b5-4dd35b035ed7)   
 [方法: [スレッド] ウィンドウを使用する](../debugger/how-to-use-the-threads-window.md)   
 [スレッドとプロセス](https://msdn.microsoft.com/73d87480-9af3-4d1b-baf5-397d5d876ae6)   
 [ブレークポイントの使用](../debugger/using-breakpoints.md)
