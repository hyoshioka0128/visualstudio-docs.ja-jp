---
title: サーバー上のドキュメントのデータにアクセスする
description: Microsoft Office Word または Microsoft Office Excel のオブジェクトモデルを使用せずに、ドキュメントレベルのカスタマイズでデータに対してプログラミングする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], accessing on server
- data access [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e436c7a30708fac0cf59c2e79100cc89dade84b2
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847625"
---
# <a name="access-data-in-documents-on-the-server"></a>サーバー上のドキュメントのデータにアクセスする
  Microsoft Office Word または Microsoft Office Excel のオブジェクトモデルを使用しなくても、ドキュメントレベルのカスタマイズでデータに対してプログラミングを行うことができます。 これは、Word または Excel がインストールされていないサーバー上のドキュメントに含まれているデータにアクセスできることを意味します。 たとえば、サーバー上のコード (たとえば、ページ内) では、 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] ドキュメント内のデータをカスタマイズし、カスタマイズされたドキュメントをエンドユーザーに送信できます。 エンドユーザーがドキュメントを開くと、ソリューションアセンブリのデータバインドコードによって、カスタマイズされたデータがドキュメントにバインドされます。 これが可能なのは、ドキュメント内のデータがユーザーインターフェイスから分離されているためです。 詳細については、「 [ドキュメントレベルのカスタマイズでのキャッシュ](../vsto/cached-data-in-document-level-customizations.md)されたデータ」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="cache-data-for-use-on-a-server"></a>サーバーで使用するデータをキャッシュする
 データオブジェクトをドキュメントにキャッシュするには、デザイン時にデータオブジェクトを属性でマークする <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> か、 `StartCaching` 実行時にホスト項目のメソッドを使用します。 ドキュメント内のデータオブジェクトをキャッシュすると、は、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ドキュメントに格納されている XML 文字列にオブジェクトをシリアル化します。 オブジェクトは、キャッシュに適合するために特定の要件を満たしている必要があります。 詳細については、「 [データのキャッシュ](../vsto/caching-data.md)」を参照してください。

 サーバー側のコードでは、データキャッシュ内の任意のデータオブジェクトを操作できます。 キャッシュされたデータインスタンスにバインドされているコントロールは、ユーザーインターフェイスと同期されるため、クライアントでドキュメントを開いたときに、データに対して行われたすべてのサーバー側の変更が自動的に表示されます。

## <a name="access-data-in-the-cache"></a>キャッシュ内のデータへのアクセス
 たとえば、コンソールアプリケーション、Windows フォームアプリケーション、Web ページなど、Office 外部のアプリケーションからキャッシュ内のデータにアクセスできます。 キャッシュされたデータにアクセスするアプリケーションは、完全に信頼されている必要があります。部分信頼を持つ Web アプリケーションは、Office ドキュメントにキャッシュされているデータを挿入、取得、または変更することはできません。

 データキャッシュには、クラスのプロパティによって公開されるコレクションの階層を介してアクセスでき <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> ます。

- プロパティは、 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> <xref:Microsoft.VisualStudio.Tools.Applications.CachedData> ドキュメントレベルのカスタマイズでキャッシュされたすべてのデータを含むを返します。

- <xref:Microsoft.VisualStudio.Tools.Applications.CachedData> にはそれぞれ、1 つまたは複数の <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> オブジェクトが格納されます。 には、 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> 1 つのクラス内で定義されている、キャッシュされたすべてのデータオブジェクトが含まれます。

