---
title: '方法: エディット コンティニュを使用する (C#) | Microsoft Docs'
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
- Edit and Continue [C#], about Edit and Continue
ms.assetid: 40e136d8-a08c-43bd-b313-fb821c55eb3c
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 39137d5fe60a3c91c8fd3904e797eb83420a8f5d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841804"
---
# <a name="how-to-use-edit-and-continue-c"></a>方法: エディット コンティニュを使用する (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C# のエディット コンティニュを使用すると、デバッグ中に中断モードでコードに変更を加えることができます。 デバッグ セッションを停止したり再開したりしなくても、変更を適用できます。  
  
 エディットコンティニュは、中断モードで変更を行ったときに自動的に呼び出されます。次に、[ **続行**]、[ **ステップ**]、 **[次のステートメントの設定**] などのデバッガー実行コマンドを選択するか、デバッガーウィンドウで関数を評価します。  
  
> [!NOTE]
> Compact Framework、最適化されたコード、ネイティブ コードとマネージ コードの混合コード、または SQL Server の共通言語ランタイム (CLR: Common Language Runtime) との統合コードのデバッグ時は、エディット コンティニュはサポートされません。 これらのシナリオのいずれかでコード変更を適用しようとすると、エディット コンティニュがサポートされないことを説明するダイアログ ボックスが表示されます。  
  
### <a name="to-invoke-edit-and-continue-automatically"></a>エディット コンティニュを自動的に呼び出すには  
  
1. 中断モードで、ソース コードを変更します。  
  
2. [ **デバッグ** ] メニューの [ **続行**]、[ **ステップ**]、または [次の **ステートメントの設定** ] をクリックするか、デバッガーウィンドウで関数を評価します。  
  
     新しいコードがコンパイルされ、その新しいコードでデバッグが続行されます。 エディット コンティニュでサポートされない変更もあります。 詳細については、「 [サポートされているコードの変更 (C#)](../debugger/supported-code-changes-csharp.md)」を参照してください。  
  
### <a name="to-enabledisable-edit-and-continue"></a>[エディット コンティニュ] を有効または無効にするには  
  
1. **[ツール]** メニューの **[オプション]** をクリックします。  
  
2. [ **オプション** ] ダイアログボックスで、[ **デバッグ** ] ノードを展開し、[ **エディットコンティニュ**] を選択します。  
  
3. [ **オプション** ] ダイアログボックスの [ **エディットコンティニュ** ] ページで、[ **エディットコンティニュを有効にする** ] チェックボックスをオンまたはオフにします。  
  
     デバッグ セッションを再開すると、この設定が有効になります。  
  
## <a name="see-also"></a>参照  
 [エディットコンティニュ (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)   
 [サポートされているコード変更 (C#)](../debugger/supported-code-changes-csharp.md)   
 [エディットコンティニュのエラーと警告 (C#)](../misc/edit-and-continue-errors-and-warnings-csharp.md)
