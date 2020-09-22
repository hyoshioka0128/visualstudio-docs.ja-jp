---
title: '方法: エディットコンティニュを使用して中断モードで編集を適用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.variables.failededit
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
helpviewer_keywords:
- Edit and Continue [Visual Basic], applying edits in break mode
- break mode, applying code changes
- Edit and Continue, applying edits in break mode
- editing, break mode
- coding, editing in break mode
- code, editing in break mode
ms.assetid: 1eef7498-6a1f-4fba-8146-510adc6375c9
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5c04dc0ae6e5272d2544ad7436fa7ca516c9a022
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841592"
---
# <a name="how-to-apply-edits-in-break-mode-with-edit-and-continue"></a>方法 : エディット コンティニュの中断モード時に編集を適用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディット コンティニュを使用すると、中断モードでコードを編集した後、コードを停止したり再起動したりせずにデバッグを継続できます。  
  
 次のデバッグ シナリオでは、エディット コンティニュを使用できません。  
  
- 混合モードでの (ネイティブ/マネージ) デバッグ  
  
- SQL デバッグ  
  
- ワトソン博士のダンプのデバッグ。  
  
- 未処理の例外を受け取った後のコード編集 ( **[ハンドルされていない例外で呼び出し履歴をアンワインドする]** オプションがオンでない場合)  
  
- 埋め込まれたランタイム アプリケーションのデバッグ  
  
- [**デバッグ**] メニューの [**開始**] を使用してアプリケーションを実行するのではなく、[**アタッチ先] を**使用してアプリケーションをデバッグする。  
  
- 最適化されたコードのデバッグ  
  
- マネージド コードのデバッグ (デバッグ対象が 64 ビット アプリケーションである場合)。 エディット コンティニュを使用する場合は、デバッグ対象を x86 に設定する必要があります  ([_プロジェクト_の**プロパティ**]、[**コンパイル**] タブ、 **[コンパイラの詳細**設定])。  
  
- ビルド エラーによって新しいバージョンのビルドが失敗した後の旧バージョンのデバッグ  
  
### <a name="to-edit-code-in-break-mode"></a>中断モードでコードを編集するには  
  
1. 以下のいずれかの操作を行って中断モードに入ります。  
  
    - コードにブレークポイントを設定した後、 **[デバッグ]** メニューの **[デバッグ開始]** をクリックし、アプリケーションがブレークポイントにヒットするのを待ちます。  
  
         \- または -  
  
    - デバッグを開始し、 **[デバッグ]** メニューの **[すべて中断]** をクリックします。  
  
         \- または -  
  
    - 例外が発生した場合は、例外処理**アシスタント**で [**編集を有効にする**] を選択します。  
  
2. 必要かつ有効なコード変更を行います。  
  
     詳細については、「 [Visual Basic のエディットコンティニュでサポートされていない編集](../debugger/unsupported-edits-in-visual-basic-edit-and-continue.md)」を参照してください。  
  
    > [!NOTE]
    > エディット コンティニュで許可されないコード変更を行おうとすると、編集部分の下に紫の波線が表示され、タスク一覧にタスクが表示されます。 この場合、無効なコード変更を元に戻さない限り、コードの実行を続行できません。  
  
3. **[デバッグ]** メニューの **[続行]** をクリックして、コードの実行を再開します。  
  
     適用した編集がプロジェクトに取り込まれた状態でコードが実行されます。  
  
## <a name="see-also"></a>参照  
 [エディットコンティニュ Visual Basic でサポートされていない編集](../debugger/unsupported-edits-in-visual-basic-edit-and-continue.md)   
 [エディット コンティニュ (Visual Basic)](../debugger/edit-and-continue-visual-basic.md)
