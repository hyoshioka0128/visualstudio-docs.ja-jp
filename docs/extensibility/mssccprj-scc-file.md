---
title: MSSCCPRJ.SCC.SCC ファイル |Microsoft Docs
description: MSSCCPRJ.SCC について説明します。SCC ファイル。これは、Visual Studio SDK で動作するソース管理プラグインによって使用されるローカルのクライアント側ファイルです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f55e99d9df10ef2f96761a9436597d227cf0cd93
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99886692"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ.SCC.SCC ファイル
IDE を使用して Visual Studio ソリューションまたはプロジェクトをソース管理下に配置すると、IDE は2つの重要な情報を受け取ります。 この情報は、ソース管理プラグインから文字列の形式で取得されます。 これらの文字列 "/" は IDE に対して不透明ですが、プラグインによって使用され、バージョン管理でソリューションまたはプロジェクトを検索します。 通常、IDE では [Sccgetprojpath](../extensibility/sccgetprojpath-function.md)を呼び出してこれらの文字列を最初に取得し、次に [Sccopenproject](../extensibility/sccopenproject-function.md)への後続の呼び出しのためにソリューションまたはプロジェクトファイルに保存します。 ソリューションファイルとプロジェクトファイルに埋め込まれている場合、ユーザーがバージョン管理されているソリューションやプロジェクトファイルを分岐、分岐、またはコピーしても、"" 更新 "と" ProjName "の文字列は自動的に更新されません。 ソリューションファイルとプロジェクトファイルがバージョンコントロールの正しい位置を指していることを確認するには、ユーザーが文字列を手動で更新する必要があります。 文字列は不透明であるため、常に更新方法が明確であるとは限りません。

 ソース管理プラグインは、Mssccprj.scc ファイルと呼ばれる特殊なファイルに "  " 文字列と "ProjName" 文字列を格納することで、この問題を回避できます。 これは、プラグインによって所有および管理されるローカルのクライアント側ファイルです。 このファイルはソース管理下には配置されませんが、ソース管理されたファイルを含むすべてのディレクトリのプラグインによって生成されます。 どのファイルが Visual Studio ソリューションとプロジェクトファイルであるかを判断するために、ソース管理プラグインは、ファイル拡張子を標準またはユーザーが指定したリストと比較できます。 プラグインが *mssccprj.scc* ファイルをサポートしていることが IDE によって検出されると、"mssccprj.scc" という文字列がソリューションとプロジェクトファイルに埋め込まれなくなり、それらの文字列がファイルから読み込まれます。

 *Mssccprj.scc* ファイルをサポートするソース管理プラグインは、次のガイドラインに従う必要があります。

- *Mssccprj.scc* ファイルは、ディレクトリごとに1つだけ指定できます。

- Mssccprj.scc ファイルには、指定されたディレクトリ内のソース管理下にある複数のファイルの "  xpath" と "ProjName" を含めることができます。

- "/Xpath" 文字列の中に引用符を含めることはできません。 区切り記号として引用符を付けることができます (たとえば、二重引用符のペアを使用して空の文字列を示すことができます)。 IDE では、Mssccprj.scc ファイルから読み取られるときに、"  xpath" 文字列からすべての引用符が削除されます。

- Mssccprj.scc の "ProjName" 文字列 *。SCC ファイル* は、関数から返された文字列と正確に一致している必要があり `SccGetProjPath` ます。 関数によって返される文字列が引用符で囲まれている場合、 *mssccprj.scc* ファイル内の文字列は引用符で囲む必要があります。その逆も同様です。

- ファイルがソース管理下に配置されるたびに、 *mssccprj.scc* ファイルが作成または更新されます。

- *Mssccprj.scc* ファイルが削除された場合、プロバイダーは、そのディレクトリに関するソース管理操作を次回実行するときに、このファイルを再生成する必要があります。

- *Mssccprj.scc* ファイルは、定義された形式に厳密に従う必要があります。

## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ.SCC の図。SCC ファイル形式
 次に示すのは、 *mssccprj.scc* ファイル形式のサンプルです (行番号はガイドとしてのみ提供されており、ファイル本文に含めることはできません)。

- [行 1] `SCC = This is a Source Code Control file`

- [2 行目]

- [行 3] `[TestApp.sln]`

- [4 行目] `SCC_Aux_Path = "\\server\vss\"`

- [行 5] `SCC_Project_Name = "$/TestApp"`

- [6 行目]

- [7 行目] `[TestApp.csproj]`

- [行 8] `SCC_Aux_Path = "\\server\vss\"`

- [9 行目] `SCC_Project_Name = "$/TestApp"`

 最初の行は、ファイルの目的を示すもので、この種類のすべてのファイルの署名として機能します。 この行は、すべての *mssccprj.scc* ファイルで次のように表示されます。

 `SCC = This is a Source Code Control file`

 次のセクションでは、ファイル名が角かっこで囲まれた各ファイルの設定について詳しく説明します。 このセクションは、追跡されるファイルごとに繰り返されます。 この行は、ファイル名のサンプルです (つまり、) `[TestApp.csproj]` 。 IDE では、次の2行が必要です。 ただし、定義されている値のスタイルは定義されません。 変数は `SCC_Aux_Path` と `SCC_Project_Name` です。

 `SCC_Aux_Path = "\\server\vss\"`

 `SCC_Project_Name = "$/TestApp"`

 このセクションには、末尾の区切り記号がありません。 ファイルの名前、およびファイルに表示されるすべてのリテラルは、scc ヘッダーファイルで定義されています。 詳細については、「 [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
