---
title: Createのインスタンスユーティリティ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- experimental hive
- experimental instance
- createexpinstance
- createexpinst
ms.assetid: 03779774-9401-49ae-997c-0c3ab25ed0d5
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7d778f0f31a7651412915a898bff9e4bdfe6c55f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196981"
---
# <a name="createexpinstance-utility"></a>CreateExpInstance ユーティリティ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Createのインスタンスユーティリティを使用して、Visual Studio の実験用インスタンスを作成、リセット、または削除します。 実験用インスタンスを使用して、基になる製品を変更せずに Visual Studio 拡張機能のデバッグとテストを行うことができます。  
  
## <a name="syntax"></a>構文  
  
```  
CreateExpInstance.exe [/Create | /Reset | /Clean] /VSInstance=VsInstance /RootSuffix=Suffix  
```  
  
#### <a name="parameters"></a>パラメーター  
 /Create  
 実験用インスタンスを作成します。  
  
 /Reset  
 実験用インスタンスを削除し、新しいインスタンスを作成します。  
  
 /Clean  
 実験用インスタンスを削除します。  
  
 /Vsinstance  
 コピーする基本 Visual Studio インスタンスが格納されているディレクトリの名前。  
  
 /RootSuffix  
 実験用インスタンスディレクトリの名前に追加するサフィックス。  
  
## <a name="remarks"></a>注釈  
 Visual Studio 拡張機能を使用しているときに、F5 キーを押して既定の実験用インスタンスを開き、現在の拡張機能をインストールできます。 実験用インスタンスが使用できない場合は、既定の設定を持つものが Visual Studio によって作成されます。  
  
 実験用インスタンスの既定の場所は、Visual Studio のバージョン番号によって異なります。 たとえば、Visual Studio 2015 の場合、場所は%localappdata%\Microsoft\VisualStudio\14.0Exp\ で、ディレクトリの場所にあるすべてのファイルがそのインスタンスの一部と見なされます。 ディレクトリ名が既定の場所に変更されていない限り、追加の実験用インスタンスは Visual Studio によって読み込まれません。  
  
 実験用インスタンスを開いたときに、Visual Studio がシステムレジストリにアクセスすることはありません。 これは、以前のバージョンの Visual Studio とは異なり、以前のバージョンのレジストリハイブが使用されていました。  
  
 Createのインスタンスユーティリティは、VsRegEx ユーティリティに代わるものです。  
  
 次の例では、Visual Studio の既定の実験用インスタンスをリセットします。  
  
 **CreateExpInstance.exe/リセット/vsinstance = 14.0/rootsuffix = Exp**  
  
## <a name="see-also"></a>参照  
 [製品のリリース](../../misc/releasing-a-visual-studio-integration-product.md)
