---
title: '方法: エディットコンティニュを有効または無効にする |Microsoft Docs'
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
- /INCREMENTAL linker option
- Apply Code Changes command
- Edit and Continue, disabling
- code changes, applying in break mode
- INCREMENTAL linker option
- Edit and Continue, enabling
- break mode, applying code changes
- Edit and Continue, applying code changes
- Step command
- Go command
ms.assetid: fd961a1c-76fa-420d-ad8f-c1a6c003b0db
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 70914da9be4046589a0ca3b8e5fd4ae13210ca51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65689263"
---
# <a name="how-to-enable-and-disable-edit-and-continue"></a>方法 : エディット コンティニュを有効および無効にする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デザイン時には、[ **オプション** ] ダイアログボックスでエディットコンティニュを無効にするか、有効にすることができます。 デバッグの最中にこの設定を変更することはできません。  
  
 エディット コンティニュはデバッグ ビルドでのみ動作します。 ネイティブ C++ については、エディット コンティニュで /INCREMENTAL オプションを使用する必要があります。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-enabledisable-edit-and-continue"></a>[エディット コンティニュ] を有効または無効にするには  
  
1. デバッグオプションページを開きます ([**ツール]/[オプション]/[デバッグ**])。  
  
2. 下にスクロール **して [エディットコンティニュ** ] カテゴリに移動します。  
  
3. 有効にするには、[ **エディットコンティニュを有効** にする] チェックボックスをオンにします。 無効にするには、このチェック ボックスをオフにします。  
  
   > [!NOTE]
   > IntelliTrace が有効になっている場合に、IntelliTrace イベントと呼び出し情報の両方を収集すると、エディット コンティニュが無効になります。 詳細については、「 [Configure IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)」を参照してください。  
  
4. **[OK]** をクリックします。  
  
   これらのオプションの詳細については、「 [[全般] ([オプション] ダイアログボックス](../debugger/general-debugging-options-dialog-box.md)-[デバッグ])」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エディット コンティニュ](../debugger/edit-and-continue.md)
