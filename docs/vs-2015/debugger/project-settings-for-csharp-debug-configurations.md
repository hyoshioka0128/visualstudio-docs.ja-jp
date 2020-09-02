---
title: C# デバッグ構成のプロジェクト設定 |Microsoft Docs
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
- debug configurations, C#
- debugging [J#], debugger settings
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- project configurations, debug
- debugging [C#], debugger settings
- debug configurations, J#
ms.assetid: e30ca810-66e9-4d6e-9cf6-9f285cd0b100
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f1ec1c18fe92409a72994e4544215da01325d209
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687517"
---
# <a name="project-settings-for--c-debug-configurations"></a>C# デバッグ構成のプロジェクト設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C# デバッグ構成のプロジェクト設定は、「[デバッグ構成とリリース構成](../debugger/how-to-set-debug-and-release-configurations.md)」で説明されているように、[**プロパティページ**] ウィンドウで変更できます。 次の表は、 **[プロパティ ページ]** ウィンドウのデバッガー関連の設定の場所を示しています。  
  
> [!WARNING]
> このトピックは Windows ストア アプリには適用されません。 「[デバッグ セッションの開始 (VB、C#、C++、および XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)」を参照してください。  
  
## <a name="debug-tab"></a><a name="BKMK_Debug_tab"></a> [デバッグ] タブ  
  
|**設定**|**説明**|  
|-----------------|---------------------|  
|**構成**|アプリケーションをコンパイルするためのモードを設定します。 **[Active (Debug)]\(アクティブ (デバッグ)\)** 、 **[デバッグ]** 、 **[リリース]** 、 **[すべての構成]** から選択します。|  
|**開始動作**|[デバッグ] メニューの [開始] を選択したときに発生するアクションを指定します。<br /><br /> -   既定値は **[プロジェクトの開始]** で、デバッグのスタートアップ プロジェクトを起動します。 詳細については、「 [スタートアッププロジェクトの選択](https://msdn.microsoft.com/222e3f32-a6fe-4941-bf37-6b2a921129fd)」を参照してください。<br />-    **[外部プログラムの開始]** では、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトに含まれないプログラムを起動してアタッチできます。 詳細については、「 [実行中のプログラムへのアタッチ](https://msdn.microsoft.com/636d0a52-4bfd-48d2-89ad-d7b9ca4dc4f4)」を参照してください。<br />-    **[ブラウザーを開始時に使用する URL]** は、Web アプリケーションのデバッグを有効にします。|  
|**コマンド ライン引数**|デバッグするプログラムのコマンド ライン引数を指定します。 コマンド名は、[外部プログラムの開始] に指定されたプログラム名です。 [開始動作] が [URL の開始] に設定されている場合、コマンド ライン引数は指定できません。|  
|**作業ディレクトリ**|デバッグするプログラムの作業ディレクトリを指定します。 [!INCLUDE[csprcs](../includes/csprcs-md.md)] では、作業ディレクトリはアプリケーションが起動されるディレクトリであり、既定では \bin\debug です。|  
|**リモート コンピューターの使用**|デバッグのためにアプリケーションを実行するリモートコンピューターの名前、または [Msvsmon サーバー名](https://msdn.microsoft.com/library/55b60ce7-834b-4e83-a10e-fe4248260a4c)。 リモート コンピューター上の EXE ファイルの場所は、[構成プロパティ] フォルダー、[ビルド] カテゴリ内の [出力パス] プロパティで指定します。 また、EXE ファイルがリモート コンピューターの共有ディレクトリにあることも必要です。|  
|**アンマネージ コード デバッグを有効にする**|マネージド アプリケーションからネイティブ (アンマネージド) Win32 コードの呼び出しをデバッグできます。|  
|**SQL Server デバッグを有効にする**|SQL Server データベース オブジェクトのデバッグを許可します。|  
  
## <a name="build-tab"></a><a name="BKMK_Build_tab"></a> [ビルド] タブ  
  
|設定|説明|  
|-------------|-----------------|  
|**条件付きコンパイルシンボル:**|定数 DEBUG および定数 TRACE をここで定義します。<br /><br /> これらの定数により、[Debug クラス](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx)と [Trace クラス](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)の条件付きコンパイルが有効になります。 これらの定数を定義すると、Debug クラスと Trace クラスのメソッドによって[出力ウィンドウ](../ide/reference/output-window.md)に出力が生成されます。 これらの定数を定義しない場合、Debug クラスと Trace クラスのメソッドはコンパイルされず、出力も生成されません。<br /><br /> -Debug は通常、プログラムのデバッグバージョンで定義され、リリースバージョンでは未定義です。<br />-Trace は通常、デバッグバージョンとリリースバージョンの両方で定義されています。|  
|**コードの最適化**|デバッグ バージョンでは、最適化されたコードにだけ現れるバグを見つけた場合に限って、この設定をオンにすることをお勧めします。 最適化されたコードは、命令がソース ウィンドウのステートメントに直接対応していないため、デバッグが困難です。|  
|**出力パス:**|通常は、デバッグ用の bin\Debug に設定します。|  
  
## <a name="see-also"></a>参照  
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
