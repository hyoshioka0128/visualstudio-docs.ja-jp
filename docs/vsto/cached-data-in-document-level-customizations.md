---
title: ドキュメントレベルのカスタマイズでのキャッシュされたデータ
description: データをデータキャッシュとして埋め込むことで、ドキュメントレベルのカスタマイズで Visual Studio がビューからデータを分離する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data islands [Office development in Visual Studio]
- view [Office development in Visual Studio]
- caching data [Office development in Visual Studio], about caching data
- data caching [Office development in Visual Studio], about data caching
- data [Office development in Visual Studio], cache
- data [Office development in Visual Studio], document-level solutions
- document-level customizations [Office development in Visual Studio], data model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f1c383b5367b2966b9fd082b2d47570264b4d191
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955776"
---
# <a name="cached-data-in-document-level-customizations"></a>ドキュメントレベルのカスタマイズでのキャッシュされたデータ
  ドキュメントレベルのカスタマイズの主な目的は、Office ドキュメントのビューからデータを分離することです。 データとは、数字やテキストを含む、ドキュメントに格納されている情報を指します。 ビューは、ユーザーインターフェイスと Microsoft Office Word および Microsoft Office Excel のオブジェクトモデルを参照します。

 Visual Studio では、データをデータ *アイランド* として埋め込む (データ *キャッシュ* とも呼ばれる) ことによって、ドキュメントレベルのカスタマイズでビューのデータを分離します。 Word または Excel を起動せずに、直接データの読み取りや変更を行うことができます。 これは、Microsoft Office がインストールされていないサーバー上のドキュメントのデータを変更する必要がある場合に便利です。 Word および Excel は、クライアント環境での使用を目的としています。サーバー上で実行するように設計されていません。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 ドキュメントレベルのカスタマイズの詳細については、「 [Office solutions development の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md) 」および「 [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

## <a name="understand-the-cached-data-programming-model"></a>キャッシュされたデータプログラミングモデルについて
 データアイランドには、ソリューション内の特定の要件を満たす任意のオブジェクトを含めることができます。 これらのオブジェクトには、 <xref:System.Data.DataSet> オブジェクト、 <xref:System.Data.DataTable> オブジェクト、およびクラスによってシリアル化できるその他のオブジェクトが含ま <xref:System.Xml.Serialization.XmlSerializer> れます。 詳細については、「 [データのキャッシュ](../vsto/caching-data.md)」を参照してください。

 キャッシュされたデータのビューを提供するには、ドキュメント上のコントロールと *ホストコントロール* をデータアイランド内のオブジェクトにバインド Windows フォームます。 データアイランドとデータバインドコントロールの間のデータバインディングでは、2つの同期が維持されます。 また、コントロールに依存しないデータに検証コードを追加することもできます。 詳細については、「 [データを Office ソリューションのコントロールにバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

 ホストコントロールは、Excel および Word オブジェクトモデルのネイティブオブジェクトの拡張バージョンです。 ネイティブオブジェクトとは異なり、ホストコントロールはマネージデータオブジェクトに直接バインドできます。 詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md) 」および「 [Office ドキュメントのコントロールの Windows フォームの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)」を参照してください。

## <a name="access-cached-data-on-the-server"></a>サーバー上のキャッシュされたデータへのアクセス
 ドキュメント内のキャッシュされたデータにアクセスするには、クラスを使用でき <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> ます。 このクラスは、の一部であり、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] Excel または Word を実行せずにサーバーで使用できます。 キャッシュされたデータを変更した後にユーザーがドキュメントを開くと、そのデータにバインドされているすべてのコントロールが自動的に変更に同期され、更新されたデータがユーザーに表示されます。 詳細については、「 [サーバー上のドキュメントのデータにアクセス](../vsto/accessing-data-in-documents-on-the-server.md)する」を参照してください。

 サーバー上のデータに書き込むために Excel と Word は必要ありません。クライアントで表示するためにのみ必要です。 Excel と Word をサーバーにインストールする必要もありません。 これにより、スケーラビリティが向上し、データアイランドを含むドキュメントのバッチ処理を高速に実行できるようになります。

## <a name="data-caching-for-offline-use"></a>オフラインで使用するためのデータキャッシュ
 データアイランドにデータを格納すると、オフラインのシナリオに対応できます。 ユーザーが最初にドキュメントを開くか、サーバーからドキュメントを要求すると、データアイランドに最新のデータが格納されます。 データアイランドはドキュメントにキャッシュされ、その後オフラインで使用できるようになります。 ライブ接続が使用できない場合でも、ユーザー (およびコード) はデータを操作できます。 ユーザーが再接続すると、データに対する変更をサーバーデータソースに反映させることができます。

## <a name="cached-data-and-custom-xml-parts-compared"></a>キャッシュされたデータとカスタム XML 部分の比較
 カスタム XML 部分は、ドキュメントに XML の任意の部分を格納する方法として、2007 Microsoft Office システムで導入されました。 カスタム XML 部分はデータキャッシュと同じシナリオの多くで役に立ちますが、データアイランドとカスタム XML 部分にはいくつかの違いがあります。 カスタム XML 部分の詳細については、「 [カスタム xml 部分の概要](../vsto/custom-xml-parts-overview.md)」を参照してください。

 次の表に、相違点と類似点の一部を示します。

|質問/特性|データ キャッシュ|カスタム XML 部分|
|-|----------------|----------------------|
|どの Office アプリケーションでこれらを使用できますか。|次のアプリケーションのドキュメントレベルのカスタマイズ:<br /><br /> -Excel<br />-Word|次のアプリケーションのドキュメントレベルおよびアプリケーションレベルのソリューション:<br /><br /> -Excel<br />-PowerPoint<br />-Word|
|どのような種類のデータを格納できますか。|特定の要件を満たす、カスタマイズアセンブリ内の任意のパブリックオブジェクト。 詳細については、「 [データのキャッシュ](../vsto/caching-data.md)」を参照してください。|任意の XML データ。|
|Microsoft Office アプリケーションを起動せずにデータにアクセスできますか。|はい。によって <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 提供されるクラスを使用し [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。|はい。名前空間のクラスを使用する <xref:System.IO.Packaging> か、OPEN XML FORMAT SDK を使用します。|

## <a name="see-also"></a>関連項目
- [Office ソリューションのデータ](../vsto/data-in-office-solutions.md)
- [Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)
