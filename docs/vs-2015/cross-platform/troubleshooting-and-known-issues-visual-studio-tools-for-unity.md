---
title: トラブルシューティングと既知の問題 (Visual Studio Tools for Unity) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-unity-tools
ms.topic: troubleshooting
ms.assetid: 8f5db192-8d78-4627-bd07-dbbc803ac554
caps.latest.revision: 7
author: conceptdev
ms.author: crdun
manager: jillfra
ms.openlocfilehash: ad085cc6c41714a551fbb344274e6d0f164ab67e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297657"
---
# <a name="troubleshooting-and-known-issues-visual-studio-tools-for-unity"></a>トラブルシューティングと既知の問題 (Visual Studio Tools for Unity)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションには、Visual Studio Tools for Unity における一般的な問題の解決法、既知の問題についての説明、およびエラー報告によって Visual Studio Tools for Unity を改善する方法について記されています。  
  
## <a name="troubleshooting"></a>トラブルシューティング  
 Visual Studio Tools for Unity の一般的な問題を解決するには、以下のセクションを参照してください。  
  
### <a name="migrating-from-unityvs-to-visual-studio-tools-for-unity"></a>UnityVS から UnityVS to Visual Studio Tools for Unity への移行  
 UnityVS から Visual Studio Tools for Unity に移行している場合、Unity プロジェクト用の新しい Visual Studio ソリューションを生成する必要があります。  
  
##### <a name="to-migrate-your-unity-project-from-unityvs-18-to-visual-studio-tools-for-unity-19"></a>Unity プロジェクトを UnityVS 1.8 から Visual Studio Tools for Unity 1.9 に移行する方法  
  
1. 古いソリューションとプロジェクト ファイルを Unity プロジェクトから削除します。 Unity プロジェクトのルート ディレクトリで、Visual Studio .sln と *proj ファイルを見つけてすべて削除します。  
  
2. Visual Studio Tools for Unity パッケージを Unity プロジェクトにインポートします。 VSTU パッケージをインポートする方法については、「 [作業の開始](../cross-platform/getting-started-with-visual-studio-tools-for-unity.md) 」ページの「Visual Studio Tools for Unity の構成」をご覧ください。  
  
3. 新しいソリューションとプロジェクト ファイルを生成します。 今すぐに作成する場合は、Unity エディターのメイン メニューで、 **[Visual Studio Tools]** 、 **[Generate Project Files]** を選択します。 あるいは、この手順をスキップすることもできます。その場合、 **[Visual Studio Tools]** 、 **[Open in Visual Studio]** と選択すると新しいファイルが自動的に Visual Studio Tools for Unity によって作成されます。  
  
### <a name="visual-studio-wont-load-the-solution-that-visual-studio-tools-for-unity-created"></a>Visual Studio が Visual Studio Tools for Unity によって作成されたソリューションを読み込まない  
 詳細については、 [この stackoverflow の質問に対する回答](https://stackoverflow.com/questions/20086755/unityvs-visual-studio-can-not-open/24035907#24035907)を参照してください。  
  
### <a name="on-windows-8-visual-studio-asks-to-download-the-unity-target-framework"></a>Windows 8 の場合に Unity ターゲット フレームワークをダウンロードするよう Visual Studio から求められる  
 UnityVS には .NET Framework 3.5 が必要ですが、Windows 8 では既定でインストールされません。 この問題を解決するには、.NET Framework 3.5 のダウンロードとインストールに関する手順に従ってください。  
  
## <a name="known-issues"></a>既知の問題  
 デバッガーが Unity の古いバージョンの C# コンパイラとやり取りする方法に起因する、Visual Studio Tools for Unity の既知の問題があります。 これらの問題を修正するために作業中ですが、修正されるまでは以下の問題が発生する可能性があります。  
  
- デバッグ時に Unity がクラッシュすることがあります。  
  
- デバッグ時に Unity がフリーズすることがあります。  
  
- メソッドのステップインとステップアウトが正しく動作しないことがあります。特に、反復子または switch ステートメント内でこれが生じる可能性があります。  
  
## <a name="reporting-errors"></a>エラーの報告  
 クラッシュ、フリーズ、またはその他のエラーが発生する場合、エラー レポートを送信することによって、Visual Studio Tools for Unity の品質向上にご協力ください。 Visual Studio Tools for Unity における問題の調査と解決に役立ちます。 ご協力に感謝いたします。  
  
### <a name="how-to-report-an-error-when-visual-studio-freezes"></a>Visual Studio がフリーズする場合にエラーを報告する方法  
 Visual Studio Tools for Unity でデバッグすると Visual Studio がフリーズするという報告を受け取っていますが、問題を把握するためにさらにデータを必要としています。 次の手順を実行していただくと、調査に役立ちます。  
  
##### <a name="to-report-that-visual-studio-freezes-while-debugging-with-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity でデバッグすると Visual Studio がフリーズすることを報告する方法  
  
1. Visual Studio の新しいインスタンスを開きます。  
  
2. [プロセスにアタッチ] ダイアログ ボックスを開きます。 Visual Studio の新しいインスタンスのメイン メニューで、 **[デバッグ]** 、 **[プロセスにアタッチ]** を選択します。  
  
3. Visual Studio のフリーズしたインスタンスに、デバッガーをアタッチします。 **[プロセスにアタッチ]** ダイアログ ボックスで、 **[選択可能なプロセス]** テーブルからフリーズした Visual Studio インスタンスを選択し、 **[アタッチ]** ボタンを選択します。  
  
4. デバッガーを一時停止します。 Visual Studio の新しいインスタンスのメイン メニューで、 **[デバッグ]** 、 **[すべて中断]** を選択するか、単に **Ctrl+Alt+Break**押します。  
  
5. スレッド ダンプを作成します。 コマンド ウィンドウで、次のコマンドを入力して **Enter**を押します。  
  
   ```powershell  
   Debug.ListCallStack /AllThreads /ShowExternalCode  
   ```  
  
    最初に **[コマンド]** ウィンドウを表示しなければならない場合もあります。 Visual Studio のメイン メニューで、 **[ビュー]** 、 **[その他のウィンドウ]** 、 **[コマンド ウィンドウ]** の順に選択します。  
  
6. 最後に、Visual Studio がフリーズ状態になったときに実行していた作業内容に関する説明を添えて、スレッド ダンプを [vstusp@microsoft.com](mailto:vstusp@microsoft.com)に送信します。
