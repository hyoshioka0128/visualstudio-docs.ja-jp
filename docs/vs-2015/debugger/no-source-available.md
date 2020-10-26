---
title: 使用できるソースはありません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.nosource
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- No Source Code Available for the Current Location dialog box
ms.assetid: ed0732bc-4b8c-490f-adb1-af06869a2a6b
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 69ea9c3a41f83b9c06dc18d6da1f859017f12ca5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697809"
---
# <a name="no-source-available"></a>使用できるソースはありません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

表示しようとしているコードのソース コードがプロジェクトに含まれていません。 原因として、 **[呼び出し履歴]** ウィンドウまたは **[スレッド]** ウィンドウで、ソース コードのないモジュールをダブルクリックしたことが考えられます。 デバッグは継続できますが、ソース ウィンドウを使ってブレークポイントを設定したり、この場所で他のアクションを実行したりすることはできません。 ブレークポイントを設定する必要があるときは、代わりに **[逆アセンブリ]** ウィンドウを使用します。  
  
 [ソリューション  プロパティ ページ] で、デバッガーがソース ファイルを検索するディレクトリを変更したり、選択されたソース ファイルをデバッガーが無視したりするように設定できます。 「[[デバッグ ソース ファイル] ([ソリューション プロパティ ページ] ダイアログ ボックス - [共通プロパティ])](../debugger/debug-source-files-common-properties-solution-property-pages-dialog-box.md)」を参照してください。  
  
 **[参照してソースを検索]**  
 このリンクをクリックすると、参照してソース コードを検索できるダイアログ ボックスが開きます。  
  
 **[逆アセンブルの表示]**  
 **[逆アセンブル]** ウィンドウを起動します。  
  
 **[見つからないソース ファイルには常に逆アセンブルを表示する]**  
 このオプションをオンにすると、利用できるソースがない場合に **[逆アセンブル] ウィンドウ**が自動的に表示されます。 この設定は、 **[オプション]** ダイアログ ボックス、 **[デバッグ]** カテゴリ、 **[全般]** ページで、 **[ソースがない場合は逆アセンブルの表示]** をオンまたはオフにすることによっても変更できます。  
  
## <a name="see-also"></a>参照  
 [[デバッグソースファイル] ([ソリューションプロパティページ] ダイアログボックス-[共通プロパティ])](../debugger/debug-source-files-common-properties-solution-property-pages-dialog-box.md)   
 [シンボル (.pdb) とソースファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [SOS.dll (SOS デバッガー拡張)](https://msdn.microsoft.com/library/9ac1b522-77ab-4cdc-852a-20fcdc9ae498)
