---
title: カスタムドキュメントプロパティの概要
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], custom properties
- custom document properties
- document-level customizations [Office development in Visual Studio], custom properties
- Office documents [Office development in Visual Studio], custom properties
- _AssemblyLocation property
- _AssemblyName property
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7b3f4038a05478d8e2d747efa700c7ece02e4827
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62951176"
---
# <a name="custom-document-properties-overview"></a>カスタムドキュメントプロパティの概要

ドキュメントレベルのプロジェクトをビルドすると、Visual Studio によって、 \_ assemblylocation と AssemblyName という2つのカスタムプロパティがプロジェクトのドキュメントに追加されます。 \_ ユーザーがドキュメントを開くと、Microsoft Office アプリケーションは、これらのカスタムドキュメントプロパティをチェックします。 ドキュメント内に存在する場合は、アプリケーションによってが読み込まれ、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] カスタマイズが開始されます。 詳細については、「 [Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="_assemblyname"></a>\_AssemblyName

このプロパティは、の Office ソリューションローダーコンポーネント内のインターフェイスの CLSID を格納し [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 CLSID 値は4E3C66D5-58D4-491E-A7D4-64AF99AF6E8B です。 この値は変更しないでください。

## <a name="_assemblylocation"></a>\_AssemblyLocation

このプロパティには、カスタマイズの配置マニフェストに関する詳細を提供する文字列が含まれています。 マニフェストの詳細については、「 [Office ソリューションのアプリケーションマニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)」を参照してください。

 \_Assemblylocation プロパティ値の形式は、ソリューションのデプロイ方法によって異なります。

- ソリューションが Web サイト、UNC パス、または CD または USB ドライブからインストールされるように公開されている場合、_AssemblyLocation プロパティの形式は*deploymentmanifestpath* | *SolutionID*です。 次の文字列を例に示します。

     file://deployserver/MyShare/ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9

- ソリューションを Visual Studio から実行またはデバッグしている場合、_AssemblyLocation プロパティの形式は*DeploymentManifestName* | *SolutionID*| vstolocal です。 次の文字列を例に示します。

     Excelworkbook1.xlsx.log | 74744e4b-e4d6-41eb-84f7-ad20346fe2d9 | vstolocal

  *SolutionID*は、が [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ソリューションを識別するために使用する GUID です。 *SolutionID*は、プロジェクトのビルド時に自動的に生成されます。 **Vstolocal**用語は、アセンブリを [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ドキュメントと同じフォルダーから読み込む必要があることをに示します。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)
- [Office ソリューションのアプリケーションマニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)
- [方法: ClickOnce を使用して Office ソリューションを発行する](https://msdn.microsoft.com/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8)
- [方法: カスタムドキュメントプロパティを作成および変更する](../vsto/how-to-create-and-modify-custom-document-properties.md)
