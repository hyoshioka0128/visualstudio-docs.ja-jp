---
title: '方法: 高パフォーマンス クラスター上でデバッグする | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- cluster debugging
- high-performance debugging
ms.assetid: a2f0eb07-840e-4f95-a1b1-9509217e5b8f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d95c6eeadfdf1bb90471997712299ae03a945be8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733668"
---
# <a name="how-to-debug-on-a-high-performance-cluster-c-visual-basic-c"></a>方法: 高パフォーマンス クラスター上でデバッグする (C#、Visual Basic、C++)

高パフォーマンス クラスター上でのマルチプロセス プログラムのデバッグは、リモート コンピューター上での通常のプログラムのデバッグと似ています。 ただし、追加の考慮事項がいくつかあります。 一般的なリモート セットアップ要件については、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

 高パフォーマンス クラスター上でデバッグするときは、リモート デバッグに使用できる [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のデバッグ ウィンドウとデバッグ手法をすべて使用できます。 ただし、リモートでデバッグするため、外部のコンソール ウィンドウは使用できません。

 **[スレッド]** ウィンドウと **[プロセス]** ウィンドウは、並列アプリケーションをデバッグする際に特に役立ちます。 これらのウィンドウの使い方に関するヒントについては、「[方法: プロセス ウィンドウを使用する](/previous-versions/visualstudio/visual-studio-2010/7h8h5sdw(v=vs.100))」と「[チュートリアル: スレッド ウィンドウを使用してデバッグする](../debugger/how-to-use-the-threads-window.md)」を参照してください。

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

`(MachineName = marvin) & (ThreadName = fourier1)`

## <a name="see-also"></a>関連項目
- [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [Remote Debugging](../debugger/remote-debugging.md)
- [方法: プロセス ウィンドウを使用する](/previous-versions/visualstudio/visual-studio-2010/7h8h5sdw(v=vs.100))
- [マルチ スレッド アプリケーションのデバッグの開始](../debugger/get-started-debugging-multithreaded-apps.md)
- [スレッドとプロセス](/previous-versions/visualstudio/visual-studio-2010/ms164740(v=vs.100))
- [ブレークポイントの使用](../debugger/using-breakpoints.md)