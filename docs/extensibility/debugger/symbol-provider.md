---
title: シンボルプロバイダー |Microsoft Docs
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
ms.openlocfilehash: 31b90846d9494ee046cf9dc4a3e5de9ff033ea3f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712821"
---
# <a name="symbol-provider"></a>シンボルプロバイダー
式エバリュエーターの実装は、変数と式を評価するために、言語コンパイラによって生成されるシンボリックデバッグ情報にアクセスする必要があります。 これを行うには、シンボルプロバイダー (SP) のインターフェイスを使用します。これは、シンボルハンドラーとも呼ばれます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] マネージコード用の Sp と、プログラムデータベース (PDB) シンボルファイル形式を使用するネイティブコードを提供します。 カスタム形式で格納されているシンボルをプログラムで使用する必要がある場合を除き、によって提供される SPs を使用することをお勧め [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

## <a name="implementation-notes"></a>実装に関するメモ
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグエンジンは、共通言語ランタイム (CLR) インターフェイスを使用して SPs と通信することを想定しています。 そのため、Visual Studio デバッグエンジンで動作する SP は、CLR をサポートしている必要があります。 すべての CLR デバッグインターフェイスの完全な一覧については、「」の一部である debugref.doc を参照 [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] してください。

 SP がカスタムデバッグエンジンでのみ動作する場合は、デバッグエンジンのニーズに応じて、必要に応じて SP を実装できます。

## <a name="see-also"></a>関連項目
- [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)
