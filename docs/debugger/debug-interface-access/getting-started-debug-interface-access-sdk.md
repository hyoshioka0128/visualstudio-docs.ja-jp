---
title: はじめに (Debug Interface Access SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- .dbg files
- DBG files
ms.assetid: cb3d040a-2846-40d7-bdbc-8a5beb5dd2f6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2dd6a98f377ba295d6a866c9db95671de4ff16ea
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745101"
---
# <a name="getting-started-debug-interface-access-sdk"></a>はじめに (Debug Interface Access SDK)
Debug Interface Access (DIA) SDK には、説明ドキュメントと、DIA API の使用方法を示すサンプルが用意されています。 DIA SDK のインターフェイスとメソッドを使用して、.pdb ファイルと dbg ファイルを開き、シンボル、値、属性、アドレス、その他のデバッグ情報の内容を検索するカスタムアプリケーションを開発します。 この SDK には、アプリケーションでC++見つかったシンボルに関連付けられたプロパティの参照テーブルも用意されています。

 DIA SDK を最適に使用するには、次のことを理解している必要があります。

- C++プログラミング言語

- COM プログラミング

- サンプルをコンパイルするための Visual Studio 統合開発環境 (IDE)

  DIA SDK は通常、Visual Studio と共にインストールされ、その既定の場所は *[drive] \ (* visual studio 9.0 \ DIA SDK) です。 インストールの一部として、DIA SDK を実装する msdia90 が自動的に登録されるため、使用するために必要なのは、プログラムに `dia2.h` を含め、`diaguids.lib` にリンクすることだけです。

  ヘッダー: include\dia2.h

  ライブラリ: lib\diaguids.lib

  DLL: bin\msdia80.dll

  IDL: idl\dia2.idl

## <a name="in-this-section"></a>このセクションの内容

[概要](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)

DIA の基本的なアーキテクチャを確認します。

[.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

DIA API を使用して .pdb ファイルのクエリを実行する手順について説明します。

## <a name="see-also"></a>関連項目

- [Debug Interface Access SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)