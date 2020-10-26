---
title: エンコーディングと改行 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.Encoding
helpviewer_keywords:
- line breaks
- encoding
- Visual Studio, encoding
- editors, line breaks
- line break characters
- Visual Studio, line break characters
ms.assetid: 8f9b3ffc-7b8d-44f4-87cb-dc29105be12d
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2e1b13cc101ea4d7609633fd9c11bf87946d7b7d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665735"
---
# <a name="encodings-and-line-breaks"></a>エンコーディングと改行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、[ファイル] メニューの **[保存オプションの詳細設定]** を使用して、必要な改行の種類を決定できます。 また、同じ設定でファイルのエンコーディングを変更することもできます。

> [!NOTE]
> 開発設定の種類によっては (Visual Basic、F#、Web 開発)、メニューに **[保存オプションの詳細設定]** が表示されない場合があります。 設定を (たとえば [全般] に) 変更するには、**[ツール] から [設定のインポートとエクスポート]** を開きます。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

 Visual Studio では、次の文字が改行として解釈されます。

- CRLF: キャリッジ リターン文字とライン フィード文字 (Unicode 文字では 000D + 000A)

- LF: ライン フィード文字 (Unicode 文字では 000A)

- NEL: 次行記号 (Unicode 文字では 0085)

- LS: 行区切り記号 (Unicode 文字では 2028)

- PS: 段落区切り記号 (Unicode 文字では 2029)

  他のアプリケーションからコピーされたテキストでは、元のエンコーディングと改行文字が保持されます。 たとえば、メモ帳からテキストをコピーし、Visual Studio でテキスト ファイルに貼り付けた場合、貼り付けたテキストの設定は、メモ帳で使用していた設定と同じになります。

  改行文字が異なるファイルを開くと、一致しない改行文字を正規化するかどうか、また、どの種類の改行を使用するかを確認するダイアログ ボックスが表示される場合があります。
