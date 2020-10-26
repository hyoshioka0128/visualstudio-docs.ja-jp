---
title: '方法: メニュー項目を使用して警告を非表示にする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- warnings, suppressing
- code analysis, suppressing warnings
ms.assetid: 36bd1850-dcde-4ed0-9bc3-0b83df434362
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 96b7433ff4f696989142aa2c2ce47982006b93b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72610012"
---
# <a name="how-to-suppress-warnings-by-using-the-menu-item"></a>方法: メニュー項目を使用して警告を抑制する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注意]
> ソース内の抑制は、web サイトプロジェクトではサポートされていません。

 [コード分析] ウィンドウを使用すると、コード分析の警告を非表示にすることができます。 警告を抑制することは、警告を無効にすることと同じではありません。 警告を非表示にすると、違反の特定のインスタンスにのみ適用されます。 同じ警告のその他の違反は、引き続きエラー一覧ウィンドウに報告されます。

 コード分析を実行した後、[コード分析] ウィンドウに表示されている1つ以上のコード分析警告がアプリケーションに適用できないことがわかります。 たとえば、コードが正しいと判断したとします。 また、一部の違反が優先度が低く、現在の開発サイクルでは修正されない場合もあります。 理由に関係なく、多くの場合、警告が適用されないことを示すと便利です。これは、コードのレビューが行われたこと、および警告が抑制される可能性があると判断されたことをチームメンバーに知らせるためです。 では、警告が生成される場所の近くに抑制を配置できるため、ソースの抑制が役立ちます。

 抑制をソースコードまたはグローバル抑制ファイルのどちらに表示するかを選択できます。 一部の抑制は、グローバル抑制ファイルに配置する必要があります。 この場合、[ **ソース内** ] オプションは無効になります。

### <a name="to-suppress-a-warning-by-using-menu-item"></a>メニュー項目を使用して警告を抑制するには

1. [ **分析** ] メニューで、[ **Windows** ]、[ **コード分析**] の順に選択します。

2. [ **コード分析** ] ウィンドウで、[警告を抑制する] を選択します。

3. [アクション] を選択し、[ **メッセージの非**表示] を選択してから、[ **ソース内** ] または [ **プロジェクト抑制ファイル内**] を選択します。

     特定の警告が抑制され、[コード分析] ウィンドウに取り消し線付きで警告が表示されます。

> [!NOTE]
> ターゲットを持たない抑制は、グローバル抑制ファイルに表示されます。
