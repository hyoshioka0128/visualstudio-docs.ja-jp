---
title: '方法: DLL プロジェクトからデバッグする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- DLL projects, debugging
- debugging DLLs
- DLLs, debugging projects
- debugging [Visual Studio], DLLs
ms.assetid: 40a94339-d3f7-4ab9-b8a1-b8cf82942f44
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6496d38e753d2338966916d1d7855abca77ace34
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842017"
---
# <a name="how-to-debug-from-a-dll-project"></a>方法 : DLL プロジェクトからデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DLL プロジェクトのデバッグを開始するには、プロジェクトのプロパティで呼び出し元のアプリケーションを指定する必要があります。 C++ のプロパティ ページは、C# と Visual Basic のプロパティ ページとレイアウトおよび内容が異なります。  
  
 マネージド DLL がネイティブ コードによって呼び出され、両方をデバッグする場合は、このプロジェクトのプロパティで指定できます。 詳細については、「 [方法: 混合モードでデバッグ](../debugger/how-to-debug-in-mixed-mode.md)する」を参照してください。  
  
> [!NOTE]
> Visual Studio の Express Edition では、外部の呼び出し元アプリケーションを指定できません。 代わりに、実行可能なプロジェクトをソリューションに追加することが必要です。次に、これをスタートアップ プロジェクトとして設定し、実行可能なプロジェクトから DLL のメソッドを呼び出します。  
  
### <a name="to-specify-the-calling-application-in-a-c-project"></a>C++ プロジェクトで呼び出し元のアプリケーションを指定するには  
  
1. **ソリューションエクスプローラー**でプロジェクトノードを右クリックし、[**プロパティ**] を選択します。 [ **デバッグ** ] タブにアクセスします。  
  
2. ウィンドウの上部にある **[構成]** フィールドが **[デバッグ]** に設定されていることを確認します。  
  
3. [ **構成プロパティ]、[デバッグ**] の順に進んでください。  
  
4. [ **起動するデバッガー** ] ボックスの一覧で、[ **ローカル windows デバッガー** ] または [ **リモート windows デバッガー**] を選択します。  
  
5. [ **コマンド** ] または [ **リモートコマンド** ] ボックスに、アプリケーションの完全修飾パス名を追加します。  
  
6. **[コマンド引数]** ボックスに、任意の必要なプログラム引数を追加します。  
  
### <a name="to-specify-the-calling-application-in-a-c-or-visual-basic-project"></a>C# または Visual Basic のプロジェクトで呼び出し元のアプリケーションを指定するには  
  
1. **ソリューションエクスプローラー**でプロジェクトノードを右クリックし、[**プロパティ**] を選択します。 [ **デバッグ** ] タブにアクセスします。  
  
     [ **外部プログラムの開始**] を選択し、実行するプログラムの完全修飾パス名を追加します。  
  
     外部プログラムのコマンドライン引数を追加する必要がある場合は、[ **コマンドライン引数** ] フィールドに追加します。  
  
2. URL としてアプリケーションを呼び出すこともできます。 ローカル ASP.NET アプリケーションが使用するマネージド DLL をデバッグする場合は、この手順を実行します。  
  
     [ **開始アクション**] で、[ **ブラウザーを開始する url** ] オプションボタンを選択し、url を入力します。  
  
### <a name="to-start-debugging-from-the-dll-project"></a>DLL プロジェクトからデバッグを開始するには  
  
1. 必要に応じてブレークポイントを設定します。  
  
2. デバッグを開始します (F5 キーを押すか、緑色の矢印をクリックするか、[ **デバッグ]/[デバッグの開始**] をクリックします)。  
  
## <a name="see-also"></a>参照  
 [DLL プロジェクトのデバッグ](../debugger/debugging-dll-projects.md)   
 [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
