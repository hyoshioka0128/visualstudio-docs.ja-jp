---
title: ソース管理プラグインを検索するためのキーとして使用される文字列 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, strings used for finding
ms.assetid: c1e31f76-42a1-4c3d-afb2-664044ef12fd
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 83ba843e318aac6a74d318978e42e2f81802d8ac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160580"
---
# <a name="strings-used-as-keys-for-finding-a-source-control-plug-in"></a>ソース管理プラグインを検索するためのキーとして使用される文字列
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

次の文字列は、ソース管理プラグインに関する情報を検索するためにレジストリにアクセスするためのキーです。  
  
 `STR_SCC_PROVIDER_REG_LOCATION`、 `STR_PROVIDERREGKEY` 、 `STR_SCCPROVIDERPATH` 、および `STR_SCCPROVIDERNAME` は、Visual Studio のソース管理プラグインとして DLL を登録するために使用されるレジストリキーまたは値です。  
  
 `SCC_PROJECTNAME_KEY`、 `SCC_PROJECTAUX_KEY` 、 `SCC_KEY, SCC_FILE_SIGNATURE` 、および `SCC_STATUS_FILE` は、mssccprj.scc の形式を説明するために使用されます。SCC ファイル。  
  
## <a name="string-keys-and-values"></a>文字列のキーと値  
  
|キー|値|  
|---------|-----------|  
|`STR_SCC_PROVIDER_REG_LOCATION`|Software\SourceCodeControlProvider|  
|`STR_PROVIDERREGKEY`|ProviderRegKey|  
|`STR_SCCPROVIDERPATH`|SCCServerPath|  
|`STR_SCCPROVIDERNAME`|SCCServerName|  
|`STR_SCC_INI_SECTION`|ソース コード管理|  
|`STR_SCC_INI_KEY`|SourceCodeControlProvider|  
|`SCC_PROJECTNAME_KEY`|SCC_Project_Name|  
|`SCC_PROJECTAUX_KEY`|SCC_Aux_Path|  
|`SCC_STATUS_FILE`|MSSCCPRJ.SCC.SCC|  
|`SCC_KEY`|SCC|  
|`SCC_FILE_SIGNATURE`|ソースコード管理ファイル|  
|`SCC_NSE`|名前空間の拡張|  
|`SCC_NSE_PREFIX`|廃棄プレフィックス|  
|`SCC_NSE_DisableOpenSCC`|DisableOpenFromSourceControl|  
|`STR_SCCHELPCOLLECTION`|HelpCollection|  
|`STR_UI_LANGUAGE`|UILanguage|  
|`STR_SRCSAFE_ROOT_KEY`|Software\Microsoft\SourceSafe|  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)   
 [方法: ソース管理プラグインをインストールする](../extensibility/internals/how-to-install-a-source-control-plug-in.md)   
 [MSSCCPRJ.SCC File](../extensibility/mssccprj-scc-file.md)
