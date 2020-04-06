---
title: デバッグ エンジン |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a4cb00796f8db23a43cd81a06d80d0fac40f075e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739066"
---
# <a name="debug-engine"></a>デバッグ エンジン
デバッグ エンジン (DE) は、インタプリタまたはオペレーティング システムと連携して、実行制御、ブレークポイント、式評価などのデバッグ サービスを提供します。 DE は、デバッグ中のプログラムの状態を監視する役割を担います。 これを実現するために、DE は、CPU から、またはランタイムによって提供される API から、サポートされているランタイムで使用できるすべてのメソッドを使用します。

 たとえば、共通言語ランタイム (CLR) は、ICorDebugXXX インターフェイスを通じて実行中のプログラムを監視するメカニズムを提供します。 CLR をサポートする DE は、デバッグ中のマネージ コード プログラムを追跡するのに適切な ICorDebugXXX インターフェイスを使用します。 その後、セッションのデバッグ マネージャー (SDM) に、状態の変更を通信[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。

> [!NOTE]
> デバッグ エンジンは、特定のランタイム、つまり、デバッグ対象のプログラムが実行されるシステムを対象とします。 CLR はマネージ コードのランタイムであり、Win32 ランタイムはネイティブ Windows アプリケーション用です。 作成した言語がこれら 2 つのランタイムのいずれかを対象とできる[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]場合は、必要なデバッグ エンジンが既に提供されています。 実装する必要があるのは、式エバリュエーターです。

## <a name="debug-engine-operation"></a>デバッグ エンジン操作
 監視サービスは DE インターフェイスを通じて実装され、デバッグ パッケージが異なる動作モード間で遷移する可能性があります。 詳細については、[操作モード](../../extensibility/debugger/operational-modes.md)を参照してください。 通常、実行時環境ごとに 1 つの DE 実装しかありません。

> [!NOTE]
> Transact-SQL と[!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)]の個別の DE 実装と、VBScript と[!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)]は、1 つの DE を共有します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグを有効にすると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグ エンジンは、シェルと同じプロセス内、またはデバッグ対象のプログラムと同じプロセスで実行できます。 後者の形式は、通常、デバッグ中のプロセスが実際にインタプリタの下で実行されているスクリプトであるときに発生します。 スクリプトを監視するには、デバッグ エンジンにインタープリタの詳しい知識が必要です。 この場合、インタプリタは実際にはランタイムです。デバッグ エンジンは、特定のランタイム実装用です。 さらに、単一の DE の実装は、プロセスとマシンの境界間で分割できます (リモート デバッグなど)。

 DE はデバッグ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]インターフェイスを公開します。 すべての通信は COM を介して行われます。 DE がインプロセス、アウトプロセス、または別のコンピューターにロードされているかどうかは、コンポーネントの通信には影響しません。

 DE は式エバリュエーター コンポーネントと連携して、その特定のランタイムの DE が式の構文を理解できるようにします。 また、デは、言語コンパイラによって生成されたシンボリック デバッグ情報にアクセスするシンボル ハンドラー コンポーネントと連携します。 詳細については、「[式エバリュエーター](../../extensibility/debugger/expression-evaluator.md) 」および[「シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
- [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)
- [シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)
