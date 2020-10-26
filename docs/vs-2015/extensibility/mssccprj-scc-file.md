---
title: MSSCCPRJ.SCC.SCC ファイル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 705e0fa821000716dc9cd729901fbb7db5fd759c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194220"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ.SCC File
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IDE を使用して Visual Studio ソリューションまたはプロジェクトをソース管理下に配置すると、IDE は、ソース管理プラグインからの2つの重要な情報を文字列の形式で受け取ります。 これらの文字列 "/" は IDE に対して不透明ですが、プラグインによって使用され、バージョン管理でソリューションまたはプロジェクトを検索します。 通常、IDE は [Sccgetprojpath](../extensibility/sccgetprojpath-function.md)を呼び出してこれらの文字列を最初に取得し、次に [Sccopenproject](../extensibility/sccopenproject-function.md)への後続の呼び出しのためにソリューションまたはプロジェクトファイルに保存します。 ソリューションファイルとプロジェクトファイルに埋め込まれている場合、ユーザーがバージョン管理されているソリューションやプロジェクトファイルを分岐、分岐、またはコピーしても、"" 更新 "と" ProjName "の文字列は自動的に更新されません。 ソリューションファイルとプロジェクトファイルがバージョンコントロールの正しい位置を指していることを確認するには、ユーザーが文字列を手動で更新する必要があります。 文字列は不透明であるため、常に更新方法が明確であるとは限りません。  
  
 ソース管理プラグインは、"MSSCCPRJ.SCC" と呼ばれる特殊なファイルに "" 文字列と "ProjName" 文字列を格納することで、この問題を回避できます。SCC ファイル。 これは、プラグインによって所有および管理されるローカルのクライアント側ファイルです。 このファイルはソース管理下には配置されませんが、ソース管理されたファイルを含むすべてのディレクトリのプラグインによって生成されます。 どのファイルが Visual Studio ソリューションとプロジェクトファイルであるかを判断するために、ソース管理プラグインは、ファイル拡張子を標準またはユーザーが指定したリストと比較できます。 IDE は、プラグインが MSSCCPRJ.SCC をサポートしていることを検出します。SCC ファイルは、ソリューションファイルとプロジェクトファイルに "MSSCCPRJ.SCC" 文字列と "ProjName" 文字列を埋め込まなくなり、これらの文字列を読み取ります。代わりに SCC ファイル。  
  
 MSSCCPRJ.SCC をサポートするソース管理プラグイン。SCC ファイルは、次のガイドラインに従う必要があります。  
  
- MSSCCPRJ.SCC は1つしか存在できません。ディレクトリごとの SCC ファイル。  
  
- MSSCCPRJ.SCC。SCC ファイルには、指定されたディレクトリ内のソース管理下にある複数のファイルに対する "/" を含めることができます。  
  
- "/Xpath" 文字列の中に引用符を含めることはできません。 区切り記号として引用符を付けることができます (たとえば、二重引用符のペアを使用して空の文字列を示すことができます)。 IDE では、MSSCCPRJ.SCC から読み取られるときに、"Xpath" 文字列からすべての引用符が削除されます。SCC ファイル。  
  
- MSSCCPRJ.SCC の "ProjName" 文字列。SCC ファイルは、関数から返された文字列と正確に一致している必要があり `SccGetProjPath` ます。 関数によって返される文字列が引用符で囲まれている場合は、MSSCCPRJ.SCC 内の文字列。SCC ファイルは引用符で囲む必要があり、逆の場合も同様です。  
  
- MSSCCPRJ.SCC。SCC ファイルは、ソース管理下にファイルが配置されるたびに作成または更新されます。  
  
- MSSCCPRJ.SCC の場合。SCC ファイルが削除されると、プロバイダーは、そのディレクトリに関するソース管理操作を次回実行するときに、そのファイルを再生成する必要があります。  
  
- MSSCCPRJ.SCC。SCC ファイルは、定義された形式に厳密に従う必要があります。  
  
## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ.SCC の図。SCC ファイル形式  
 MSSCCPRJ.SCC の例を次に示します。SCC ファイル形式 (行番号はガイドとしてのみ提供されており、ファイル本文に含めることはできません):  
  
 [行 1] `SCC = This is a Source Code Control file`  
  
 [2 行目]  
  
 [行 3] `[TestApp.sln]`  
  
 [4 行目] `SCC_Aux_Path = "\\server\vss\"`  
  
 [行 5] `SCC_Project_Name = "$/TestApp"`  
  
 [6 行目]  
  
 [7 行目] `[TestApp.csproj]`  
  
 [行 8] `SCC_Aux_Path = "\\server\vss\"`  
  
 [9 行目] `SCC_Project_Name = "$/TestApp"`  
  
 最初の行は、ファイルの目的を示すもので、この種類のすべてのファイルの署名として機能します。 この行は、すべての MSSCCPRJ.SCC でこれとまったく同じように表示されます。SCC ファイル:  
  
 `SCC = This is a Source Code Control file`  
  
 次に示すのは、ファイル名が角かっこで囲まれた各ファイルの設定のセクションです。 このセクションは、追跡されるファイルごとに繰り返されます。 この行は、ファイル名のサンプルです (つまり、) `[TestApp.csproj]` 。 IDE では、次の2行が必要です。 ただし、定義されている値のスタイルは定義されません。 変数は `SCC_Aux_Path` と `SCC_Project_Name` です。  
  
 `SCC_Aux_Path = "\\server\vss\"`  
  
 `SCC_Project_Name = "$/TestApp"`  
  
 このセクションには、末尾の区切り記号がありません。 ファイルの名前、およびファイルに表示されるすべてのリテラルは、scc ヘッダーファイルで定義されています。 詳細については、「 [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)   
 [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
