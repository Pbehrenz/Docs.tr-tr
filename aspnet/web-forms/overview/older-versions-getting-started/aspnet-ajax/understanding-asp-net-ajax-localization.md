---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: "ASP.NET AJAX yerelleştirme anlama | Microsoft Docs"
author: scottcate
description: "Yerelleştirme tasarlama ve uygulama ya da bir uygulama bileşeni belirli bir dil ve kültür için destek tümleştirme işlemidir. MIC..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2008
ms.topic: article
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 5b801586ea77af78284f780fe47fe09cafb984af
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-aspnet-ajax-localization"></a><span data-ttu-id="2b6a2-104">ASP.NET AJAX yerelleştirme anlama</span><span class="sxs-lookup"><span data-stu-id="2b6a2-104">Understanding ASP.NET AJAX Localization</span></span>
====================
<span data-ttu-id="2b6a2-105">tarafından [Scott göstermek](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="2b6a2-105">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="2b6a2-106">PDF indirin</span><span class="sxs-lookup"><span data-stu-id="2b6a2-106">Download PDF</span></span>](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> <span data-ttu-id="2b6a2-107">Yerelleştirme tasarlama ve uygulama ya da bir uygulama bileşeni belirli bir dil ve kültür için destek tümleştirme işlemidir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-107">Localization is the process of designing and integrating support for a specific language and culture into an application or an application component.</span></span> <span data-ttu-id="2b6a2-108">Microsoft ASP.NET platformunu standart .NET yerelleştirme modeli tümleştirerek standart ASP.NET uygulamaları için yerelleştirme için kapsamlı destek sağlar; Microsoft AJAX Framework yerelleştirme gerçekleştirilebilir çeşitli senaryoları desteklemek için tümleşik modelini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-108">The Microsoft ASP.NET platform provides extensive support for localization for standard ASP.NET applications by integrating the standard .NET localization model; the Microsoft AJAX Framework utilize the integrated model to support the diverse scenarios in which localization can be performed.</span></span>


## <a name="introduction"></a><span data-ttu-id="2b6a2-109">Giriş</span><span class="sxs-lookup"><span data-stu-id="2b6a2-109">Introduction</span></span>

<span data-ttu-id="2b6a2-110">Microsoft ASP.NET teknolojisi bir nesne yönelimli ve olay kaynaklı programlama modeli getirir ve derlenmiş kod yararları birleştirmiştir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-110">Microsoft's ASP.NET technology brings an object-oriented and event-driven programming model and unites it with the benefits of compiled code.</span></span> <span data-ttu-id="2b6a2-111">Bununla birlikte, kendi sunucu tarafı işleme modelini birkaç dezavantajları birçok Microsoft AJAX Hizmetleri .NET Framework yalıtır System.Web.Extensions ad alanı içinde sunulan yeni özelliklerle çözülebilir teknolojisinde devralınmış vardır 3.5.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-111">However, its server-side processing model has several drawbacks inherent in the technology, many of which can be addressed by the new features included in the System.Web.Extensions namespace, which encapsulates the Microsoft AJAX Services in the .NET Framework 3.5.</span></span> <span data-ttu-id="2b6a2-112">Bu uzantılar birçok zengin istemci özellikleri, ASP.NET 2.0 AJAX uzantıları parçası, ancak Framework temel sınıf kitaplığı şimdi bir parçası olarak önceden kullanılabilir etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-112">These extensions enable many rich client features, previously available as part of the ASP.NET 2.0 AJAX Extensions, but now part of the Framework Base Class Library.</span></span> <span data-ttu-id="2b6a2-113">Web Hizmetleri aracılığıyla istemci komut dosyası (profil oluşturma API'si ASP.NET dahil) erişim olanağı bir tam sayfa yenileme gerek kalmadan sayfaların kısmi işleme denetimleri ve bu ad alanındaki özellikleri ekleyin ve kapsamlı bir istemci-tarafı API birçok yansıtmak üzere tasarlanmış ASP.NET sunucu tarafı denetimi kümesinde görüldüğü denetim düzenleri.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-113">Controls and features in this namespace include partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="2b6a2-114">Bu teknik Microsoft AJAX Framework ve Microsoft AJAX komut dosyası kitaplığı, mevcut iş gereksinimini yerelleştirme desteği ve Web yerelleştirme için zaten tümleşik destek gözden geçirme bağlamında yerelleştirme özelliklerini inceler .NET Framework tarafından sağlanan uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-114">This whitepaper examines the localization features present in the Microsoft AJAX Framework and Microsoft AJAX Script Library, in the context of business need for localization support and reviewing already-integrated support for localization in web applications provided by the .NET Framework.</span></span> <span data-ttu-id="2b6a2-115">Microsoft AJAX komut dosyası kitaplığı tümleşik IDE desteği ve paylaşılabilir kaynak türü sağlayan önceden .NET uygulamaları tarafından kullanılan .resx dosya biçimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-115">The Microsoft AJAX Script Library utilizes the .resx file format already used by .NET applications, which provides integrated IDE support and a shareable resource type.</span></span>

<span data-ttu-id="2b6a2-116">Bu teknik temel Microsoft Visual Studio 2008 Beta 2 sürümü üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-116">This whitepaper is based on the Beta 2 release of Microsoft Visual Studio 2008.</span></span> <span data-ttu-id="2b6a2-117">Bu Teknik İnceleme de Visual Studio 2008 ile değil Visual Web Developer Express, çalışma ve Visual Studio kullanıcı arabirimi göre izlenecek yollar sağlar varsayar.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-117">This whitepaper also assumes that you will be working with Visual Studio 2008, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="2b6a2-118">Bazı kod örnekleri Visual Web Developer Express kullanılamayabilir proje şablonları yararlanacak olan.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-118">Some code samples will utilize project templates that may be unavailable in Visual Web Developer Express.</span></span>

## <a name="the-need-for-localization"></a><span data-ttu-id="2b6a2-119">*Yerelleştirme gereksinimini*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-119">*The Need for Localization*</span></span>

<span data-ttu-id="2b6a2-120">Özellikle kuruluş uygulama geliştiricileri ve Bileşen geliştiriciler için kültürlere ve dilleri arasındaki farkların farkında Araçlar oluşturma yeteneği giderek çıkmıştır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-120">Particularly for enterprise application developers and component developers, the ability to create tools that can be aware of the differences between cultures and languages has become increasingly necessary.</span></span> <span data-ttu-id="2b6a2-121">İstemcinin yerel uyarlama olanağı ile bileşenlerini tasarlamayı Geliştirici verimliliğini artırır ve genel olarak çalışması için bir bileşen uyarlama için gereken iş miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-121">Designing components with the ability to adapt to the locale of the client increases developer productivity and reduces the amount of work required for the adaptation of a component to function globally.</span></span>

<span data-ttu-id="2b6a2-122">Yerelleştirme tasarlama ve uygulama ya da bir uygulama bileşeni belirli bir dil ve kültür için destek tümleştirme işlemidir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-122">Localization is the process of designing and integrating support for a specific language and culture into an application or an application component.</span></span> <span data-ttu-id="2b6a2-123">Microsoft ASP.NET platformunu standart .NET yerelleştirme modeli tümleştirerek standart ASP.NET uygulamaları için yerelleştirme için kapsamlı destek sağlar; Microsoft AJAX Framework yerelleştirme gerçekleştirilebilir çeşitli senaryoları desteklemek için tümleşik modelini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-123">The Microsoft ASP.NET platform provides extensive support for localization for standard ASP.NET applications by integrating the standard .NET localization model; the Microsoft AJAX Framework utilize the integrated model to support the diverse scenarios in which localization can be performed.</span></span> <span data-ttu-id="2b6a2-124">Microsoft AJAX çerçevesiyle komut dosyaları ya da uydu derlemelerini dağıtılan ya da bir statik dosya sistemi yapısı kullanılarak yerelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-124">With the Microsoft AJAX Framework, scripts can either be localized by being deployed into satellite assemblies, or by utilizing a static file system structure.</span></span>

## <a name="embedding-scripts-with-satellite-assemblies"></a><span data-ttu-id="2b6a2-125">*Uydu derlemeleri kodlarla katıştırma*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-125">*Embedding Scripts with Satellite Assemblies*</span></span>

<span data-ttu-id="2b6a2-126">Standart .NET Framework yerelleştirme stratejisi ile tutarlı, kaynakları uydu derlemeleri dahil edilebilir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-126">Consistent with the standard .NET Framework localization strategy, resources can be included in satellite assemblies.</span></span> <span data-ttu-id="2b6a2-127">Uydu derlemeleri sağlayan çeşitli avantajları ikili - geleneksel kaynak eklenmesi üzerinden verilen tüm yerelleştirme büyük görüntü güncelleştirmeden güncelleştirilebilir, uydu derlemelerini içine yükleyerek ek yerelleştirmeler dağıtılabilir Proje klasörünü ve uydu derlemelerini yeniden ana proje derlemesinin neden olmadan dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-127">Satellite assemblies provide several advantages over traditional resource inclusion in binaries - any given localization can be updated without updating the larger image, additional localizations can be deployed simply by installing satellite assemblies into the project folder, and satellite assemblies can be deployed without causing a reload of the main project assembly.</span></span> <span data-ttu-id="2b6a2-128">ASP.NET projeleri, özellikle de bu artımlı güncelleştirmeler tarafından kullanılan sistem kaynaklarının miktarını önemli ölçüde azaltabilir çünkü yararlıdır ve en düşük düzeyde üretim Web sitesi kullanım kesintiye uğratır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-128">Particularly in ASP.NET projects, this is beneficial because it can significantly reduce the amount of system resources used by incremental updates, and minimally disrupts production website usage.</span></span>

<span data-ttu-id="2b6a2-129">Komut dosyaları katıştırılmış derlemelerine dahil ederek derlemesini derleme zamanında dahil dosyaları .resx yönetilen (veya .resources derlenmiş).</span><span class="sxs-lookup"><span data-stu-id="2b6a2-129">Scripts are embedded into assemblies by including them in managed .resx (or compiled .resources) files, which are included into the assembly at compile-time.</span></span> <span data-ttu-id="2b6a2-130">Kaynaklarını ardından AJAX çalışma oluşturulan kod, derleme düzeyi öznitelikleri aracılığıyla üzerinden betik uygulama için kullanılabilir hale getirilir</span><span class="sxs-lookup"><span data-stu-id="2b6a2-130">Their resources are then made available to the script application through AJAX runtime-generated code, via assembly-level attributes</span></span>

<span data-ttu-id="2b6a2-131">*Katıştırılmış komut dosyaları için adlandırma kuralları*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-131">*Naming Conventions for Embedded Script Files*</span></span>

<span data-ttu-id="2b6a2-132">Microsoft AJAX Framework komut dosyası Yönetimi dağıtım ve komut dosyaları sınama kullanılmak üzere çeşitli seçenekleri destekler ve bu seçenekler kolaylaştırmak için yönergeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-132">The Microsoft AJAX Framework script management supports a variety of options for use in deployment and testing of scripts, and guidelines are provided to facilitate these options.</span></span>

<span data-ttu-id="2b6a2-133">*Hata ayıklama kolaylaştırmak için:*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-133">*To facilitate debugging:*</span></span>

<span data-ttu-id="2b6a2-134">Yayın (üretim) komut dosyaları dahil `.debug` filename niteleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-134">Release (production) scripts should not include the `.debug` qualifier in the filename.</span></span> <span data-ttu-id="2b6a2-135">Hata ayıklama içermesi için tasarlanmış betikleri `.debug` dosya.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-135">Scripts designed for debugging should include `.debug` in the filename.</span></span>

<span data-ttu-id="2b6a2-136">*Yerelleştirme kolaylaştırmak için:*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-136">*To facilitate localization:*</span></span>

<span data-ttu-id="2b6a2-137">Nötr kültür komut dosyaları, dosya adına herhangi bir kültür tanımlayıcısı içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-137">Neutral-culture scripts should not include any culture identifier in the name of the file.</span></span> <span data-ttu-id="2b6a2-138">Yerelleştirilmiş kaynakları içeren komut dosyaları için ISO dil kodu dosya adı belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-138">For scripts that contain localized resources, the ISO language code should be specified in the file name.</span></span> <span data-ttu-id="2b6a2-139">Örneğin, `es-CO` İspanyolca, Columbia anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-139">For example, `es-CO` stands for Spanish, Columbia.</span></span>

<span data-ttu-id="2b6a2-140">Aşağıdaki tabloda adlandırma kuralları örnekleri içeren dosya özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-140">The following table summarizes the file naming conventions with examples:</span></span>

| <span data-ttu-id="2b6a2-141">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="2b6a2-141">Filename</span></span> | <span data-ttu-id="2b6a2-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2b6a2-142">Meaning</span></span> |
| --- | --- |
| <span data-ttu-id="2b6a2-143">Script.js</span><span class="sxs-lookup"><span data-stu-id="2b6a2-143">Script.js</span></span> | <span data-ttu-id="2b6a2-144">Bir yayın sürümü kültür Tarafsız komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-144">A release-version culture-neutral script.</span></span> |
| <span data-ttu-id="2b6a2-145">Script.Debug.js</span><span class="sxs-lookup"><span data-stu-id="2b6a2-145">Script.debug.js</span></span> | <span data-ttu-id="2b6a2-146">Hata ayıklama sürümü kültür Tarafsız komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-146">A debug-version culture-neutral script.</span></span> |
| <span data-ttu-id="2b6a2-147">Script.en US.js</span><span class="sxs-lookup"><span data-stu-id="2b6a2-147">Script.en-US.js</span></span> | <span data-ttu-id="2b6a2-148">Bir yayın sürümü İngilizce, Amerika Birleşik Devletleri komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-148">A release version English, United States script.</span></span> |
| <span data-ttu-id="2b6a2-149">Script.Debug.es CO.js</span><span class="sxs-lookup"><span data-stu-id="2b6a2-149">Script.debug.es-CO.js</span></span> | <span data-ttu-id="2b6a2-150">Bir hata ayıklama sürümü İspanyolca, Columbia komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-150">A debug-version Spanish, Columbia script.</span></span> |

## <a name="walkthrough-create-an-localized-embedded-script"></a><span data-ttu-id="2b6a2-151">İzlenecek yol: bir yerelleştirilmiş, katıştırılmış komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b6a2-151">Walkthrough: Create an Localized, Embedded Script</span></span>

<span data-ttu-id="2b6a2-152">*Lütfen unutmayın: Visual Web Developer Express Sınıf Kitaplığı projelerinde için bir proje şablonu içermez gibi bu kılavuzda Visual Studio 2008 kullanılmasını gerektirir.*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-152">*Please note: this walkthrough requires the use of Visual Studio 2008 as Visual Web Developer Express does not include a project template for class library projects.*</span></span>

1. <span data-ttu-id="2b6a2-153">Yeni bir Web sitesi projesi, ASP.NET AJAX tümleşik uzantılarıyla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-153">Create a new Web Site project with ASP.NET AJAX Extensions integrated.</span></span> <span data-ttu-id="2b6a2-154">Başka bir projeye, LocalizingResources adlı çözüm içinde bir sınıf kitaplığı proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-154">Create another project, a Class Library project, within the solution called LocalizingResources.</span></span>
2. <span data-ttu-id="2b6a2-155">.Resx kaynakları dosyaları DeletionResources.resx ve DeletionResources.es.resx adlı yanı sıra VerifyDeletion.js LocalizingResources projeye adlı Jscript dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-155">Add a Jscript file called VerifyDeletion.js to the LocalizingResources project, as well as .resx resources files called DeletionResources.resx and DeletionResources.es.resx.</span></span> <span data-ttu-id="2b6a2-156">Eski kültür Tarafsız kaynakları içerecek; İkinci İspanyolca dil kaynakları içerir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-156">The former will contain culture-neutral resources; the latter will contain Spanish-language resources.</span></span>
3. <span data-ttu-id="2b6a2-157">VerifyDeletion.js için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-157">Add the following code to VerifyDeletion.js:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

<span data-ttu-id="2b6a2-158">JavaScript Regex sözdizimi, tek eğik metinde alışık olanlar için (önceki örnekte /FILENAME/ örneğidir) RegExp nesnesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-158">For those unfamiliar with JavaScript Regex syntax, text within single forward slashes (in the previous example, /FILENAME/ is an example) denotes a RegExp object.</span></span> <span data-ttu-id="2b6a2-159">MSDN Kitaplığı kapsamlı bir JavaScript başvurusu içeriyor ve JavaScript yerel nesneleri kaynakları çevrimiçi olarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-159">The MSDN Library contains an extensive JavaScript reference, and resources on JavaScript native objects can be found online.</span></span>

1. <span data-ttu-id="2b6a2-160">Aşağıdaki kaynak dizeleri için DeletionResources.resx ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-160">Add the following resource strings to DeletionResources.resx:</span></span> 

    <span data-ttu-id="2b6a2-161">**VerifyDelete**: FILENAME silmek istediğinizden emin misiniz?</span><span class="sxs-lookup"><span data-stu-id="2b6a2-161">**VerifyDelete**: Are you sure you want to delete FILENAME?</span></span>

    <span data-ttu-id="2b6a2-162">**Silinen**: FILENAME silinmiş.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-162">**Deleted**: FILENAME has been deleted.</span></span>

1. <span data-ttu-id="2b6a2-163">Aşağıdaki kaynak dizeleri için DeletionResources.es.resx ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-163">Add the following resource strings to DeletionResources.es.resx:</span></span> 

    <span data-ttu-id="2b6a2-164">**VerifyDelete**: Est seguro que desee quitar FILENAME?</span><span class="sxs-lookup"><span data-stu-id="2b6a2-164">**VerifyDelete**: Est seguro que desee quitar FILENAME?</span></span>

    <span data-ttu-id="2b6a2-165">**Silinen**: FILENAME se ha quitado.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-165">**Deleted**: FILENAME se ha quitado.</span></span>
2. <span data-ttu-id="2b6a2-166">Aşağıdaki kod satırlarını AssemblyInfo dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-166">Add the following lines of code to the AssemblyInfo file:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. <span data-ttu-id="2b6a2-167">System.Web ve System.Web.Extensions başvuruları LocalizingResources projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-167">Add references to System.Web and System.Web.Extensions to the LocalizingResources project.</span></span>
2. <span data-ttu-id="2b6a2-168">Web sitesi projeden LocalizingResources projesine bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-168">Add a reference to the LocalizingResources project from the Web Site project.</span></span>
3. <span data-ttu-id="2b6a2-169">Web sitesi projesini altında default.aspx ScriptManager denetimi ile aşağıdaki ek biçimlendirme güncelleştirmek:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-169">In default.aspx, under the Web Site project, update the ScriptManager control with the following additional markup:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. <span data-ttu-id="2b6a2-170">Herhangi bir yere sayfasında default.aspx bu biçimlendirme ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-170">In default.aspx, anywhere on the page, include this markup:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. <span data-ttu-id="2b6a2-171">F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-171">Press F5.</span></span> <span data-ttu-id="2b6a2-172">İstenirse, hata ayıklamayı etkinleştir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-172">If prompted, enable debugging.</span></span> <span data-ttu-id="2b6a2-173">Sayfa yüklendiğinde Sil düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-173">When the page is loaded, press the Delete button.</span></span> <span data-ttu-id="2b6a2-174">(Bilgisayarınızı İspanyolca dil kaynakları tercih için varsayılan olarak ayarlanmadığı sürece), İngilizce onaylamanız istenir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-174">Note that you are prompted in English (unless your computer is set to prefer Spanish-language resources by default) for confirmation.</span></span>
2. <span data-ttu-id="2b6a2-175">Tarayıcı penceresini kapatın ve için default.aspx dönün.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-175">Close the browser window and return to default.aspx.</span></span> <span data-ttu-id="2b6a2-176">İçinde @Page üstbilgi yönergesi, es-ES kültür ve UICulture Değiştir otomatik.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-176">In the @Page header directive, replace auto for Culture and UICulture with es-ES.</span></span> <span data-ttu-id="2b6a2-177">Tarayıcıda web uygulamasını yeniden yeniden başlatmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-177">Press F5 again to launch the web application in the browser again.</span></span> <span data-ttu-id="2b6a2-178">Bu süre, İspanyolca dosyasında silmeniz istenecektir dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-178">This time, note that you are prompted to delete the file in Spanish:</span></span>


[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

<span data-ttu-id="2b6a2-179">([Tam boyutlu görüntüyü görüntülemek için tıklatın](understanding-asp-net-ajax-localization/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2b6a2-179">([Click to view full-size image](understanding-asp-net-ajax-localization/_static/image3.png))</span></span>


[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

<span data-ttu-id="2b6a2-180">([Tam boyutlu görüntüyü görüntülemek için tıklatın](understanding-asp-net-ajax-localization/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2b6a2-180">([Click to view full-size image](understanding-asp-net-ajax-localization/_static/image6.png))</span></span>


<span data-ttu-id="2b6a2-181">Bu kılavuz çeşitli Çeşitlemeler olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-181">Note that there are several variations for this walkthrough.</span></span> <span data-ttu-id="2b6a2-182">Örneğin, komut dosyaları ScriptManager denetimi ile programlı olarak sayfa yükleme sırasında kaydı yapılamadı.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-182">For instance, scripts could be registered with the ScriptManager control programmatically during page load.</span></span>

## <a name="including-a-static-script-file-structure"></a><span data-ttu-id="2b6a2-183">*Statik betik dosya yapısı dahil*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-183">*Including a Static Script File Structure*</span></span>

<span data-ttu-id="2b6a2-184">Statik komut dosyaları için dağıtım kullanırken, devralınan .NET yerelleştirme şeması kullanarak avantajlarından bazıları kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-184">When using static script files for deployment, you lose some of the benefits of using the inherent .NET localization scheme.</span></span> <span data-ttu-id="2b6a2-185">Öncelikle, komut dosyası kaynak dosyaları dahil olmak üzere oluşturulan otomatik türü kaybetmeniz görülebilir; Yukarıdaki kılavuzda, örneğin, kaynakları ileti ScriptManager denetiminden adlı bir otomatik olarak oluşturulan türü tarafından ortaya.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-185">Primarily visible is that you lose the automatic type generated from including script resource files; in the above walkthrough, for example, resources were exposed by an automatically-generated type called Message from the ScriptManager control.</span></span>

<span data-ttu-id="2b6a2-186">Ancak, bir statik betik dosya yapısı kullanmanın bazı avantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-186">There are, however, some benefits to using a static script file structure.</span></span> <span data-ttu-id="2b6a2-187">Güncelleştirmeleri yeniden derlenmesi ve uydu derlemelerini gerek olmadan gerçekleştirilebilir ve bir statik dosya yapısı kullanımını da alınmamış işlevselliği küçük bir parçasını bileşeni ile tümleştirmek için katıştırılmış betik geçersiz kılmak için yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-187">Updates can be performed without recompiling and redeploying satellite assemblies, and the use of a static file structure can also be done to override embedded script, to integrate a minor piece of functionality that may not have been shipped with a component.</span></span>

<span data-ttu-id="2b6a2-188">Microsoft betik kaynaklarınızı otomatik olarak proje derleme sırasında oluşturarak sürüm denetimi sorunu önlemenin önerir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-188">Microsoft recommends avoiding a version control issue by automatically generating your script resources during project compilation.</span></span> <span data-ttu-id="2b6a2-189">Kapsamlı bir kod temel korurken kod değişiklikleri yerelleştirilmiş her komut dosyasında yansıtılır sağlamak giderek daha çok zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-189">When maintaining an extensive script code base, it can become increasingly difficult to ensure that code changes are reflected in each localized script.</span></span> <span data-ttu-id="2b6a2-190">Alternatif olarak, yalnızca tek bir mantık betik ve birden fazla yerelleştirme komut dosyası, proje oluşturulurken dosyaları birleştirme bulundurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-190">As an alternative, you can simply maintain one logic script and multiple localization scripts, merging the files while building the project.</span></span>

<span data-ttu-id="2b6a2-191">Bildirimli olarak eklenecek kaynakları olmadığından statik komut dosyaları olmalıdır ekleyerek ya da başvurulan `<asp:ScriptElement>` öğeler bir alt öğesi olarak `<Scripts>` etiketi ScriptManager denetimi veya program aracılığıyla ekleyerek `ScriptReference` nesneleri için `Scripts` özelliği `ScriptManager` çalışma zamanında sayfasında denetimi.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-191">Because there are not resources to declaratively include, static script files should be referenced either by adding `<asp:ScriptElement>` elements as a child of the `<Scripts>` tag of the ScriptManager control, or by programmatically adding `ScriptReference` objects to the `Scripts` property of the `ScriptManager` control on the page at runtime.</span></span>

## <a name="the-scriptmanager-and-its-role-in-localization"></a><span data-ttu-id="2b6a2-192">*ScriptManager ve onun rolünde yerelleştirme*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-192">*The ScriptManager and its Role in Localization*</span></span>

<span data-ttu-id="2b6a2-193">ScriptManager yerelleştirilmiş uygulamalar için birkaç otomatik davranışları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2b6a2-193">The ScriptManager enables several automatic behaviors for localized applications:</span></span>

- <span data-ttu-id="2b6a2-194">Otomatik olarak ayarlar ve adlandırma kurallarına göre komut dosyaları da bulur; örneği için hata ayıklama etkin betikleri hata ayıklama modunda yükler ve komut dosyaları tarayıcının kullanıcı arabirimi seçimine göre yükleri yerelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-194">It automatically locates script files based on settings and naming conventions; for instance, it loads debug-enabled scripts when in debugging mode, and loads localized scripts based on the browser's user interface selection.</span></span>
- <span data-ttu-id="2b6a2-195">Özel kültürler dahil olmak üzere kültürler tanımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-195">It enables the definition of cultures, including custom cultures.</span></span>
- <span data-ttu-id="2b6a2-196">Bu komut dosyaları sıkıştırma HTTP üzerinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-196">It enables the compression of script files over HTTP.</span></span>
- <span data-ttu-id="2b6a2-197">Birçok istekleri verimli bir şekilde yönetmek için komut dosyaları önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-197">It caches scripts to efficiently manage many requests.</span></span>
- <span data-ttu-id="2b6a2-198">Komut dosyaları şifrelenmiş bir URL cmdlet'ine yönelterek yöneltme bir katmanı ekler.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-198">It adds a layer of indirection to scripts by piping them through an encrypted URL.</span></span>

<span data-ttu-id="2b6a2-199">Komut dosyası başvuruları ScriptManager denetimi program aracılığıyla veya bildirim temelli biçimlendirme tarafından eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-199">Script references can be added to the ScriptManager control either programmatically or by declarative markup.</span></span> <span data-ttu-id="2b6a2-200">Düzeltmeleri gönderilen gibi komut dosyasının adını olasılıkla değiştirmez gibi bildirim temelli biçimlendirme web sitesi projesini kendisi dışında katıştırılmış derlemeleri komut dosyaları ile çalışırken, özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-200">Declarative markup is particularly useful when working with scripts embedded in assemblies other than the web site project itself, as the name of the script will likely not change as revisions are pushed through.</span></span>

## <a name="summary"></a><span data-ttu-id="2b6a2-201">Özet</span><span class="sxs-lookup"><span data-stu-id="2b6a2-201">Summary</span></span>

<span data-ttu-id="2b6a2-202">Web uygulamaları, daha büyük bir izleyici ulaşması arttıkça, daha geniş kültürler ve toplulukları ulaşabilmesi için gereken iş modeli çekirdek olur; yabancı para ile mücadele etmek e-ticaret web uygulamaları gerekir, içerik yönetim sistemleri içeriklerini ancak aynı zamanda bunların Gezinti ipuçları ve form alanlarını diğer dillere ve şirketler bu ihtiyacı olduğunu bilmeniz yapabileceksiniz değil yalnızca mevcut olması gerekir erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-202">As web applications grow to reach a larger audience, the need to be able to reach broader cultures and communities becomes core to a business model; e-commerce web applications need to be able to deal with foreign currencies, content management systems need to be able to not only present their content but also their navigation hints and form fields in other languages, and companies need to know that this need is accessible.</span></span>

<span data-ttu-id="2b6a2-203">.NET Framework uydu derlemelerini ve XML kaynak (.resx) dosyaları bir Tekdüzen Kaynak dizeleri ve görüntüleri Ara şekilde sunmak için kullanan bir zengin yerelleştirme framework doğası gereği destekler.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-203">The .NET Framework intrinsically supports a rich localization framework, utilizing satellite assemblies and XML resource (.resx) files to present a uniform way to look up resource strings and images.</span></span> <span data-ttu-id="2b6a2-204">Microsoft AJAX Framework ve Microsoft AJAX komut dosyası kitaplığı gibi ASP.NET AJAX uzantıları bu programlama modeli için istemci tarafı koda kolay kaynak dize aramaları etkinleştirme desteği.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-204">The ASP.NET AJAX Extensions, including the Microsoft AJAX Framework and Microsoft AJAX Script Library, provide support for this programming model into client-side code, enabling easy resource string lookups.</span></span> <span data-ttu-id="2b6a2-205">Dosya adları belirli bir adlandırma şeması izlediğiniz sürece otomatik eklenmesi ScriptResource.axd aracılığıyla komut dosyası kaynakları (gerçek .js dosyaları), uydu derlemelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-205">Satellite assemblies support the automatic inclusion of script resources (actual .js files) through ScriptResource.axd as long as the filenames follow a given naming scheme.</span></span> <span data-ttu-id="2b6a2-206">Bu destek sayesinde, ASP.NET AJAX uzantıları betikleri yerelleştirme ve Genelleştirme uygulamaların basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-206">With this support, the ASP.NET AJAX Extensions simplify the localization of scripts and the globalization of applications.</span></span>

## <a name="bio"></a><span data-ttu-id="2b6a2-207">*Biyografisi*</span><span class="sxs-lookup"><span data-stu-id="2b6a2-207">*Bio*</span></span>

<span data-ttu-id="2b6a2-208">Tan göstermek Microsoft Web teknolojileri ile bu yana 1997 çalışma ve myKB.com Başkanı ise ([www.myKB.com](http://www.myKB.com)) kendisine ASP.NET yazılırken burada uzmanlaşmış tabanlı Bilgi Bankası yazılım çözümlerini odaklanmış uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="2b6a2-208">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="2b6a2-209">Tan temas kurulabileceğini doğrula e-posta aracılığıyla [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) veya kendi blog adresindeki [ScottCate.com](http://ScottCate.com)</span><span class="sxs-lookup"><span data-stu-id="2b6a2-209">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="2b6a2-210">[Önceki](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
[sonraki](understanding-asp-net-ajax-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="2b6a2-210">[Previous](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
[Next](understanding-asp-net-ajax-web-services.md)</span></span>