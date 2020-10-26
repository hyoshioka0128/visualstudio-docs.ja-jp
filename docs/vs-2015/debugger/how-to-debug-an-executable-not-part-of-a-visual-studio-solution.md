---
title: '方法: Visual Studio ソリューションの一部ではない実行可能ファイルをデバッグする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], executables
- executable files, importing
- executable files, debugging outside of projects
ms.assetid: 3ea176e8-1ce5-42c4-b7a2-abe3a2765033
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e33233fd313cd6a73013ce55333a860663ddb601
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704525"
---
# <a name="how-to-debug-an-executable-not-part-of-a-visual-studio-solution"></a>方法 : Visual Studio ソリューションに含まれていない実行可能ファイルをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトに含まれない実行可能ファイルをデバッグすることが必要な場合もあります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の外部で作成された実行可能ファイルや、他の人から受け取った実行可能ファイルなどがその例です。  
  
 この問題を解決するには、通常、Visual Studio 外部の実行可能ファイルを起動して、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デバッガーを使用してそのファイルにアタッチします。 詳細については、「[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)」を参照してください。  
  
 アプリケーションへのアタッチは、一部を手動で実行する必要があります。この処理には数秒かかります。 アプリケーションの起動時に発生する問題をデバッグする場合は、このわずかな遅延のため、アタッチが役に立ちません。 また、ユーザー入力を待たず、すぐに終了するプログラムをデバッグする場合は、アタッチしている時間がないこともあります。 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] がインストールされている場合は、このようなプログラムの EXE プロジェクトを作成できます。  
  
### <a name="to-create-an-exe-project-for-an-existing-executable"></a>既存の実行可能ファイルの EXE プロジェクトを作成するには  
  
1. [ **ファイル** ] メニューの [ **開く** ] をクリックし、[ **プロジェクト**] を選択します。  
  
2. [ **プロジェクトを開く** ] ダイアログボックスで、[ **ファイル名** ] ボックスの横にあるドロップダウンリストをクリックし、[ **すべてのプロジェクトファイル**] を選択します。  
  
3. 実行可能ファイルを見つけて、[ **OK]** をクリックします。  
  
     これにより、実行可能ファイルを格納する一時的なソリューションが作成されます。  
  
### <a name="to-import-an-executable-into-a-visual-studio-solution"></a>Visual Studio ソリューションに実行可能ファイルをインポートするには  
  
1. [ **ファイル** ] メニューの [ **プロジェクトの追加**] をポイントし、[ **既存のプロジェクト**] をクリックします。  
  
2. [ **既存のプロジェクトの追加** ] ダイアログボックスで、[ **ファイル名** ] ボックスの横にあるドロップダウンリストをクリックし、[ **すべてのプロジェクトファイル**] を選択します。  
  
3. 目的の実行可能ファイルを見つけ、選択します。  
  
4. **[OK]** をクリックします。  
  
5. [**デバッグ**] メニューの [**開始**] などの実行コマンドを選択して、実行可能ファイルを起動します。  
  
    > [!NOTE]
    > EXE プロジェクトをサポートしていないプログラミング言語もあります。 この機能を使用する必要がある場合は、[!INCLUDE[vcprvc](../includes/vcprvc-md.md)] をインストールしてください。  
  
     ソース コードなしで実行可能ファイルをデバッグする場合は、実行中の実行可能ファイルにアタッチするか、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションに実行可能ファイルを追加するかにかかわらず、利用できるデバッグ機能が限られます。 実行可能ファイルが、互換性のある形式のデバッグ情報を持たずにビルドされていた場合、利用できる機能はさらに限られます。 ソース コードがある場合は、そのソース コードを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] にインポートして、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で実行可能ファイルのデバッグ ビルドを作成するのが最適です。  
  
## <a name="see-also"></a>参照  
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [DBG ファイル](https://msdn.microsoft.com/91e449e9-8b65-4123-960f-2107cd1f1cfd)
