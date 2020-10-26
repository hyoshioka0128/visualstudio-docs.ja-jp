---
title: プロジェクトの種類を作成する場合 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5b5bc2bacb53973bd552b983b742e4f9e68fe31b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687708"
---
# <a name="when-to-create-project-types"></a>プロジェクト タイプを作成する状況
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

新しいプロジェクトの種類を作成すると、ユーザー向けにカスタマイズするための基礎と [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] なります。 ただし、すべてのカスタマイズに新しいプロジェクトの種類を作成する必要はありません [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 次のガイドラインは、シナリオに新しいプロジェクトの種類が必要かどうかを判断するのに役立ちます。  
  
## <a name="create-a-new-project-type"></a>新しいプロジェクトの種類を作成する  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]次の1つまたは複数の方法で動作するようにをカスタマイズする場合は、プロジェクトの種類を作成する必要があります。  
  
- ビルド、配置、構成、ソース管理に参加します。  
  
- デバッグサポートを提供します。  
  
- **ソリューションエクスプローラー**にプロジェクト項目を表示します。  
  
- [ **プロジェクトを開く** ] または [ **新しいプロジェクト** ] ダイアログボックスを使用します。  
  
- プロジェクトの入れ子をサポートします。  
  
## <a name="extend-an-existing-project-type"></a>既存のプロジェクトの種類を拡張する  
 次の方法でを使用して、プロジェクト [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のビルドプロセスを変更するなど、既存のプロジェクトの種類の動作を変更または拡張できる、新しいプロジェクトの種類を作成することができ [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] ます。  
  
- 複数のファイルを1つの単位として操作します。  
  
- サブ項目の階層として1つのファイルを表示します。  
  
- エディターの周囲にコマンドコンテキストを表示します。  
  
- エディターのサービスコンテキストを表示します。  
  
## <a name="use-an-existing-project-type"></a>既存のプロジェクトの種類を使用する  
 新しいプロジェクトを作成する必要はない場合があります。 次の表に、プロジェクトの種類を作成する必要がないタスクを示します。  
  
|タスク|説明|  
|----------|-----------------|  
|コマンドの処理|VSPackage は、コマンドを処理できます。|  
|エディターのビルド|カスタムエディターを登録できます。 詳細については、「 [ドキュメントウィンドウとエディター](https://msdn.microsoft.com/603625e1-62b6-413a-bc44-089346e166bc)」を参照してください。|  
|所有しているウィンドウ|新しいプロジェクトの種類を追加せずに、ツールウィンドウとドキュメントウィンドウの両方を作成できます。|  
|プロパティウィンドウでのプロパティの公開|すべてのオブジェクトがプロパティを公開できます。|  
  
## <a name="create-a-project-subtype"></a>プロジェクトのサブタイプを作成する  
 プロジェクトのサブタイプを使用して、新しいプロジェクトの種類を作成することなく、マネージプロジェクトの種類を拡張することができます。 プロジェクトのサブタイプは、COM 集計を使用して、Microsoft またはで記述されたマネージプロジェクトを拡張し [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] ます。 COM 集計を使用すると、マネージプロジェクトシステムの実装の大部分を再利用しながら、集計やサポートインターフェイスを使用して特定のシナリオに合わせてカスタマイズできます。 プロジェクトのサブタイプの詳細については、「 [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ドキュメントウィンドウとエディター](https://msdn.microsoft.com/603625e1-62b6-413a-bc44-089346e166bc)   
 [チェックリスト: 新しいプロジェクトの種類の作成](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)
