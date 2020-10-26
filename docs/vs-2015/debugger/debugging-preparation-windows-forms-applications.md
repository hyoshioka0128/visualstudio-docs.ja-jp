---
title: 'デバッグの準備: Windows フォーム Applications |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
helpviewer_keywords:
- debugging Windows applications
- Windows applications, debugging
- debugging [Visual Studio], Windows applications
- debugging [J#], Windows applications
- debugging [C#], Windows applications
- debugging [Visual Basic], Windows applications
ms.assetid: 7092ee7f-8378-4def-aef8-1695bd97cf14
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5b11855fbd19dc464f92b4339684ef8346556c21
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691150"
---
# <a name="debugging-preparation-windows-forms-applications"></a>デバッグの準備: Windows フォーム アプリケーション
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows フォーム プロジェクト テンプレートは、Windows フォーム アプリケーションを作成します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、この種類のアプリケーションを簡単にデバッグできます。 詳細については、[Windows アプリケーション プロジェクトの作成](https://msdn.microsoft.com/b2f93fed-c635-4705-8d0e-cf079a264efa)に関するページを参照してください。  
  
 プロジェクト テンプレートを使用して Windows フォーム プロジェクトを作成する場合、デバッグ構成とリリース構成に必要な設定は [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によって自動的に作成されます。 この設定は必要に応じて変更できます。 これらの設定は、[ ** \<project name> プロパティページ**] ダイアログボックス (Visual Basic の **[マイプロジェクト**]) で変更できます。  
  
 詳細については、「[プロパティの推奨設定](../debugger/managed-debugging-recommended-property-settings.md)」を参照してください。  
  
 推奨される追加のプロパティ設定を次の表に示します。  
  
### <a name="configuration-properties-in-debug-tab"></a>[デバッグ] タブの構成プロパティ  
  
|**プロパティ名**|**設定**|  
|-----------------------|-----------------|  
|**開始動作**|ほとんどの場合、 **[スタート プロジェクト]** に設定します。 デバッグの開始時に他の実行可能ファイルを起動する場合 (通常は DLL をデバッグする場合) には、 **[外部プログラムの開始]** に設定します。|  
  
 Windows フォーム アプリケーションは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内から、または既に実行中のアプリケーションにアタッチすることによってデバッグできます。 アタッチの詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。  
  
### <a name="to-debug-a-c-f-or-visual-basic-windows-forms-application"></a>C#、F#、または Visual Basic の Windows フォーム アプリケーションをデバッグするには  
  
1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でプロジェクトを開きます。  
  
2. 必要に応じて、ブレークポイントを作成します。  
  
    Windows フォーム アプリケーションはイベント ドリブンであるため、ブレークポイントはイベント ハンドラー コード内またはイベント ハンドラー コードによって呼び出されるメソッド内に設定します。 ブレークポイントが配置される一般的なイベントは次のとおりです。  
  
   1. Click、Enter などのコントロールに関連付けられたイベント。  
  
   2. Load、Activated など、アプリケーションの起動またはシャットダウンに関連付けられたイベント。  
  
   3. フォーカス イベントと検証イベント。  
  
      詳細については、「[Windows フォーム内でのイベント ハンドラーの作成](https://msdn.microsoft.com/library/6514e530-c6b8-489c-a8d2-eda7b7072701)」を参照してください。  
  
3. **[デバッグ]** メニューの **[開始]** をクリックします。  
  
4. 「 [デバッガーの基本](../debugger/debugger-basics.md)」で説明されている手法を使用してデバッグします。  
  
## <a name="see-also"></a>参照  
 [マネージコードのデバッグ](../debugger/debugging-managed-code.md)   
 [C#、F #、および Visual Basic プロジェクトの種類](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [方法: デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)   
 [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [実行中のプロセスにアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Windows フォーム](https://msdn.microsoft.com/library/627df1e9-b254-41af-bbac-9a4f02810c54)
