---
title: モジュールを使用してソリューションにファイルを含める | Microsoft Docs
description: SharePoint ソリューション内のファイル用にモジュールまたはコンテナーを使用して、ファイルの種類 (マスター ページなど) に関係なく、ファイルを SharePoint サーバーに配置します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deployment modules
- SharePoint development in Visual Studio, modules
- modules [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: aa0d6fe1855a1d60a0e1293e8422791f8148bd04
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95442522"
---
# <a name="use-modules-to-include-files-in-the-solution"></a>モジュールを使用してソリューションにファイルを含める
  ファイルの種類 (新しいマスター ページなど) に関係なく、SharePoint サーバーへのファイルの配置が必要になる場合があります。 その場合は、"*モジュール*" ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] コード モジュールと混同しないでください) を使用できます。 モジュールは、SharePoint ソリューション内のファイルのコンテナーです。 ソリューションが配置されると、モジュール内のファイルが SharePoint サーバー上の指定されたフォルダーにコピーされます。

## <a name="module-items-and-elements"></a>モジュールの項目と要素
 モジュールを作成するには、 **[新しい項目の追加]** ダイアログ ボックスでそれを選択し、プロジェクトに追加します。 その後、その *Elements.xml* ファイルを変更し、配置するファイルの名前、システム上の配置先、および SharePoint サーバー上でのコピー先を含めます。

 モジュールの *Elements.xml* ファイルの例を以下に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Module Name="Module1">
        <File Path="Module1\Sample.txt" Url="Module1/Sample.txt" />
    </Module>
</Elements>

```

 新しく作成されたモジュールには、次の既定のファイルが含まれています。

|ファイル名|説明|
|---------------|-----------------|
|*Elements.xml*|モジュールの定義ファイル。|
|*Sample.txt*|モジュール内のファイルの例として機能するプレースホルダー ファイル。|

 *Elements.xml* ファイルには次の要素が含まれます。

|要素名|説明|
|------------------|-----------------|
|要素|モジュールで定義されているすべての要素が含まれます。|
|モジュール|Module 要素には、`<Module Name="Module1">` という形式でモジュールの名前を指定する 1 つの属性 (*Name*) があります。<br /><br /> モジュールの名前 (またはその *Folder Name* プロパティ) を変更した場合は、Module 要素内の名前を手動で更新する必要があることに注意してください。<br /><br /> Module 要素内のファイルのサブディレクトリを指定すると、[!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] (WSS) によって、それに一致するディレクトリ構造が自動的に作成されます。|
|ファイル|File 要素には、*Path* と *Url* の 2 つのパラメーターがあります。<br /><br /> - Path: SharePoint ソリューション内のファイルの名前と場所。 形式は `Path="Module1\Sample.txt"` です。<br /><br /> - Url: SharePoint サーバー上のファイルの配置先。 形式は `Url="Module1/Sample.txt"` です。<br /><br /> - Type: 次の 2 つの設定値を持つ省略可能な属性: *GhostableInLibrary* と *Ghostable*。 形式は `Type="GhostableInLibrary"` です。 *GhostableInLibrary* を指定すると、ファイルは、ライブラリに追加されたときにそのファイルに付随するリスト項目と共に、SharePoint のドキュメント ライブラリに追加されます。 *Ghostable* を指定すると、ファイルがドキュメント ライブラリの外部の SharePoint に追加されます。|

 配置する各ファイルでは、*Elements.xml* に個別の `<File>` 要素エントリが必要です。

## <a name="see-also"></a>関連項目
- [方法: モジュールを使用してファイルを含める](../sharepoint/how-to-include-files-by-using-a-module.md)
- [方法: ファイルをプロビジョニングする](/previous-versions/office/developer/sharepoint-2010/ms441170(v=office.14))
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint の Web パーツの作成](../sharepoint/creating-web-parts-for-sharepoint.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
