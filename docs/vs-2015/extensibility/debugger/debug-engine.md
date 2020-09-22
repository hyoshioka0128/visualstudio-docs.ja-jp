---
title: デバッグエンジン |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6e81a95cffebc9e26821b9cc6157627100343452
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841816"
---
# <a name="debug-engine"></a>デバッグ エンジン
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグエンジン (DE) はインタープリターやオペレーティングシステムと連携して、実行制御、ブレークポイント、式の評価などのデバッグサービスを提供します。 DE は、デバッグ中のプログラムの状態を監視する役割を担います。 これを実現するために、DE は、サポートされているランタイムで使用可能な任意のメソッド (CPU から、またはランタイムによって提供される Api) を使用します。  
  
 たとえば、共通言語ランタイム (CLR) は、実行中のプログラムをコンポーネントのインターフェイスで監視するメカニズムを提供します。 CLR をサポートする DE は、適切なツールのインターフェイスを使用して、デバッグされているマネージコードプログラムを追跡します。 次に、状態の変更をセッションデバッグマネージャー (SDM) に伝達します。これにより、このような情報が IDE に転送さ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] れます。  
  
> [!NOTE]
> デバッグエンジンは、特定のランタイム (デバッグ対象のプログラムが実行されるシステム) を対象とします。 CLR はマネージコードのランタイムであり、Win32 ランタイムはネイティブ Windows アプリケーション用です。 作成した言語がこれら2つのランタイムのいずれかを対象とする場合は、に [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 必要なデバッグエンジンが既に用意されています。 実装する必要があるのは、式エバリュエーターだけです。  
  
## <a name="debug-engine-operation"></a>デバッグエンジンの操作  
 監視サービスは、DE インターフェイスによって実装され、デバッグパッケージが異なる動作モード間で移行する可能性があります。 詳細については、「 [操作モード](../../extensibility/debugger/operational-modes.md)」を参照してください。 通常、実行時環境ごとに1つの DE 実装のみが存在します。  
  
> [!NOTE]
> Transact-sql とでは個別の DE が実装されてい [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] ますが、VBScript を使用して [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] 1 つの de を共有します。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] デバッグを使用すると、デバッグエンジンは、シェルと同じプロセス内、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] またはデバッグ対象のプログラムと同じプロセスで、次の2つの方法のいずれかを実行できます。 後者の形式は通常、デバッグ中のプロセスがインタープリターで実行されるスクリプトであり、スクリプトを監視するために、デバッグエンジンがインタープリターに関する詳しい知識を持っている必要がある場合に発生します。 この場合、インタープリターは実際にはランタイムです。デバッグエンジンは、特定のランタイム実装に使用されます。 さらに、単一の DE の実装は、プロセスとコンピューターの境界を越えて分割できます (リモートデバッグなど)。  
  
 DE はデバッグインターフェイスを公開し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 すべての通信は COM を介して行われます。 DE がインプロセス、アウトプロセス、または別のコンピューターのどちらに読み込まれても、コンポーネントの通信には影響しません。  
  
 DE は、式エバリュエーターコンポーネントと連携して、特定の実行時間の DE を有効にして、式の構文を理解します。 また、DE は、シンボルハンドラーコンポーネントと共に、言語コンパイラによって生成されるシンボリックデバッグ情報にアクセスします。 詳細については、「 [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md) と [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)   
 [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)   
 [シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)
