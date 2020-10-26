---
title: クライアント側のスクリプトのデバッグ |Microsoft Docs
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
- debugging [Visual Studio], client-side scripts
- client-side scripts, debugging
ms.assetid: bb668527-2288-47bd-a6c8-cecbad76dde2
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6405a35068b7be7ac93eb91f4d9100e6a840b0bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702381"
---
# <a name="client-side-script-debugging"></a>クライアント側スクリプトのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio デバッガーには、ASP.NET ページ内のクライアント側スクリプトのエラーを検出および修正するための包括的なデバッグ環境が用意されています。  
  
## <a name="opening-script-documents"></a>スクリプト ドキュメントを開く  
 **ソリューション エクスプローラー** では、閲覧できるサーバー側およびクライアント側のスクリプト ドキュメントのリストを表示できます。 **ソリューション エクスプローラー**で、任意のスクリプト ドキュメントを開くことができます。 詳細については、[スクリプト ドキュメントを表示する](../debugger/how-to-view-script-documents.md)」を参照してください。  
  
## <a name="breakpoint-mapping"></a>ブレークポイントのマップ  
 Visual Studio では、サーバー側コードを直接デバッグすることはできませんが、サーバー側ファイルにブレークポイントを設定できます。 Visual Studio では、設定されたブレークポイントがクライアント側ファイルの対応する場所に自動的にマップされ、マップされたブレークポイントがクライアント側コードに作成されます。  
  
## <a name="manually-or-automatically-attaching-to-script"></a>手動または自動によるスクリプトへのアタッチ  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]でスクリプトをデバッグするには、デバッグするスクリプトにデバッガーをアタッチする必要があります。 これは手動で行うことも、自動的に行うこともできます。  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デバッガー インターフェイスを使用して、アタッチする実行中のスクリプト プロセスを選択することにより、手動でアタッチできます。 詳細については、「 [How to: Attach to Script](../debugger/how-to-attach-to-script.md)」を参照してください。  
  
 次のいずれかの状況が発生すると、デバッガーは自動的にスクリプトにアタッチされます。  
  
- スクリプトに設定されているブレークポイントにヒットした。  
  
- スクリプト コード内の VBScript `Stop` ステートメントまたは JScript `debugger` ステートメントにヒットした。  
  
- ブラウザーまたはサーバーが、スクリプト内で構文エラーまたはランタイム エラーを検出した。 これが発生すると、ダイアログ ボックスが表示され、デバッグを開始できます。  
  
  手動でスクリプトにアタッチした場合、そのスクリプト プロセスは、何らかの理由で停止するまで、引き続き実行されます。 **[デバッグ]** メニューの **[中断]** を選択することによって、プロセスを停止できます。  
  
  デバッガーが自動的にアタッチされると、スクリプトの実行は、ブレークポイント、 `Stop` ステートメント、 `debugger` ステートメント、またはエラーが発生した行、あるいは Internet Explorer でデバッグを開始するように選択した位置で停止します。  
  
  この時点で、通常のデバッガー機能を使用してデバッグを開始できます。 たとえば、 **[ステップ]** コマンドを使用すると、コードを行単位で継続して実行できます。 **[呼び出し履歴]** ウィンドウを使用して、スクリプトのフローの表示と制御を行うことができます。 変数ウィンドウまたは **イミディエイト** ウィンドウを使用して、変数およびプロパティの表示または変更を行うことができます。  
  
## <a name="enhanced-error-messages-for-script-debugging"></a>スクリプト デバッグのための強化されたエラー メッセージ  
 Visual Studio では、一般的なスクリプトのデバッグ問題を示すエラー メッセージが強化されています。 これらのメッセージは、Internet Explorer に手動でアタッチした場合のみ表示されます。 Internet Explorer が自動的に開かれたときにエラー状態が検出される場合は、手動でアタッチするとエラー メッセージが表示されます。  
  
## <a name="debugging-ajax-script-applications"></a>AJAX スクリプト アプリケーションのデバッグ  
 AJAX 対応の Web アプリケーションではスクリプト コードを頻繁に使用するため、デバッグは困難になる可能性があります。 AJAX をデバッグする手法の詳細については、次を参照してください。  
  
 [Debugging and Tracing Ajax Applications Overview](https://msdn.microsoft.com/library/92684ea0-7bb4-4a34-9203-3aa6394ce375)で、任意のスクリプト ドキュメントを開くことができます。  
  
## <a name="see-also"></a>参照  
 [ASP.NET と AJAX アプリケーションのデバッグ](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [スクリプトのデバッグに関する制限事項](../debugger/limitations-on-script-debugging.md)   
 [変数ウィンドウ](https://msdn.microsoft.com/library/ce0a67f6-2502-4b7a-ba45-cc32f8aeba3e)   
 [イミディエイトウィンドウ](../ide/reference/immediate-window.md)   
 [Ajax アプリケーションのデバッグとトレースの概要](https://msdn.microsoft.com/library/92684ea0-7bb4-4a34-9203-3aa6394ce375)
