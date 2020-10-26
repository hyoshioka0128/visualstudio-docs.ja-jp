---
title: '方法: ネイティブ Dll をデバッグする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.dll
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging DLLs
- DLLs, debugging
- executable files, specifying for debug sessions
ms.assetid: 76b34d15-a66d-4963-842e-c8b955c81696
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 16a533b27e619526edab71374d922e68baf0a4b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702679"
---
# <a name="how-to-debug-native-dlls"></a>方法: ネイティブ DLL サーバーをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
 DLL をデバッグするときには、次のプロジェクトからデバッグを開始できます。  
  
- DLL を呼び出す実行可能ファイルの作成に使用したプロジェクト  
  
  \- または  
  
- DLL 自身を作成するのに使用したプロジェクト  
  
  実行可能ファイルの作成に使用したプロジェクトがある場合は、そのプロジェクトからデバッグを開始します。 実行可能ファイルの作成に使用したプロジェクトに含まれていない DLL でも、そのソース ファイルを開いてブレークポイントを設定できます。 詳細については、「[ブレークポイント](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583)」を参照してください。  
  
  DLL を作成したプロジェクトからデバッグを開始する場合は、DLL のデバッグに使用する実行可能ファイルを指定する必要があります。  
  
### <a name="to-specify-an-executable-for-the-debug-session"></a>デバッグ セッション用の実行可能ファイルを指定するには  
  
1. [ **ソリューションエクスプローラー**で、DLL を作成するプロジェクトを選択します。  
  
2. [ **表示** ] メニューの [**プロパティページ**] をクリックします。  
  
3. [ **プロパティページ** ] ダイアログボックスで、[ **構成プロパティ** ] フォルダーを開き、[ **デバッグ** ] カテゴリを選択します。  
  
4. [ **コマンド** ] ボックスで、コンテナーのパス名を指定します。 たとえば、「C:\Program Files\MyApplication\MYAPP.EXE」のように指定します。  
  
5. [ **コマンド引数** ] ボックスに、実行可能ファイルに必要な引数を指定します。  
  
   [_プロジェクト_の**プロパティページ**] ダイアログボックスで実行可能ファイルを指定しない場合、デバッグを開始すると、[[デバッグセッションの実行可能ファイル] ダイアログボックス](../debugger/executable-for-debugging-session-dialog-box.md)が表示されます。  
  
## <a name="see-also"></a>参照  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)
