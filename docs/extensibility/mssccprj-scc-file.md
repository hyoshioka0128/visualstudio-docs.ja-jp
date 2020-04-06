---
title: MSSCCPRJ.SCC ファイル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89511b7c8b69c5793eceef7d58153dde253a4f47
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702463"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ.SCC ファイル
IDE を使用して Visual Studio のソリューションまたはプロジェクトをソース管理下に配置すると、IDE は 2 つの重要な情報を受け取ります。 この情報は、ソース管理プラグインから文字列形式で取得されます。 これらの文字列 "AuxPath" および "ProjName" は IDE に対して不透明ですが、バージョン管理のソリューションまたはプロジェクトを見つけるためにプラグインによって使用されます。 IDE は通常[、SccGetProjPath](../extensibility/sccgetprojpath-function.md)を呼び出すことによってこれらの文字列を初めて取得し、その後[SccOpenProject](../extensibility/sccopenproject-function.md)を呼び出すためにソリューション ファイルまたはプロジェクト ファイルに保存します。 ソリューション ファイルとプロジェクト ファイルに埋め込まれている場合、バージョン管理のソリューション ファイルやプロジェクト ファイルを分岐、フォーク、またはコピーしたときに、"AuxPath" および "ProjName" 文字列は自動的に更新されません。 ソリューション ファイルとプロジェクト ファイルがバージョン管理の正しい場所を指していることを確認するには、ユーザーが文字列を手動で更新する必要があります。 文字列は不透明であるため、更新方法が明確であるとは限りません。

 ソース管理プラグインは、"AuxPath" および "ProjName" 文字列を*MSSCCPRJ.SCC*ファイルと呼ばれる特別なファイルに格納することで、この問題を回避できます。 これは、プラグインによって所有および管理されるローカルのクライアント側ファイルです。 このファイルはソース管理下に置かれることはありませんが、ソース管理されたファイルを含むすべてのディレクトリのプラグインによって生成されます。 どのファイルが Visual Studio ソリューション ファイルとプロジェクト ファイルかを判断するために、ソース管理プラグインは、標準またはユーザー指定のリストとファイル拡張子を比較できます。 プラグインが*MSSCCPRJ.SCC*ファイルをサポートしていることを検出すると、"AuxPath" および "ProjName" 文字列がソリューション ファイルとプロジェクト ファイルに埋め込まれなくなり、代わりに*MSSCCPRJ.SCC*ファイルからそれらの文字列が読み込まれます。

 *MSSCCPRJ.SCC*ファイルをサポートするソース管理プラグインは、次のガイドラインに従う必要があります。

- ディレクトリごとに 1 つの*MSSCCPRJ.SCC*ファイルしか存在できません。

- *MSSCCPRJ.SCC*ファイルには、特定のディレクトリ内でソース管理下にある複数のファイルの "AuxPath" および "ProjName" を含めることができます。

- "AuxPath" 文字列の中に引用符を含んではなりません。 引用符を区切り文字として囲むことができます (たとえば、二重引用符のペアを使用して空の文字列を示すことができます)。 IDE は *、MSSCCPRJ.SCC*ファイルから読み取られると、"AuxPath" 文字列からすべての引用符を削除します。

- MSSCCPRJ の "ProjName" 文字列 *。SCC ファイル*は、関数から返された文字列`SccGetProjPath`と完全に一致する必要があります。 関数によって返される文字列に引用符が含まれる場合 *、MSSCCPRJ.SCC*ファイル内の文字列は引用符を含む必要があります。

- *MSSCCPRJ.SCC*ファイルは、ソース管理下に置かれるたびに作成または更新されます。

- *MSSCCPRJ.SCC*ファイルが削除された場合、プロバイダは、そのディレクトリに関するソース管理操作を次回実行する時に、ファイルを再生成する必要があります。

- *MSSCCPRJ.SCC*ファイルは、定義された形式に厳密に従う必要があります。

## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ の図。SCC ファイル形式
 以下は*MSSCCPRJ.SCC*ファイル形式のサンプルです (行番号はガイドとしてのみ提供され、ファイル本文に含めるべきではありません)。

- [1行目]`SCC = This is a Source Code Control file`

- [2行目]

- [3行目]`[TestApp.sln]`

- [4行目]`SCC_Aux_Path = "\\server\vss\"`

- [5行目]`SCC_Project_Name = "$/TestApp"`

- [6行目]

- [7行目]`[TestApp.csproj]`

- [8行目]`SCC_Aux_Path = "\\server\vss\"`

- [9行目]`SCC_Project_Name = "$/TestApp"`

 最初の行は、ファイルの目的を示し、この種類のすべてのファイルの署名として機能します。 この行は、すべての*MSSCCPRJ.SCC*ファイルで次のように表示されます。

 `SCC = This is a Source Code Control file`

 次のセクションでは、ファイル名が角かっこで囲まれた各ファイルの設定について詳しく説明します。 このセクションは、追跡対象のファイルごとに繰り返されます。 この行は、ファイル名のサンプルです`[TestApp.csproj]`。 IDE では、次の 2 行が想定されます。 ただし、定義された値のスタイルは定義されません。 変数は`SCC_Aux_Path`と`SCC_Project_Name`です。

 `SCC_Aux_Path = "\\server\vss\"`

 `SCC_Project_Name = "$/TestApp"`

 このセクションには終了区切り記号はありません。 ファイルの名前と、ファイルに含まれるすべてのリテラルは、scc.h ヘッダー ファイルで定義されます。 詳細については、「[ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
