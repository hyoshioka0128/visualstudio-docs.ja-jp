---
title: XML データを使用するときのセキュリティに関する考慮事項
description: XML エディターまたは XSLT デバッガーで XML データを操作する場合のセキュリティに関する考慮事項について学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fce2b708-1aef-454f-be59-52b76f359351
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d9e98e18e3e01f53afa6b0a9ea3bdec94f2186f
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94351350"
---
# <a name="security-considerations-when-working-with-xml-data"></a>XML データを使用するときのセキュリティに関する考慮事項

このトピックでは、XML エディターや XSLT デバッガーを使用する際に知っておく必要があるセキュリティの問題について説明します。

## <a name="xml-editor"></a>XML エディター

XML エディターは、Visual Studio のテキスト エディターに基づいています。 XML エディターは通常、<xref:System.Xml> クラスと <xref:System.Xml.Xsl> クラスに依存して XML プロセスを処理します。

- XSLT 変換は、新しいアプリケーション ドメインで実行されます。 XSLT 変換は *サンドボックス化* されています。つまり、コンピューターのコード アクセス セキュリティ ポリシーを使用して、XSLT スタイル シートが置かれている場所に基づいてアクセス許可制限が決定されます。 たとえば、インターネット上にあるスタイル シートは最も制限されたアクセス許可を持ち、ユーザーのハード ディスクにコピーされているスタイル シートは "完全な信頼" で実行されます。

- <xref:System.Xml.Xsl.XslCompiledTransform> クラスは、XSLT を Microsoft Intermediate Language (MSIL) にコンパイルし、実行時の処理速度を高めるために使用されます。

- XML エディターが最初に読み込みを行うときに、カタログ ファイルの外部の場所を指し示すスキーマが自動的にダウンロードされます。 <xref:System.Xml.Schema.XmlSchemaSet> クラスは、スキーマをコンパイルするために使用されます。 XML エディターに付属するカタログ ファイルには、外部スキーマへのリンクは記述されていません。 XML エディターでスキーマ ファイルをダウンロードする前に、ユーザーは外部スキーマへの参照を明示的に追加する必要があります。 XML エディターの **[Miscellaneous Tools Options (その他のツールのオプション)]** ページで、HTTP のダウンロードを無効にすることができます。

- XML エディターでは、<xref:System.Net> クラスを使用してスキーマがダウンロードされます。

## <a name="xslt-debugger"></a>XSLT デバッガー

XSLT デバッガーは、Visual Studio のマネージド デバッグ エンジンと、<xref:System.Xml> および <xref:System.Xml.Xsl> 名前空間のクラスを使用します。

- XSLT デバッガーは、それぞれの XSLT 変換をサンドボックスで保護されたアプリケーション ドメインで実行します。 コンピューターのコード アクセスに関するセキュリティ ポリシーを使用し、XSLT スタイル シートが置かれている場所に基づいて、アクセス許可の制限が決定されます。 たとえば、インターネット上にあるスタイル シートは最も制限されたアクセス許可を持ち、ユーザーのハード ディスクにコピーされているスタイル シートは "完全な信頼" で実行されます。

- XSLT スタイル シートは、<xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用してコンパイルされます。

- XSLT 式エバリュエーターは、マネージド デバッグ エンジンによって読み込まれます。 マネージド デバッグ エンジンは、すべてのコードがユーザーのローカル コンピューターから実行されることを前提としています。 そのため、<xref:System.Xml.Xsl.XslCompiledTransform> クラスによって XSLT ファイルがユーザーのコンピューターにダウンロードされます。 実行特権で評価が行われる可能性は、制限されたアクセス許可を使用して、新しいアプリケーション ドメインですべての XSLT 変換を実行することにより軽減されます。

## <a name="see-also"></a>関連項目

- [アプリケーション ドメイン](/dotnet/framework/app-domains/application-domains)