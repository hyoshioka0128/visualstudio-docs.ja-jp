---
title: '[エディットコンティニュエラーメッセージ] ダイアログボックス |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.ENC.SupportedButNotAvailable
- vs.debug.ENC.CannotEditWhileException
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue Error Message dialog box
ms.assetid: f98c91c0-447a-4533-85b6-87170a0dc4c3
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5437ef982309ef8595f08283f2685e93d346e764
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62428296"
---
# <a name="edit-and-continue-error-message-dialog-box"></a>エディット コンティニュ エラー メッセージ ダイアログ ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このダイアログボックスは、エディットコンティニュをサポートする言語でデバッグする場合に表示されますが、 **エディットコンティニュ** は、実行したコード変更の種類には使用できません。 ダイアログ ボックス内のエラー メッセージに、より詳しい説明が示されます。 このダイアログ ボックスが表示される原因としては、次のことが考えられます。  
  
- アンマネージド デバッグを有効にしているときに、マネージド コードを編集しようとした。 混合モード デバッグを実行している場合は、エディット コンティニュを使用できません。  
  
- SQL Server コードを編集しようとした。  
  
- ワトソン博士ダンプのデバッグ中にコードを編集しようとしました。  
  
- 未処理の例外が発生した後でコードを編集しようとしましたが、[ハンドルされていない**例外で呼び出し履歴をアンワインド**する] オプションが選択されていませんでした。  
  
- 埋め込まれたランタイム アプリケーションをデバッグしているときに、コードを編集しようとした。  
  
- [ **デバッグ** ] メニューから起動するのではなく、アタッチしたプログラムのコードを編集しようとしました。  
  
- 最適化されたコードを編集しようとした。  
  
- デバッグ対象が 64 ビット アプリケーションである場合に、マネージド コードをデバッグしようとした。 エディット コンティニュを使用する場合は、デバッグ対象を x86 に設定する必要があります  ([*プロジェクト*の **プロパティ**]、[ **コンパイル** ] タブ、 **[コンパイラの詳細** 設定])。  
  
- デバッグ中に変更され、再読み込みされたアセンブリのコードを編集しようとした。  
  
- 読み込まれていないアセンブリのコードを編集しようとした。  
  
- 新しいバージョンでビルド エラーが発生したため、古いバージョンでアプリケーションのデバッグを開始した。  
  
- 実行中のコードを編集しようとした。  
  
## <a name="uielement-list"></a>UIElement の一覧  
 **[OK]**  
 ダイアログ ボックスを閉じ、直前の編集操作をキャンセルします。  
  
## <a name="see-also"></a>参照  
 [サポートされているコード変更 (C++)](../debugger/supported-code-changes-cpp.md)
