---
title: グリフコントロール (ソース管理 VSPackage) |Microsoft Docs
description: 独自のアイコンを使用してソース管理下の項目の状態を示すことができるように、ソース管理 VSPackage にカスタムグリフを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glyphs, source control packages
- source control packages, glyphs
ms.assetid: b9413b08-b3c3-4fc3-a6e0-3dc0db3652d7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3ea9300c96cf63c932d88335c0ca0f9fd4542f72
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99954775"
---
# <a name="glyph-control-source-control-vspackage"></a>グリフコントロール (ソース管理 VSPackage)
ソース管理 Vspackage で使用できる詳細な統合の一部は、ソース管理下の項目の状態を示す独自のグリフを表示する機能です。

## <a name="levels-of-glyph-control"></a>グリフコントロールのレベル
 状態グリフは、 **ソリューションエクスプローラー** や **クラスビュー** などで表示されたときの項目の現在の状態を示すアイコンです。 ソース管理 VSPackage は、2つのレベルのグリフコントロールを実行できます。 このオプションは、IDE によって提供される定義済みのグリフセットに対して、グリフの選択を制限し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] たり、表示されるグリフのカスタムセットを定義したりすることができます。

### <a name="default-set-of-glyphs"></a>既定のグリフセット
 **ソリューションエクスプローラー** の項目に関連付けられている状態グリフを確認するために、プロジェクトはを使用してソース管理から状態グリフを要求し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A> ます。 ソース管理 VSPackage は、IDE によって提供される定義済みのグリフに限定されたグリフの選択を保持することができます。 この場合、VSPackage は、 *vsshell .idl* に定義されているグリフ列挙体を表す値の配列を返します。 詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>」を参照してください。 これは、チェックインされたグリフの南京錠、チェックアウトされたグリフのチェックマークなど、IDE によって設定された定義済みのグリフセットです。

### <a name="custom-set-of-glyphs"></a>グリフのカスタムセット
 ソース管理 VSPackage は、インストールされている独自の外観に独自のグリフを使用できます。 新しいソース管理 VSPackage がアクティブになると、以前のソース管理 VSPackage がまだ読み込まれていても非アクティブであっても、独自のグリフの使用を開始できるようになります。 このモードでは、ソース管理 VSPackage は既存のアイコンを使用して、選択されている場合にとの一貫性を維持することができ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>サービスはインターフェイスをサポートしてい <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> ます。これは、VSPackage が必要に応じて実装でき、IDE によって要求されます。 IDE が要求を行ったときに、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、現在登録されているソース管理 VSPackage からこのインターフェイスを取得しようとします。 インターフェイスが登録されている VSPackage に存在する場合、IDE のカスタムグリフの要求は成功します。それ以外の場合、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE では既定のグリフセットが使用されます。

 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] さまざまなソース管理状態を示すイメージの一覧を取得するために、によって使用されます。 ソース管理 VSPackage は、カスタムグリフのイメージリストへのハンドルを IDE に返します。 IDE はこの時点でイメージリストのコピーを作成し、後で表示するグリフを選択するために使用します。 新しいインターフェイスがサポートされていない場合、または `IVsSccGlyphs::GetCustomGlyphList` メソッドがを返した場合 `E_NOTIMPL` 、IDE はによって提供されるグリフの既定のリストからグリフを取得し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>
- <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>
