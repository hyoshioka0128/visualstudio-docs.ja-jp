---
title: '[VC++ プロジェクトの設定][オプション] ダイアログ ボックス - [プロジェクトおよびソリューション] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.VCBuild
helpviewer_keywords:
- builds [Visual Studio], logs
- build process [C++]
- files [Visual Studio], built by C/C++ compiler
- file extensions, built by C or C++ compiler
- cl.exe compiler, file extensions
- extensions, files built by C or C++ compiler
- BuildLog.htm
ms.assetid: 56420efd-6a95-464e-b890-e2b38c48d66a
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ef861d13387c013659e5e4c1714680b71896858c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657862"
---
# <a name="vc-project-settings-projects-and-solutions-options-dialog-box"></a>[VC++ プロジェクトの設定][オプション] ダイアログ ボックス - [プロジェクトおよびソリューション]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このダイアログ ボックスを使用すると、ビルドのログおよびサポートするファイルの種類に関連する [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] プロジェクトの設定を定義できます。

### <a name="to-access-this-dialog-box"></a>このダイアログ ボックスを表示するには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[プロジェクトおよびソリューション]** をクリックし、 **[VC++ プロジェクトの設定]** をクリックします。

## <a name="build-customization-search-path"></a>[ビルドのカスタマイズの検索パス]
 .rules ファイルを含むディレクトリの一覧を指定します。これは、プロジェクトのビルド ルールを定義するときに役立ちます。

## <a name="build-logging"></a>[ビルドのログ]
 **はい**ビルドログファイルの生成をオンにします。 このオプションを指定すると、プロジェクトの中間ファイル ディレクトリに BuildLog.htm ファイルが生成されます。 新しくビルドを実行するたびに、以前の BuildLog.htm ファイルは上書きされます。

 **いいえ**ビルドログファイルの生成をオフにします。

## <a name="build-timing"></a>[ビルド時間]
 **はい**ビルドのタイミングをオンにします。 このオプションをオンにすると、ビルドが完了するまでに要した時間がアウトプット ウィンドウに表示されます。 詳細については、「[[出力] ウィンドウ](../../ide/reference/output-window.md)」を参照してください。

 **いいえ**ビルドのタイミングをオフにします。

## <a name="extensions-to-hide"></a>[表示しない拡張子]
 **[すべてのファイルを表示]** が有効になっているときに**ソリューション エクスプローラー**に表示されないファイルのファイル名拡張子を指定します。

## <a name="extensions-to-include"></a>[含める拡張子]
 プロジェクトに移植できるファイルのファイル名拡張子を指定します。

## <a name="maximum-concurrent-c-compilations"></a>[同時実行する C++ コンパイルの最大数]
 C++ の並列コンパイルに使用する CPU コアの最大数を指定します。

## <a name="show-environment-in-log"></a>[ログで環境を表示]
 **はい**ビルドログファイル内の環境変数を一覧表示します。 このオプションを使用すると、[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] プロジェクトのビルド中に、すべての環境変数がビルド ログ ファイルにエコーされます。

 **いいえ**ビルドログファイルから環境変数を除外します。

## <a name="solution-explorer-mode"></a>[ソリューション エクスプローラー モード]
 **プロジェクト内のファイルのみを表示**プロジェクト内のファイルのみを表示するように**ソリューションエクスプローラー**を構成します。

 **すべてのファイルを表示**プロジェクト内のファイルとディスク上のファイルをプロジェクトフォルダーに表示するように**ソリューションエクスプローラー**を構成します。

## <a name="see-also"></a>関連項目
 [ビルド c/C++プログラム](https://msdn.microsoft.com/library/fa6ed4ff-334a-4d99-b5e2-a1f83d2b3008) [c/C++ビルドリファレンス](https://msdn.microsoft.com/library/100b4ccf-572c-4d1f-970c-fa0bc0cc0d2d)
