---
title: MSBuild 12.0 の新機能 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
ms.assetid: 9976a6ad-c052-4017-b848-35b5ae4a2f66
caps.latest.revision: 26
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ba733b7ef20c9a03ad19d9847a4046e4d72ebdef
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75844455"
---
# <a name="what39s-new-in-msbuild-120"></a>MSBuild 12.0 の新機能
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild は、.NET Framework の一部ではなく Visual Studio の一部としてインストールされます。 MSBuild の現在のバージョン番号は 12.0 です。 MSBuild を個別にインストールする場合は、[MSBuild ダウンロード](https://www.microsoft.com/download/details.aspx?id=40760)からインストール パッケージをダウンロードします。  
  
## <a name="changed-path"></a>変更されたパス  
 MSBuild は、*%ProgramFiles%* の下に直接インストールされます (例: C:\Program Files\MSBuild\\)。  
  
## <a name="changed-properties"></a>変更されたプロパティ  
 新しいバージョン番号に伴い、次の MSBuild プロパティが変更されました。  
  
- `MSBuildToolsVersion`: このバージョンのツールでは 12.0 になります。  
  
- `MSBuildToolsPath`: このプロパティは、32 ビット オペレーティング システムでは %ProgramFiles%\MSBuild\12.0\bin になり、64 ビット オペレーティング システムでは %ProgramFiles%\MSBuild\12.0\bin\amd64 になります。  
  
- `ToolsVersion`: このプロパティの値は、32 ビット オペレーティング システムでは HKLM\SOFTWARE\Microsoft\MSBuild\ToolsVersions\12.0 で、64 ビット オペレーティング システムでは HKLM\SOFTWARE\Wow6432Node\Microsoft\MSBuild\ToolsVersions\12.0 で確認できます。  
  
- `SDK35ToolsPath` および `SDK40ToolsPath`: これらのプロパティは、このバージョンの Visual Studio に含まれている .NET Framework SDK を指しています (たとえば、4.X ツールの場合は 8.1A など)。  
  
## <a name="new-properties"></a>新しいプロパティ  
  
- `MSBuildFrameworkToolsPath`: 32 ビット オペレーティング システムでは %windir%\Microsoft.NET\Framework\v4.0.30319、64 ビット オペレーティング システムでは %windir%\Microsoft.NET\Framework64\v4.0.30319 を値として持つ新しいプロパティです。 このプロパティは、.NET Framework のツールとユーティリティを指すために使用できる `MSBuildToolsPath` に代わるプロパティです。  
  
- `MSBuildToolsPath` と `MSBuildFrameworkToolsPath` は 32 ビット対応のプロパティであり、`MSBuildToolsPath32` と `MSBuildFrameworkToolsPath32` は、32 ビットまたは 64 ビットの MSBuild を使用しているかどうかに関係なく、常に 32 ビットの場所を指します。

## <a name="see-also"></a>参照
[MSBuild](msbuild.md)
