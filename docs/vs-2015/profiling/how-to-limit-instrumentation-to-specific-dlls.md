---
title: '方法: インストルメンテーションを特定の DLL に制限する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, runtime profiling control window
ms.assetid: 17c5996f-e3d0-4e44-b175-52b401b0f2d5
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5dc2fe8e6f9b0ed1e6970943ab5eedf1b62eb961
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841813"
---
# <a name="how-to-limit-instrumentation-to-specific-dlls"></a>方法 : インストルメンテーションを特定の DLL に制限する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

インストルメンテーション プロファイリング方式を使用すると、プロファイリング データの収集をアプリケーションの 1 つ以上の DLL に制限することができます。 アプリケーションの 1 つ以上の DLL をプロファイルするには、ターゲットとして .dll ファイルを含むパフォーマンス セッションを作成します。 プロファイルする DLL は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションのプロジェクトとしてまたは独立したバイナリ ファイルとして指定できます。  
  
### <a name="to-limit-instrumentation-to-specific-dlls-in-a-visual-studio-solution"></a>インストルメンテーションを Visual Studio ソリューションの特定の DLL に制限するには  
  
1. [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] で DLL を含むソリューションを開きます。  
  
2. **[分析]** メニューの **[パフォーマンス ウィザードの起動]** を選択します。  
  
3. プロファイリング方式として **[インストルメンテーション]** を選択し、 **[次へ]** をクリックします。  
  
4. [ **次の使用可能なターゲットからプロファイルするターゲット**を選択してください] で、.dll プロジェクトの名前を選択し、[ **次へ**] をクリックします。  
  
5. **[完了]** をクリックしてウィザードを終了すると、 **[パフォーマンス エクスプローラー]** ウィンドウに新しいパフォーマンス セッションが表示されます。  
  
6. **[ターゲット]** を右クリックして **[ターゲット プロジェクトの追加]** を選択します。  
  
7. **[ターゲット プロジェクトの追加]** リストで、DLL を実行するために使用する実行可能なプロジェクトを選択します。  
  
     任意。 プロファイルする DLL プロジェクトはいくつでも追加できます。  
  
8. 追加されたプロジェクトのデータ収集を回避するには、プロジェクトの名前を右クリックし、 **[インストルメント]** チェック ボックスをオフにします。  
  
### <a name="to-specify-specific-dlls-to-profile-as-independent-binaries"></a>プロファイルする特定の DLL を独立したバイナリとして指定するには  
  
1. [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]を開きます。  
  
2. **[分析]** メニューの **[パフォーマンス ウィザードの起動]** を選択します。  
  
3. **[次の使用可能なターゲットからプロファイルするターゲットを選択]** で **[ダイナミック リンク ライブラリ (.DLL) のプロファイル]** を選択して、 **[次へ]** をクリックします。  
  
4. ウィザードの 2 ページ目で次の手順を実行します。  
  
    - **Dll パス**にプロファイルする .dll ファイルのパスとファイル名を入力します。 省略記号ボタン (...) をクリックして、 **[プロファイルするダイナミック リンク ライブラリ]** ダイアログ ボックスでファイルを指定することもできます。 次の手順で選択する実行可能 (.exe) ファイルによって起動される .dll ファイルのコピーを指定する必要があることにご注意ください。  
  
    - 実行可能ファイルのパスとファイル名を入力します。このファイルは、.exe ファイルを **実行**します。 省略記号ボタン (...) をクリックして、 **[起動する実行可能ファイル]** ダイアログ ボックスでファイルを指定することもできます。  
  
    - 任意。 実行可能ファイルに渡すコマンド ライン引数があれば、 **[コマンド ライン引数]** に入力します。 必要に応じて、アプリケーションの作業ディレクトリを **[作業ディレクトリ]** に指定します。  
  
    - **[次へ]** をクリックします。  
  
5. プロファイリング方式として **[インストルメンテーション]** を選択し、 **[次へ]** をクリックします。  
  
6. **[完了]** をクリックしてウィザードを終了すると、 **[パフォーマンス エクスプローラー]** ウィンドウに新しいパフォーマンス セッションが表示されます。  
  
7. 任意。 .Dll ファイルを追加するには、[ **ターゲット** ] を右クリックし、[ **ターゲットバイナリの追加**] を選択します。 **[ターゲット バイナリの追加]** ダイアログ ボックスからファイルを選択します。  
  
    > [!NOTE]
    > DLL を実行する実行可能 (.exe) ファイルは指定しないでください。  
  
## <a name="see-also"></a>参照  
 [データコレクションの制御](../profiling/controlling-data-collection.md)   
 [方法: インストルメンテーションを特定の関数に制限する](../profiling/how-to-limit-instrumentation-to-specific-functions.md)