- <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> にはそれぞれ、1 つまたは複数の <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> オブジェクトが格納されます。 は、 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> 1 つのキャッシュされたデータオブジェクトを表します。

  Excel ブックプロジェクトのクラスのキャッシュされた文字列にアクセスする方法を次のコード例に示し `Sheet1` ます。 この例は、メソッドに対して用意されている大規模な例の一部です <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> 。

  [!code-csharp[Trin_ServerDocument#12](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#12)]
  [!code-vb[Trin_ServerDocument#12](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#12)]

## <a name="modify-data-in-the-cache"></a>キャッシュ内のデータを変更する
 キャッシュされたデータオブジェクトを変更するには、通常、次の手順を実行します。

1. キャッシュされたオブジェクトの XML 表現をオブジェクトの新しいインスタンスに逆シリアル化します。 XML にアクセスするには、キャッシュされた <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> データオブジェクトを表すのプロパティを使用し <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> ます。

2. このコピーに変更を加えます。

3. 次のいずれかのオプションを使用して、変更されたオブジェクトをデータキャッシュにシリアル化して戻します。

    - 変更を自動的にシリアル化する場合は、メソッドを使用し <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> ます。 このメソッドは **DiffGram** <xref:System.Data.DataSet> 、 <xref:System.Data.DataTable> データキャッシュ内の、、および型指定された dataset オブジェクトをシリアル化するために DiffGram 形式を使用します。 **DiffGram** 形式を指定すると、オフラインドキュメントのデータキャッシュに対する変更がサーバーに正しく送信されます。

    - キャッシュされたデータを変更するために独自のシリアル化を実行する場合は、プロパティに直接書き込むことができ <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> ます。 、 **DiffGram** <xref:System.Data.Common.DataAdapter> <xref:System.Data.DataSet> <xref:System.Data.DataTable> 、または型指定されたデータセットのデータに加えられた変更を使用してデータベースを更新する場合は、DiffGram 形式を指定します。 それ以外の場合、は <xref:System.Data.Common.DataAdapter> 既存の行を変更するのではなく、新しい行を追加してデータベースを更新します。

### <a name="modify-data-without-deserializing-the-current-value"></a>現在の値を逆シリアル化せずにデータを変更する
 場合によっては、最初に現在の値を逆シリアル化せずに、キャッシュされたオブジェクトの値を変更することが必要になることがあります。 たとえば、文字列や整数などの単純型を持つオブジェクトの値を変更する場合や、 <xref:System.Data.DataSet> サーバー上のドキュメントにキャッシュされたを初期化する場合に、この操作を行うことができます。 このような場合は、最初にキャッシュされた <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> オブジェクトの現在の値を逆シリアル化せずに、メソッドを使用できます。

 Excel ブックプロジェクトのクラスでキャッシュされた文字列の値を変更する方法を次のコード例に示し `Sheet1` ます。 この例は、メソッドに対して用意されている大規模な例の一部です <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> 。

 [!code-csharp[Trin_ServerDocument#11](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#11)]
 [!code-vb[Trin_ServerDocument#11](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#11)]

### <a name="modify-null-values-in-the-data-cache"></a>データキャッシュ内の null 値を変更する
 ドキュメントを保存して閉じた場合、値が **null** のオブジェクトはデータキャッシュに格納されません。 キャッシュされたデータを変更すると、次のようないくつかの影響があります。

- データキャッシュ内のオブジェクトを **null** 値に設定すると、ドキュメントを開いたときにデータキャッシュ内のすべてのオブジェクトが自動的に **null** に設定され、ドキュメントを保存して閉じたときにデータキャッシュ全体がクリアされます。 つまり、キャッシュされたオブジェクトはすべてデータキャッシュから削除され、コレクションは <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 空になります。

- データキャッシュに **null** オブジェクトを含むソリューションをビルドし、ドキュメントを初めて開く前にクラスを使用してこれらのオブジェクトを初期化する場合は <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 、データキャッシュ内のすべてのオブジェクトを初期化する必要があります。 オブジェクトの一部だけを初期化すると、ドキュメントを開いたときにすべてのオブジェクトが **null** に設定され、ドキュメントを保存して閉じたときにデータキャッシュ全体がクリアされます。

## <a name="access-typed-datasets-in-the-cache"></a>キャッシュ内の型指定されたデータセットへのアクセス
 Office ソリューションと、Windows フォームアプリケーションやプロジェクトなど、Office 以外のアプリケーションから、型指定されたデータセットのデータにアクセスする場合は、 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 両方のプロジェクトで参照される別のアセンブリに、型指定されたデータセットを定義する必要があります。 **データソース構成** ウィザードまたは **データセットデザイナー** を使用して、型指定されたデータセットを各プロジェクトに追加する場合、.NET Framework では、2つのプロジェクト内の型指定されたデータセットを異なる型として扱います。 型指定されたデータセットの作成の詳細については、「 [Visual Studio でのデータセットの作成と構成](../data-tools/create-and-configure-datasets-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [サーバー上のドキュメントのデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)
- [ドキュメントレベルのカスタマイズでのキャッシュされたデータ](../vsto/cached-data-in-document-level-customizations.md)