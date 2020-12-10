---
title: シンボルプロバイダー |Microsoft Docs
description: 式エバリュエーターが変数と式を評価できるように、Visual Studio に用意されているシンボルプロバイダーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 043014ebababd990c9cae03f28cb1b642d576071
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996046"
---
# <a name="symbol-provider"></a>シンボルプロバイダー
式エバリュエーターの実装は、変数と式を評価するために、言語コンパイラによって生成されるシンボリックデバッグ情報にアクセスする必要があります。 これを行うには、シンボルプロバイダー (SP) のインターフェイスを使用します。これは、シンボルハンドラーとも呼ばれます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] マネージコード用の Sp と、プログラムデータベース (PDB) シンボルファイル形式を使用するネイティブコードを提供します。 カスタム形式で格納されているシンボルをプログラムで使用する必要がある場合を除き、によって提供される SPs を使用することをお勧め [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

## <a name="implementation-notes"></a>実装に関するメモ
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグエンジンは、共通言語ランタイム (CLR) インターフェイスを使用して SPs と通信することを想定しています。 そのため、Visual Studio デバッグエンジンで動作する SP は、CLR をサポートしている必要があります。 すべての CLR デバッグインターフェイスの完全な一覧については、「」の一部である debugref.doc を参照 [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] してください。

 SP がカスタムデバッグエンジンでのみ動作する場合は、デバッグエンジンのニーズに応じて、必要に応じて SP を実装できます。

## <a name="see-also"></a>こちらもご覧ください
- [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)
