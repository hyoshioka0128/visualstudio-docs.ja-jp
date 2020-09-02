---
title: Debug Interface Access SDK |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging [DIA SDK]
- debugger [DIA SDK]
- DIA SDK
ms.assetid: 4c0abe53-11d3-4b7a-bdc7-b054f85aaf40
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ddaea95bc879364de99c0ec01213cda30fa4e7d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197619"
---
# <a name="debug-interface-access-sdk"></a>Debug Interface Access SDK
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Microsoft debug Interface Access Software Development Kit (DIA SDK) を使用すると、microsoft ポストコンパイラ tools によって生成されたプログラムデータベース (.pdb) ファイルに格納されているデバッグ情報にアクセスできます。 ポストコンパイラツールによって生成される .pdb ファイルの形式は定数リビジョンであるため、形式の公開は現実的ではありません。 DIA API を使用すると、.pdb ファイルに格納されているデバッグ情報を検索および参照するアプリケーションを開発できます。 このようなアプリケーションでは、レポートスタックのトレースバック情報や、パフォーマンスデータの分析などを行うことができます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [はじめに](../../debugger/debug-interface-access/getting-started-debug-interface-access-sdk.md)  
 DIA SDK 機能の概要について説明し、DIA SDK がインストールされる場所、および必要なヘッダーファイルとライブラリファイルを示します。  
  
 [.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)  
 DIA API を使用して .pdb ファイルのクエリを実行する方法について説明します。  
  
 [シンボルとシンボル タグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)  
 DIA API でのシンボルおよびシンボルタグの使用方法について説明します。  
  
 [リファレンス](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)  
 DIA API のインターフェイス、メソッド、列挙型、および構造体が含まれています。  
  
 [Dia2dump サンプル](../../debugger/debug-interface-access/dia2dump-sample.md)  
 DIA API を使用してデバッグ情報を検索および参照する方法について説明します。  
  
 [Dia2dump.cpp ソース ファイル](../../debugger/debug-interface-access/dia2dump-cpp-source-file.md)  
 DIA API を示すために [Dia2dump サンプル](../../debugger/debug-interface-access/dia2dump-sample.md) で使用されるソースコード。
