---
title: C/C++ のコード分析の概要 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: overview
helpviewer_keywords:
- annotations, code analysis
- build integration, code analysis
- C/C++ code analysis
- IDE, code analysis
- pragma directive, code analysis
- code analysis, C/C++
- code analysis tool
- command line, code analysis
- C++, code analysis
- check-in policies, code analysis
- '#pragma directives, code analysis'
- C, code analysis
ms.assetid: 81f0c9e8-f471-4de5-aac4-99db336a8809
caps.latest.revision: 27
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 1ce41cd1c0dabc94658b83aa5e2bcdc08d005fdb
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "77275364"
---
# <a name="code-analysis-for-cc-overview"></a>C/C++ のコード分析の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C/C++ コード分析ツールは、C/C++ ソース コードの障害に関する情報を開発者に提供します。 このツールによってレポートされる一般的なコーディング エラーとしては、バッファー オーバーラン、初期化されていないメモリ、null ポインターの逆参照、メモリ リーク、リソース リークなどがあります。  
  
## <a name="ide-integrated-development-environment-integration"></a>IDE (統合開発環境) の統合  
 開発者が分析ツールを自然に使用できるように、分析ツールは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE に完全に統合されています。 ビルド プロセス中は、ソース コードに対して生成された警告がエラー一覧に表示されます。 警告の原因となったソース コードに移動して、問題の原因と考えられる解決策に関する追加情報を表示できます。  
  
## <a name="pragma-support"></a>#pragma のサポート  
 開発者は `#pragma` ディレクティブを使用して、警告をエラーとして扱うか、警告を有効または無効にするか、個々のコード行の警告を非表示にすることができます。 詳細については、[Enable and Disable Code Analysis for Specific C/C++ Warnings](https://msdn.microsoft.com/910b8518-71f1-4b2e-b012-70647795642a)」(特定の C/C++ の警告についてコード分析を有効または無効にする) を参照してください。  
  
## <a name="annotation-support"></a>注釈のサポート  
 注釈によってコード分析の精度が向上します。 注釈には、関数のパラメーターと戻り値の型について、事前および事後の状態に関する追加情報を指定します。 詳細については、[__analysis_assume を使用して追加のコード情報を指定する](../code-quality/how-to-specify-additional-code-information-by-using-analysis-assume.md)」を参照してください。  
  
## <a name="run-analysis-tool-as-part-of-check-in-policy"></a>チェックイン ポリシーの一部としての分析ツールの実行  
 チェックインされるすべてのソース コードが、特定のポリシーを満たしていることが必要な場合があります。 具体的には、最新のローカル ビルドのステップとして分析が実行されたことを確認する必要があります。 コード分析チェックイン ポリシーを有効にする方法の詳細については、「[コード分析を用いたチェックイン ポリシーの作成と使用](../code-quality/creating-and-using-code-analysis-check-in-policies.md)」を参照してください。  
  
## <a name="team-build-integration"></a>チーム ビルドの統合  
 ビルド システムの統合機能を使用すると、コード分析ツールを [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] ビルド プロセスのステップとして実行できます。 詳細については、「[アプリケーションのビルド](/azure/devops/pipelines/index)」をご覧ください。  
  
## <a name="command-line-support"></a>コマンド ラインのサポート  
 開発環境内への完全な統合に加えて、次の例に示すように、開発者はコマンド ラインから分析ツールを使用することもできます。  
  
 `C:\>cl /analyze Sample.cpp`
