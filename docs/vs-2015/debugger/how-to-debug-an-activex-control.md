---
title: '方法: ActiveX コントロールをデバッグする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vc.controls.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- testing [Visual Studio], test containers
- ActiveX control container debugging [Visual Studio]
- debugging ActiveX controls
- data-bound controls, ActiveX
- test container
- containers, specifying for debug sessions
- ActiveX controls, debugging
- testing [Visual Studio], ActiveX controls
ms.assetid: bbc02cf7-a7e6-44fe-99af-87a43e1d7251
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9524ab08ab955609f29f437e8a1576af02738aa1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704461"
---
# <a name="how-to-debug-an-activex-control"></a>方法: ActiveX コントロールをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注意]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
 ActiveX コントロールをデバッグするには、そのコントロールが実行されるコンテナー (実行可能ファイル) を指定する必要があります。  
  
### <a name="to-specify-a-container-for-the-debug-session"></a>デバッグ セッションのコンテナーを指定するには  
  
1. ソリューション エクスプローラーでプロジェクトを選択します。  
  
2. **[表示]** メニューの **[プロパティ ページ]** をクリックします。  
  
3. **[プロジェクト プロパティ ページ]** ダイアログ ボックスで、 **[構成プロパティ]** フォルダーを開き、 **[デバッグ]** を選択します。  
  
4. **[デバッグ]** カテゴリの **[コマンド]** プロパティを探します。  
  
5. コンテナーのパス名を指定します。 たとえば、「C:\Program Files\Internet Explorer\IEXPLORE.EXE」のように指定します。  
  
6. Internet Explorer をコンテナーとして指定し、アクティブ デスクトップを使用している場合は、 **[コマンド引数]** ボックスに「`/new`」と入力します。  
  
7. **[OK]** をクリックします。  
  
     **[プロジェクト プロパティ ページ]** ダイアログ ボックスでコンテナーを指定しなかった場合でも、デバッグを開始するときにコンテナーを指定できます。 実行コマンドを選択してデバッグを開始するときに、[[デバッグ セッションで実行可能] ダイアログ ボックス](../debugger/executable-for-debugging-session-dialog-box.md)が表示されます。 ダイアログ ボックスにコンテナーのパス名を指定します。  
  
## <a name="see-also"></a>参照  
 [ActiveX コントロール](https://msdn.microsoft.com/library/52aaec4d-3889-402e-b57d-758078f8ac57)   
 [テストコンテナーでのプロパティとイベントのテスト](https://msdn.microsoft.com/library/626867cf-fe53-4c30-8973-55bb93ef3917)   
 [COM および ActiveX のデバッグ](../debugger/com-and-activex-debugging.md)   
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)
