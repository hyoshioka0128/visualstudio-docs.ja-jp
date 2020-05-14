---
title: シンボルプロバイダー |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712821"
---
# <a name="symbol-provider"></a>シンボル プロバイダー
式エバリュエーターの実装は、変数と式を評価するために、言語コンパイラによって生成されたシンボリック デバッグ情報にアクセスする必要があります。 これは、シンボル・ハンドラーとも呼ばれるシンボル・プロバイダー (SP) のインターフェースを使用することによって行われます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、プログラムのデータ ベース (PDB) シンボル ファイル形式を使用して、マネージ コードとネイティブ コードの SP を提供します。 プログラムでカスタム形式で保存されたシンボルを使用する必要が強い場合を除き、 によって[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供される SP を使用することをお勧めします。

## <a name="implementation-notes"></a>実装に関するメモ
 デバッグ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]エンジンは、共通言語ランタイム (CLR) インターフェイスを使用して SP と対話することを期待します。 その結果、Visual Studio のデバッグ エンジンで動作する SP が CLR をサポートしている必要があります。 すべての CLR デバッグ インターフェイスの完全な一覧は、 の一部である debugref.doc にあります[!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)]。

 SP がカスタム デバッグ エンジンでのみ動作する場合は、デバッグ エンジンのニーズに応じて、SP を適切に実装できます。

## <a name="see-also"></a>関連項目
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
