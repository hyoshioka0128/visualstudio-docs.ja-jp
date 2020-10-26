---
title: SGen タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#SGen
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- SGen task [MSBuild]
- MSBuild, SGen task
ms.assetid: 22c5ade4-4159-4667-b891-0c1aa06f4df5
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3be3aa5426c2d1283b8b4cded51cc9c2772642ab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682101"
---
# <a name="sgen-task"></a>SGen タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定されたアセンブリの種類に対応する XML シリアル化アセンブリを作成します。 このタスクは、XML シリアライザー ジェネレーター ツール (Sgen.exe) をラップするタスクです。 詳細については、「 [XML Serializer Generator Tool (Sgen.exe)](https://msdn.microsoft.com/library/cc1d1f1c-fb26-4be9-885a-3fe84c81cec6)」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 `SGen` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`BuildAssemblyName`|必須の `String` 型のパラメーターです。<br /><br /> シリアル化コード生成の対象となるアセンブリ。|  
|`BuildAssemblyPath`|必須の `String` 型のパラメーターです。<br /><br /> シリアル化コード生成の対象となるアセンブリのパス。|  
|`DelaySign`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、完全署名されたアセンブリを必要とすることが指定されます。 `false` の場合、アセンブリに公開キーを含めることだけを要求するように指定されます。<br /><br /> `KeyFile` または `KeyContainer` パラメーターと併用しない限り、このパラメーターには何の効果もありません。|  
|`KeyContainer`|省略可能な `String` 型のパラメーターです。<br /><br /> キー ペアを保持するコンテナーを指定します。 こうすると、アセンブリ マニフェストに公開キーを挿入することによって、アセンブリに対する署名が行われます。 次に、タスクは最終的なアセンブリに秘密キーで署名します。|  
|`KeyFile`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリに署名するためのキー ペアまたは公開キーを指定します。 コンパイラは、アセンブリ マニフェストに公開キーを挿入し、最終的なアセンブリに秘密キーで署名します。|  
|`Platform`|省略可能な `String` 型のパラメーターです。<br /><br /> 出力アセンブリの生成に使用されるコンパイラ プラットフォームを取得または設定します。 このパラメーターの値には、`x86`、`x64`、または `anycpu` を指定できます。 既定値は `anycpu` です。|  
|`References`|省略可能な `String[]` 型のパラメーターです。<br /><br /> XML シリアル化が必要な型によって参照されるアセンブリを指定します。|  
|`SdkToolsPath`|省略可能な `String` 型のパラメーターです。<br /><br /> resgen.exe などの SDK ツールのパスを指定します。|  
|`SerializationAssembly`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 生成されたシリアル化アセンブリが格納されます。|  
|`SerializationAssemblyName`|省略可能な `String` 型のパラメーターです。<br /><br /> 生成されるシリアル化アセンブリの名前を指定します。|  
|`ShouldGenerateSerializer`|必須の `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、SGen タスクでシリアル化アセンブリを生成する必要があります。|  
|`Timeout`|省略可能な `Int32` 型のパラメーターです。<br /><br /> タスク実行を終了するまでの時間をミリ秒単位で指定します。 既定値は `Int.MaxValue` であり、タイムアウト期限がないことを示します。|  
|`ToolPath`|省略可能な `String` 型のパラメーターです。<br /><br /> タスクが基になる実行可能ファイル (sgen.exe) を読み込む場所を指定します。 このパラメーターを指定しないと、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] を実行しているフレームワークのバージョンに対応する SDK インストール パスがタスクに使用されます。|  
|`Types`|省略可能な `String[]` 型のパラメーターです。<br /><br /> シリアル化コードを生成する特定の型の一覧を取得または設定します。 SGen は、これらの型に対してのみ、シリアル化コードを生成します。|  
|`UseProxyTypes`|必須の `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、SGen タスクでは XML Web サービス プロキシ型に対してのみシリアル化コードを生成します。|  
  
## <a name="remarks"></a>Remarks  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.ToolTaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.ToolTask> クラスから継承されます。 これらの追加パラメーターとその説明の一覧については、「 [Tooltaskextension Base Class](../msbuild/tooltaskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)   
 [タスク](../msbuild/msbuild-tasks.md)   
 [MSBuild の概念](../msbuild/msbuild-concepts.md)
