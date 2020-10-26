---
title: '方法: プログラムのクラッシュが発生している DLL を確認する | Microsoft Docs'
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
- debugger, DLL crashes
- Module List dialog box
- errors [debugger], DLL crashes
- Modules window
- debugging [Visual Studio], DLL crashes
- DLLs, load order of
ms.assetid: ecf62568-8b65-4a41-b8a4-e962ff2dfb71
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 44ebe042ff6e2507530e4be410e768550e922b44
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703628"
---
# <a name="how-to-find-which-dll-your-program-crashed-in"></a>方法 : プログラムのクラッシュが発生している DLL を確認する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注意]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
 システム DLL または他の開発者が作成したコードを呼び出す部分でアプリケーションがクラッシュした場合、クラッシュが発生した DLL を確認する必要があります。 プログラム外の DLL でクラッシュが発生している場合は、 **[モジュール]** ウィンドウを使用してその場所を確認できます。  
  
### <a name="to-find-where-a-crash-occurred-using-the-modules-window"></a>[モジュール] ウィンドウを使ってクラッシュの発生場所を確認するには  
  
1. クラッシュが発生したアドレスをメモします。  
  
2. **[デバッグ]** メニューの **[ウィンドウ]** をポイントし、 **[モジュール]** をクリックします。  
  
3. **[モジュール]** ウィンドウの **[アドレス]** 列に注目します。 必要に応じて、スクロール バーを使用します。  
  
4. 列の上部にある **[アドレス]** ボタンをクリックして、DLL をアドレス順に並べ替えます。  
  
5. 並べ替えたリストを検索して、アドレス範囲内にクラッシュ場所がある DLL を探します。  
  
6. **[名前]** 列と **[パス]** 列で、DLL の名前とパスを確認します。  
  
## <a name="see-also"></a>参照  
 [方法: ネイティブ Dll をデバッグする](../debugger/how-to-debug-native-dlls.md)   
 [方法: [モジュール] ウィンドウを使用する](../debugger/how-to-use-the-modules-window.md)
