---
title: Visual Basic デバッグ構成のプロジェクト設定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vbProjectPropertiesDebug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- debugging [Visual Basic], debugger settings
- projects [Visual Studio], debug configurations
- project configurations, debug
- debug configurations, Visual Basic
ms.assetid: 72a8483a-af0b-4403-8b0d-ee9ad71ee435
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 27acc89790e0759d3b284e3d9a4c6798c3d9a16f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687572"
---
# <a name="project-settings-for-a-visual-basic-debug-configuration"></a>Visual Basic デバッグ構成のプロジェクト設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

「[デバッグ構成とリリース構成](../debugger/how-to-set-debug-and-release-configurations.md)」で説明されているように、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] のデバッグ構成に対するプロジェクト設定は **[プロパティ ページ]** ウィンドウで変更できます。 次の表は、 **[プロパティ ページ]** ウィンドウのデバッガー関連の設定の場所を示しています。  
  
> [!WARNING]
> このトピックはストア アプリには適用されません。 「[デバッグ セッションの開始 (VB、C#、C++、および XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)」を参照してください。  
  
### <a name="debug-tab"></a>[デバッグ] タブ  
  
|設定|説明|  
|-------------|-----------------|  
|**構成**|アプリケーションをコンパイルするためのモードを設定します。 **[Active (Debug)]\(アクティブ (デバッグ)\)** 、 **[デバッグ]** 、 **[リリース]** 、 **[すべての構成]** から選択します。|  
|**開始動作**|[デバッグ] メニューの [開始] を選択したときに発生するアクションを指定します。<br /><br /> -   既定値は **[プロジェクトの開始]** で、デバッグのスタートアップ プロジェクトを起動します。 詳細については、「 [NIB 方法: Set Startup Projects](https://msdn.microsoft.com/31465836-0911-48db-a5d9-e456b635e970)」を参照してください。<br />-    **[外部プログラムの開始]** では、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトに含まれないプログラムを起動してアタッチできます。 詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。<br />-    **[ブラウザーを開始時に使用する URL]** は、Web アプリケーションのデバッグを有効にします。|  
|**コマンド ライン引数**|デバッグするプログラムのコマンド ライン引数を指定します。 コマンド名は、[外部プログラムの開始] に指定されたプログラム名です。 [開始動作] を [URL の開始] に設定した場合、コマンド ライン引数は無視されます。|  
|**作業ディレクトリ**|デバッグするプログラムの作業ディレクトリを指定します。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] では、作業ディレクトリはアプリケーションが起動されるディレクトリです。 既定の作業ディレクトリは、現在の構成に応じて、\bin\Debug または \bin\Release です。|  
|**リモート コンピューターの使用**|このチェック ボックスがオンの場合、リモート デバッグは有効です。 テキスト ボックスには、デバッグ用にアプリケーションを実行するリモート コンピューターの名前または [Msvsmon サーバー名](https://msdn.microsoft.com/library/55b60ce7-834b-4e83-a10e-fe4248260a4c)を入力できます。 リモート コンピューター上の EXE ファイルの場所は、[ビルド] タブの [出力パス] プロパティで指定します。また、EXE ファイルがリモート コンピューターの共有ディレクトリにあることも必要です。|  
|**Unmanaged code debugging (アンマネージド コード デバッグ)**|マネージド アプリケーションからネイティブ (アンマネージド) Win32 コードの呼び出しをデバッグできます。 これは、[!INCLUDE[vcprvc](../includes/vcprvc-md.md)] プロジェクトで [デバッガーのタイプ] に [混合] を選択するのと同じ効果があります。|  
|**SQL Server デバッグ**|SQL Server データベース オブジェクトのデバッグを許可します。|  
  
### <a name="compile-tab-press-advanced-compile-options-button"></a>[コンパイル] タブ : [詳細コンパイル オプション] ボタンをクリックします。  
  
|設定|説明|  
|-------------|-----------------|  
|**最適化を有効にする**|このオプションはオフにしておくことをお勧めします。 最適化を有効にすると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] に表示されるソース コードとは異なるコードが実行されるため、デバッグが困難になります。 コードが最適化されている場合、"マイ コードのみ" でデバッグするときに、既定でシンボルが読み込まれません。|  
|**デバッグ情報を作成**|既定で、デバッグ バージョンとリリース バージョンの両方に定義されます。この設定 (/debug コンパイラ オプションに相当します) に基づいて、ビルド時にデバッグ情報が作成されます。 デバッガーでは、この情報を使って変数名やその他の情報を見やすい形式でデバッグ時に表示します。 この情報を設定せずにプログラムをコンパイルすると、デバッガーの機能は制限されます。 詳細については、「[/debug](https://msdn.microsoft.com/library/c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2)」を参照してください。|  
|**定数 DEBUG の定義**|このシンボルを定義すると、[Debug クラス](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx)の出力関数の条件付きコンパイルが可能になります。 このシンボルを定義すると、Debug クラスのメソッドは[出力ウィンドウ](../ide/reference/output-window.md)に出力を生成します。 このシンボルを定義しない場合、Debug クラスのメソッドはコンパイルされず、出力も生成されません。 このシンボルは、デバッグ バージョンに定義します。リリース バージョンには定義しません。 リリース バージョンにこのシンボルを定義すると、不要なコードのためにプログラムの実行速度が低下します。|  
|**定数 TRACE の定義**|このシンボルを定義すると、[Trace クラス](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)の出力関数の条件付きコンパイルが可能になります。 このシンボルを定義すると、Trace クラスのメソッドは[出力ウィンドウ](../ide/reference/output-window.md)に出力を生成します。 このシンボルを定義しない場合、Trace クラスのメソッドはコンパイルされず、出力も生成されません。 このシンボルは、既定で、デバッグ バージョンとリリース バージョンの両方に定義されます。|  
  
## <a name="see-also"></a>参照  
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
