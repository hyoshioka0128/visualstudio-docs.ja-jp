---
title: 使用できるソースはありません | Microsoft Docs
description: ご利用のプロジェクトに、表示したいコードのソース コードが含まれていない場合の対処方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.nosource
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- No Source Code Available for the Current Location dialog box
ms.assetid: ed0732bc-4b8c-490f-adb1-af06869a2a6b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e9993c4482d20393a3ca46d9afcd0a8ec1b13f65
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942036"
---
# <a name="no-source-available"></a>使用できるソースはありません
表示しようとしているコードのソース コードがプロジェクトに含まれていません。 原因として、 **[呼び出し履歴]** ウィンドウまたは **[スレッド]** ウィンドウで、ソース コードのないモジュールをダブルクリックしたことが考えられます。 デバッグは継続できますが、ソース ウィンドウを使ってブレークポイントを設定したり、この場所で他のアクションを実行したりすることはできません。 ブレークポイントを設定する必要があるときは、代わりに **[逆アセンブリ]** ウィンドウを使用します。

 [ソリューション  プロパティ ページ] で、デバッガーがソース ファイルを検索するディレクトリを変更したり、選択されたソース ファイルをデバッガーが無視したりするように設定できます。 「[[デバッグ ソース ファイル] ([ソリューション プロパティ ページ] ダイアログ ボックス - [共通プロパティ])](../debugger/debug-source-files-common-properties-solution-property-pages-dialog-box.md)」を参照してください。

 **参照してソースを検索**: このリンクをクリックすると、参照してソース コードを検索できるダイアログ ボックスが開きます。

 **逆アセンブリの表示**: **[逆アセンブリ] ウィンドウ** を起動します。

 **見つからないソース ファイルには常に逆アセンブルを表示する**: 利用できるソースがない場合に **[逆アセンブリ] ウィンドウ** を自動的に表示するには、このオプションをオンにします。 この設定は、 **[オプション]** ダイアログ ボックス、 **[デバッグ]** カテゴリ、 **[全般]** ページで、 **[ソースがない場合は逆アセンブルの表示]** をオンまたはオフにすることによっても変更できます。

## <a name="see-also"></a>関連項目
- [[デバッグ ソース ファイル] ([ソリューション プロパティ ページ] ダイアログ ボックス - [共通プロパティ])](../debugger/debug-source-files-common-properties-solution-property-pages-dialog-box.md)
- [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [SOS.dll (SOS デバッガー拡張)](/dotnet/framework/tools/sos-dll-sos-debugging-extension)