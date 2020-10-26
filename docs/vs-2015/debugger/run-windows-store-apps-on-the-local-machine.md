---
title: ローカルコンピューターで Windows ストアアプリを実行する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: e42a21a8-6423-4caf-b4dc-72b263e76019
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 031d764b95aa0f292702dde6167e0be9826270bf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196317"
---
# <a name="run-windows-store-apps-on-the-local-machine"></a>ローカル コンピューターでの Windows ストア アプリの実行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows のみに適用されます] (../Image/windows_only_content.png "windows_only_content")  
  
 Windows ストア アプリのパフォーマンス分析のデバッグ、テスト、実行を行う場合、Visual Studio をホストする同じコンピューター上でアプリを実行することができます。 デバイスのディスプレイがタッチ対応である場合は、アプリの全機能を実施できますが、そうでない場合の操作はマウスとキーボードに限定されます。  
  
## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容  
 以下を学習できます。  
  
 [ローカル コンピューター上での実行方法](#BKMK_How_to_run_on_a_local_machine)  
  
 [1 つのモニターで Windows ストア アプリと Visual Studio を切り替える方法](#BKMK_How_to_switch_between_a_Windows_Store_app_and_Visual_Studio_on_a_single_monitor)  
  
## <a name="how-to-run-on-a-local-machine"></a><a name="BKMK_How_to_run_on_a_local_machine"></a> ローカルコンピューターでを実行する方法  
 ローカルコンピューターでアプリケーションを実行するには、[デバッガーの**標準**] ツールバーの [デバッグの開始] ボタンの横にあるドロップダウンリストから [**ローカルコンピューター** ] を選択します。  
  
 ![ローカル コンピューターでの実行](../debugger/media/vsrun-f5-local.png "VSRUN_F5_Local")  
  
 [ **標準** ] ツールバーが表示されない場合は、[ **表示** ] メニューの [ **ツールバー**] をポイントし、[ **標準**] をクリックします。  
  
 ドロップダウン リストでの選択はプロジェクトのプロパティ ファイルに残され、既定の実行ターゲットとなります。  
  
 実行ターゲットは、プロジェクトのプロパティ ファイルに直接設定することもできます。 **ソリューションエクスプローラー**でプロジェクト名を右クリックし、[**プロパティ**] を選択します。 次のいずれかの手順を行います。  
  
- C# および Visual Basic プロジェクトで、[**デバッグ**] をクリックし、[**ターゲットデバイス**] ボックスの一覧から [**ローカルコンピューター** ] を選択します。  
  
     ![C&#35; と Visual Basic プロジェクトのプロパティページ](../debugger/media/vsrun-cs-vb-projprop-local.png "VSRUN_CS_VB_ProjProp_Local")  
  
- C++ と JavaScript のプロジェクトで、[**構成プロパティ**] ノードを展開し、[**デバッグ**] をクリックします。次に、[**起動するデバッガー** ] ボックスの一覧から [**ローカルデバッガー** ] を選択します。  
  
     ![C&#43;&#43; と JavaScript のプロジェクトプロパティページ](../debugger/media/vsrun-cpp-js-projprop-local.png "VSRUN_CPP_JS_ProjProp_Local")  
  
## <a name="how-to-switch-between-a-windows-store-app-and-visual-studio-on-a-single-monitor"></a><a name="BKMK_How_to_switch_between_a_Windows_Store_app_and_Visual_Studio_on_a_single_monitor"></a> 1つのモニターで Windows ストアアプリと Visual Studio を切り替える方法  
 **Windows ストア アプリの実行中のインスタンスから Visual Studio へ切り替えるには**  
  
 ローカル コンピューターで Windows ストア アプリを実行する際に 1 つのモニターだけを使用する場合は、アプリを実行したまま Visual Studio へ切り替えるといいでしょう。 たとえば、イベント待ちだったり長いループや無限ループにトラップされるなど、アプリがブレークポイントに到達できない状態にある可能性があります。 Visual Studio に戻るには、Alt + Tab キーを押します。
