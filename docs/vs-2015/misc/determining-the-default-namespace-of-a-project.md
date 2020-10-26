---
title: プロジェクトの既定の名前空間を決定する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- custom tools, computing default namespace
ms.assetid: 6d890676-7016-458c-8a6a-95cc0a068612
caps.latest.revision: 13
manager: jillfra
ms.openlocfilehash: 1d58c8986922c30192d6300a623a635b24c34ed5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65705772"
---
# <a name="determining-the-default-namespace-of-a-project"></a>プロジェクトの既定の名前空間の決定
[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]では、 `CustomToolNamespace` プロパティが入力ファイルに設定されている場合、の値は、 `CustomToolNamespace` メソッドに渡される既定の namespace パラメーターの値になり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> ます。 それ以外の場合、 `wszDefaultNamespace` に渡されるパラメーター `Generate` は、常にルート名前空間と同じになります。 名前空間の詳細については、「 [名前空間キーワード](https://msdn.microsoft.com/library/091a66eb-b10d-4f54-9102-5ac0d4bdb84b)」を参照してください。  
  
 [!INCLUDE[csprcs](../includes/csprcs-md.md)] フォルダーベースの名前空間を使用します。 つまり、名前空間は、ルート名前空間、およびカスタムツールを含むフォルダーの名前で構成されます。 各フォルダー名は、有効な識別子に変換され、ピリオドはすべての名前に分けられます。 たとえば、入力ファイルが FolderA\FolderB\FolderC\MyInput.txt で、ルート名前空間が CL9 の場合、計算された既定の名前空間は CL9 になり **ます。FolderA. Foldera. Foldera**。  
  
 このルールの例外は、階層チェーンに Web 参照フォルダが含まれている場合に発生します。 たとえば、次のような場合です。  
  
- FolderC は Web 参照フォルダーであるため、名前空間は CL9 になり **ます。FolderC**。  
  
- FolderB は Web 参照フォルダーであり、名前空間は **CL9 です。FolderB. Folderb**。  
  
  つまり、名前空間は次の形式を使用します。  
  
```  
rootNamespace.webReferenceFolder.containedFolder.containedFolder ...  
```  
  
## <a name="see-also"></a>参照  
 [単一ファイルジェネレーターの実装](../extensibility/internals/implementing-single-file-generators.md)   
 [登録 (単一ファイルジェネレーターを)](../extensibility/internals/registering-single-file-generators.md)   
 [ビジュアル デザイナーへのタイプの公開](../extensibility/internals/exposing-types-to-visual-designers.md)