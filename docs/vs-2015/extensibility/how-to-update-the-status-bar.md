---
title: '方法: ステータスバーを更新する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - update status bar
ms.assetid: 7500c8a7-4913-4818-a88b-bfd1b9887cb6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1d48b07dd5e4fc1fe745e3669041884c1b8eacd9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703143"
---
# <a name="how-to-update-the-status-bar"></a>方法: ステータス バーを更新する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**ステータスバー**は、1つまたは複数のステータステキスト行またはインジケーターを含む多くのアプリケーションウィンドウの下部にあるコントロールバーです。  
  
### <a name="to-update-the-status-bar"></a>ステータスバーを更新するには  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>フォームビューやコードビューなど、エディターに用意されている個々のビューオブジェクト (docview) にを実装します。  
  
2. IDE がを呼び出すときに <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> 、のメソッドを呼び出して、 **ステータスバー** の情報を更新し <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> ます。  
  
    > [!NOTE]
    > IDE は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> ドキュメントウィンドウが最初にアクティブになったときにのみを呼び出します。 ドキュメントウィンドウがアクティブになっている残りの時間については、エディターの状態が変化したときに **ステータスバー** の情報を更新する必要があります。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 **ステータスバー**には、次の4つのフィールドがあります。  
  
- 状態テキスト  
  
- 進行状況バー  
  
- アニメーションアイコン  
  
- エディター情報  
  
  詳細については、「 [ステータスバー](https://msdn.microsoft.com/library/fcbc5029-1aab-4e14-adf7-419038a4935e)」を参照してください。  
  
  ドキュメントウィンドウがアクティブになると、IDE は自動的に <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> 実装のメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> ます。  
  
  VSPackage の実装者は、ステータスバーのステータステキストを更新します。 状態テキストフィールドがアイドル時に空のテキスト ("") に設定されている場合、IDE はこの文字列を "READY" にリセットします。  
  
## <a name="see-also"></a>参照  
 [ステータスバー](https://msdn.microsoft.com/library/fcbc5029-1aab-4e14-adf7-419038a4935e)
