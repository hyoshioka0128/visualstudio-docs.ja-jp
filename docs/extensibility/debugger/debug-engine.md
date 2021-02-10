---
title: デバッグエンジン |Microsoft Docs
description: 実行制御、ブレークポイント、式の評価などのサービスを提供するために、インタープリターまたはオペレーティングシステムでデバッグエンジンがどのように機能するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9e278b83e69a063c88b4cb3ff48d919d2b07ea6a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955165"
---
# <a name="debug-engine"></a>デバッグエンジン
デバッグエンジン (DE) はインタープリターやオペレーティングシステムと連携して、実行制御、ブレークポイント、式の評価などのデバッグサービスを提供します。 DE は、デバッグ中のプログラムの状態を監視する役割を担います。 これを実現するために、DE は、サポートされているランタイムで使用可能な任意のメソッド (CPU から、またはランタイムによって提供される Api) を使用します。

 たとえば、共通言語ランタイム (CLR) は、実行中のプログラムをコンポーネントのインターフェイスで監視するメカニズムを提供します。 CLR をサポートする DE は、適切なツールのインターフェイスを使用して、デバッグされているマネージコードプログラムを追跡します。 次に、状態の変更をセッションデバッグマネージャー (SDM) に伝達します。これにより、このような情報が IDE に転送さ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] れます。

> [!NOTE]
> デバッグエンジンは、特定のランタイム (デバッグ対象のプログラムが実行されるシステム) を対象とします。 CLR はマネージコードのランタイムであり、Win32 ランタイムはネイティブ Windows アプリケーション用です。 作成した言語がこれら2つのランタイムのいずれかを対象とする場合は、に [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必要なデバッグエンジンが既に用意されています。 実装する必要があるのは、式エバリュエーターだけです。

## <a name="debug-engine-operation"></a>デバッグエンジンの操作
 監視サービスは、DE インターフェイスによって実装され、デバッグパッケージが異なる動作モード間で移行する可能性があります。 詳細については、「 [操作モード](../../extensibility/debugger/operational-modes.md)」を参照してください。 通常、実行時環境ごとに1つの DE 実装のみが存在します。

> [!NOTE]
> Transact-sql とでは個別の DE が実装されてい [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] ますが、VBScript を使用して [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] 1 つの de を共有します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグを使用すると、デバッグエンジンは、シェルと同じプロセス内、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] またはデバッグ対象のプログラムと同じプロセスで、次の2つの方法のいずれかを実行できます。 後者の形式は通常、デバッグ中のプロセスが、実際にはインタープリターで実行されるスクリプトである場合に発生します。 デバッグエンジンは、スクリプトを監視するためにインタープリターに関する詳しい知識を持っている必要があります。 この場合、インタープリターは実際にはランタイムです。デバッグエンジンは、特定のランタイム実装に使用されます。 さらに、単一の DE の実装は、プロセスとコンピューターの境界を越えて分割できます (リモートデバッグなど)。

 DE はデバッグインターフェイスを公開し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 すべての通信は COM を介して行われます。 DE がインプロセス、アウトプロセス、または別のコンピューターのどちらに読み込まれても、コンポーネントの通信には影響しません。

 DE は式エバリュエーターコンポーネントと連携して、特定のランタイムが式の構文を理解できるようにします。 また、DE は、シンボルハンドラーコンポーネントと共に、言語コンパイラによって生成されるシンボリックデバッグ情報にアクセスします。 詳細については、「 [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md) と [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)
- [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)
- [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md)
