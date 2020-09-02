---
title: '方法: ネイティブフレームが [呼び出し履歴] ウィンドウに表示されない場合にマネージコードからステップアウトするMicrosoft Docs'
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
- SQL
- VB
- CSharp
- C++
helpviewer_keywords:
- Call Stack window, missing native frames
- code, managed code
- native frames
- stepping, out of managed code
- managed code, stepping out of
ms.assetid: 97cdd2a8-02a9-4a06-a5b1-c92b1e431979
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 63bd55fd254dd263540a9161e8579ea6600e97f1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690100"
---
# <a name="how-to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-window"></a>方法 : ネイティブ フレームが [呼び出し履歴] ウィンドウに見つからないときにマネージド コードからステップ アウトする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[呼び出し履歴]** ウィンドウで表示されないネイティブ フレームがあるコードでは、マネージド コードからステップ アウトすると、予期しない結果になる場合があります。 代替手段として、**ステップ アウト**ではなくブレークポイントを使用できます。  
  
> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-display"></a>呼び出し履歴にネイティブ フレームが表示されないときにマネージド コードからステップ アウトするには  
  
1. ネイティブ コード内で、マネージド コードの呼び出し後に位置ブレークポイントを設定します。  
  
2. **[デバッグ]** メニューの **[続行]** をクリックします。  
  
     マネージド呼び出しが完了すると、ネイティブ コードのブレークポイントで実行が停止します。  
  
## <a name="see-also"></a>参照  
 [方法: [呼び出し履歴] ウィンドウを使用する](../debugger/how-to-use-the-call-stack-window.md)
