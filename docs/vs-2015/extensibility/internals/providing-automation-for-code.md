---
title: コードの自動化の提供 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- CodeModel object
ms.assetid: 21cb3e63-f25c-404b-bc1d-a32ad0fdd4d5
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2e4d47a72adf787f5d560374e1c44743004d25f9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203234"
---
# <a name="providing-automation-for-code"></a>コードのオートメーションの提供
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

コードのオートメーションモデルを作成する必要はありません。 環境 SDK には、そのためのサンプルが用意されていません。 コードモデルの詳細については、オブジェクトを参照してください <xref:EnvDTE.CodeModel> 。  
  
 コードモデルを実装するには、内部データ構造によって決定されるインターフェイスを実装する必要があります。 オブジェクトは、クラスから派生する必要があり `IDispatch` ます。  
  
 拡張するオブジェクトとは、 <xref:EnvDTE.CodeModel> <xref:EnvDTE.FileCodeModel> オブジェクトから使用でき、 <xref:EnvDTE.Project> 次のようになります。  
  
 <xref:EnvDTE.Project.CodeModel%2A>  
  
 <xref:EnvDTE.ProjectItem.FileCodeModel%2A>  
  
 `CodeModel` `FileCodeModel` オブジェクトとオブジェクトから返されたオブジェクトに、インターフェイスまたはインターフェイスだけを実装することを選択でき `Project` <xref:EnvDTE.ProjectItem> ます。 このインターフェイスには、プロジェクトシステムに適した機能をすべて提供します。  
  
 標準およびインターフェイスからは使用できない機能 (メソッドやプロパティなど) を追加する場合は `CodeModel` 、 `FileCodeModel` 標準から継承する独自のインターフェイスを作成します。 エンドユーザーが見つけられるように、プロジェクトシステムでドキュメント化してください。 標準のインターフェイスを返しますが、ユーザーはメソッドを呼び出すことも、インターフェイスにキャストすることもでき `QueryInterface` ます (存在する場合)。  
  
## <a name="see-also"></a>参照  
 [オートメーション モデルの概要](../../extensibility/internals/automation-model-overview.md)
