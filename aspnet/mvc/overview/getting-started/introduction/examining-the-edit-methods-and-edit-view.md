---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: "Düzenleme görünümü ve düzenleme yöntemler inceleniyor | Microsoft Docs"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2015
ms.topic: article
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 84aadccc18e7fa0fb56c7a78e144a1bf1038aac5
ms.sourcegitcommit: d1d8071d4093bf2444b5ae19d6e45c3d187e338b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/19/2017
---
<a name="examining-the-edit-methods-and-edit-view"></a><span data-ttu-id="936f4-102">Düzenleme görünümü ve düzenleme yöntemler inceleniyor</span><span class="sxs-lookup"><span data-stu-id="936f4-102">Examining the Edit Methods and Edit View</span></span>
====================
<span data-ttu-id="936f4-103">Tarafından [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="936f4-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

<span data-ttu-id="936f4-104">Bu bölümde, oluşturulan inceleyeceğiz `Edit` eylem yöntemleri ve görünümler film denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="936f4-104">In this section, you'll examine the generated `Edit` action methods and views for the movie controller.</span></span> <span data-ttu-id="936f4-105">Ancak daha iyi Ara yayın tarihi yapmak için kısa bir değişiklik ilk alacaktır.</span><span class="sxs-lookup"><span data-stu-id="936f4-105">But first will take a short diversion to make the release date look better.</span></span> <span data-ttu-id="936f4-106">Açık *Models\Movie.cs* dosya ve aşağıda gösterilen vurgulanan satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="936f4-106">Open the *Models\Movie.cs* file and add the highlighted lines shown below:</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

<span data-ttu-id="936f4-107">Bu gibi belirli tarih kültür de yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="936f4-107">You can also make the date culture specific like this:</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

<span data-ttu-id="936f4-108">Şu konulara değineceğiz [DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx) sonraki öğreticide.</span><span class="sxs-lookup"><span data-stu-id="936f4-108">We'll cover [DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx) in the next tutorial.</span></span> <span data-ttu-id="936f4-109">[Görüntülemek](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayattribute.aspx) özniteliği ne bir alanın adını (Bu durumda "ReleaseDate" yerine "yayın tarihi") için görüntülenecek belirtir.</span><span class="sxs-lookup"><span data-stu-id="936f4-109">The [Display](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayattribute.aspx) attribute specifies what to display for the name of a field (in this case "Release Date" instead of "ReleaseDate").</span></span> <span data-ttu-id="936f4-110">[DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği veri türünü belirtir, alanda depolanan saat bilgisi gösterilmesi için bu durumda bir tarih.</span><span class="sxs-lookup"><span data-stu-id="936f4-110">The [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute specifies the type of the data, in this case it's a date, so the time information stored in the field is not displayed.</span></span> <span data-ttu-id="936f4-111">[DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliği tarih biçimleri hatalı işler Chrome tarayıcıda bir hata için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="936f4-111">The [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute is needed for a bug in the Chrome browser that renders date formats incorrectly.</span></span>

<span data-ttu-id="936f4-112">Uygulamayı çalıştırın ve Gözat `Movies` denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="936f4-112">Run the application and browse to the `Movies` controller.</span></span> <span data-ttu-id="936f4-113">Fare işaretçisini tutun bir **Düzenle** bağlandığı URL'yi görmek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="936f4-113">Hold the mouse pointer over an **Edit** link to see the URL that it links to.</span></span>

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

<span data-ttu-id="936f4-115">**Düzenle** bağlantı tarafından üretilen `Html.ActionLink` yönteminde *Views\Movies\Index.cshtml* görünümü:</span><span class="sxs-lookup"><span data-stu-id="936f4-115">The **Edit** link was generated by the `Html.ActionLink` method in the *Views\Movies\Index.cshtml* view:</span></span>

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

<span data-ttu-id="936f4-117">`Html` Nesnesi üzerinde bir özelliği kullanılarak kullanıma sunulan bir yardımcı olan [System.Web.Mvc.WebViewPage](https://msdn.microsoft.com/en-us/library/gg402107(VS.98).aspx) temel sınıfı.</span><span class="sxs-lookup"><span data-stu-id="936f4-117">The `Html` object is a helper that's exposed using a property on the [System.Web.Mvc.WebViewPage](https://msdn.microsoft.com/en-us/library/gg402107(VS.98).aspx) base class.</span></span> <span data-ttu-id="936f4-118">`ActionLink` Yardımcı yöntemini eylem yöntemlerine denetleyicilerde bağlantı HTML köprüler dinamik olarak oluşturulacak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="936f4-118">The `ActionLink` method of the helper makes it easy to dynamically generate HTML hyperlinks that link to action methods on controllers.</span></span> <span data-ttu-id="936f4-119">İlk bağımsız değişken `ActionLink` yöntemdir işlemek için bağlantı metni (örneğin, `<a>Edit Me</a>`).</span><span class="sxs-lookup"><span data-stu-id="936f4-119">The first argument to the `ActionLink` method is the link text to render (for example, `<a>Edit Me</a>`).</span></span> <span data-ttu-id="936f4-120">İkinci bağımsız değişkeni çağırılacak eylem yönteminin adıdır (Bu durumda, `Edit` eylem).</span><span class="sxs-lookup"><span data-stu-id="936f4-120">The second argument is the name of the action method to invoke (In this case, the `Edit` action).</span></span> <span data-ttu-id="936f4-121">Son bağımsız değişken bir [anonim nesneyi](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) (Bu durumda, 4 kimliği) rota verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="936f4-121">The final argument is an [anonymous object](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) that generates the route data (in this case, the ID of 4).</span></span>

<span data-ttu-id="936f4-122">Önceki görüntüde gösterildiği oluşturulan bağlantı `http://localhost:1234/Movies/Edit/4`.</span><span class="sxs-lookup"><span data-stu-id="936f4-122">The generated link shown in the previous image is `http://localhost:1234/Movies/Edit/4`.</span></span> <span data-ttu-id="936f4-123">Varsayılan yol (oluşturulmuş *uygulama\_Start\RouteConfig.cs*) URL deseni alır `{controller}/{action}/{id}`.</span><span class="sxs-lookup"><span data-stu-id="936f4-123">The default route (established in *App\_Start\RouteConfig.cs*) takes the URL pattern `{controller}/{action}/{id}`.</span></span> <span data-ttu-id="936f4-124">Bu nedenle, ASP.NET çevirir `http://localhost:1234/Movies/Edit/4` bir istek içine `Edit` eylem yöntemi `Movies` parametresiyle denetleyicisi `ID` 4 eşittir.</span><span class="sxs-lookup"><span data-stu-id="936f4-124">Therefore, ASP.NET translates `http://localhost:1234/Movies/Edit/4` into a request to the `Edit` action method of the `Movies` controller with the parameter `ID` equal to 4.</span></span> <span data-ttu-id="936f4-125">Aşağıdaki kod inceleyin *uygulama\_Start\RouteConfig.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="936f4-125">Examine the following code from the *App\_Start\RouteConfig.cs* file.</span></span> <span data-ttu-id="936f4-126">[MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) yöntemi, HTTP isteklerini doğru denetleyici ve eylem yöntemine yönlendirmek ve isteğe bağlı ID parametresi sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="936f4-126">The [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) method is used to route HTTP requests to the correct controller and action method and supply the optional ID parameter.</span></span> <span data-ttu-id="936f4-127">[MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) yöntemi tarafından kullanılan de [HtmlHelpers](https://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper(v=vs.108).aspx) gibi `ActionLink` verilen denetleyici, eylem yöntemi ve herhangi bir rota veri URL üretmek için.</span><span class="sxs-lookup"><span data-stu-id="936f4-127">The [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) method is also used by the [HtmlHelpers](https://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper(v=vs.108).aspx) such as `ActionLink` to generate URLs given the controller, action method and any route data.</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

<span data-ttu-id="936f4-128">Eylem yöntemi parametrelerini bir sorgu dizesi kullanarak da geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="936f4-128">You can also pass action method parameters using a query string.</span></span> <span data-ttu-id="936f4-129">Örneğin, URL `http://localhost:1234/Movies/Edit?ID=3` parametresi de geçirir `ID` için 3'ün `Edit` eylem yöntemi `Movies` denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="936f4-129">For example, the URL `http://localhost:1234/Movies/Edit?ID=3` also passes the parameter `ID` of 3 to the `Edit` action method of the `Movies` controller.</span></span>

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

<span data-ttu-id="936f4-131">Açık `Movies` denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="936f4-131">Open the `Movies` controller.</span></span> <span data-ttu-id="936f4-132">İki `Edit` eylem yöntemleri aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="936f4-132">The two `Edit` action methods are shown below.</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

<span data-ttu-id="936f4-133">İkinci fark `Edit` tarafından eylem yöntemi öncesinde `HttpPost` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="936f4-133">Notice the second `Edit` action method is preceded by the `HttpPost` attribute.</span></span> <span data-ttu-id="936f4-134">Bu öznitelik belirleyen aşırı yüklemesini `Edit` yöntemi yalnızca POST istekleri için çağrılan.</span><span class="sxs-lookup"><span data-stu-id="936f4-134">This attribute specifies that the overload of the `Edit` method can be invoked only for POST requests.</span></span> <span data-ttu-id="936f4-135">Geçerli olabilir `HttpGet` ilk öznitelik Düzenle yöntemi, ancak bu gerekli değildir, varsayılan olduğundan.</span><span class="sxs-lookup"><span data-stu-id="936f4-135">You could apply the `HttpGet` attribute to the first edit method, but that's not necessary because it's the default.</span></span> <span data-ttu-id="936f4-136">(Örtük olarak atanmış olan eylem yöntemlerine bakın `HttpGet` olarak özniteliği `HttpGet` yöntemlerini.) [Bağlamak](https://msdn.microsoft.com/en-us/library/system.web.mvc.bindattribute(v=vs.108).aspx) veri modeliniz için aşırı gönderim bilgisayar korsanlarının tutar başka bir önemli güvenlik mekanizması bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="936f4-136">(We'll refer to action methods that are implicitly assigned the `HttpGet` attribute as `HttpGet` methods.) The [Bind](https://msdn.microsoft.com/en-us/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute is another important security mechanism that keeps hackers from over-posting data to your model.</span></span> <span data-ttu-id="936f4-137">Değiştirmek istediğiniz bağlama özniteliğinde özellikleri yalnızca içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="936f4-137">You should only include properties in the bind attribute that you want to change.</span></span> <span data-ttu-id="936f4-138">Overposting ve bağ özniteliğinde hakkında bilgi edinebilirsiniz my [güvenlik notu overposting](https://go.microsoft.com/fwlink/?LinkId=317598).</span><span class="sxs-lookup"><span data-stu-id="936f4-138">You can read about overposting and the bind attribute in my [overposting security note](https://go.microsoft.com/fwlink/?LinkId=317598).</span></span> <span data-ttu-id="936f4-139">Bu öğreticide kullanılan basit modelde biz modeldeki tüm veri bağlama.</span><span class="sxs-lookup"><span data-stu-id="936f4-139">In the simple model used in this tutorial, we will be binding all the data in the model.</span></span> <span data-ttu-id="936f4-140">[ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) özniteliği istek sahteciliğini önlemek için kullanılır ve ile eşleştirilmiş `@Html.AntiForgeryToken()` düzenleme görünümü dosyasındaki (*Views\Movies\Edit.cshtml*), bir bölümü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="936f4-140">The [ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) attribute is used to prevent forgery of a request and is paired up with `@Html.AntiForgeryToken()` in the edit view file (*Views\Movies\Edit.cshtml*), a portion is shown below:</span></span>

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

<span data-ttu-id="936f4-141">`@Html.AntiForgeryToken()`içinde eşleşmelidir bir gizli form sahteciliğe karşı koruma belirteci oluşturur `Edit` yöntemi `Movies` denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="936f4-141">`@Html.AntiForgeryToken()` generates a hidden form anti-forgery token that must match in the `Edit` method of the `Movies` controller.</span></span> <span data-ttu-id="936f4-142">Daha fazla bilgiyi hakkında siteler arası istek sahteciliği (XSRF veya CSRF olarak da bilinir) my öğreticideki [XSRF/CSRF önleme mvc'de](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md).</span><span class="sxs-lookup"><span data-stu-id="936f4-142">You can read more about Cross-site request forgery (also known as XSRF or CSRF) in my tutorial [XSRF/CSRF Prevention in MVC](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md).</span></span>

<span data-ttu-id="936f4-143">`HttpGet` `Edit` Yöntemi film ID parametresi alır, Entity Framework kullanarak filmi arar `Find` yöntemi ve seçili film düzenleme görünümü döndürür.</span><span class="sxs-lookup"><span data-stu-id="936f4-143">The `HttpGet` `Edit` method takes the movie ID parameter, looks up the movie using the Entity Framework `Find` method, and returns the selected movie to the Edit view.</span></span> <span data-ttu-id="936f4-144">Bir filmi bulunamazsa [HttpNotFound](https://msdn.microsoft.com/en-us/library/gg453938(VS.98).aspx) döndürülür.</span><span class="sxs-lookup"><span data-stu-id="936f4-144">If a movie cannot be found, [HttpNotFound](https://msdn.microsoft.com/en-us/library/gg453938(VS.98).aspx) is returned.</span></span> <span data-ttu-id="936f4-145">Yapı iskelesi sistem düzenleme görünümü oluşturduğunuzda, incelenmesi `Movie` sınıfı ve işlemek için oluşturulan kodu `<label>` ve `<input>` sınıfın her bir özellik için öğeleri.</span><span class="sxs-lookup"><span data-stu-id="936f4-145">When the scaffolding system created the Edit view, it examined the `Movie` class and created code to render `<label>` and `<input>` elements for each property of the class.</span></span> <span data-ttu-id="936f4-146">Aşağıdaki örnek, visual studio yapı iskelesi sistem tarafından oluşturulan düzenleme görünümü gösterir:</span><span class="sxs-lookup"><span data-stu-id="936f4-146">The following example shows the Edit view that was generated by the visual studio scaffolding system:</span></span>

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

<span data-ttu-id="936f4-147">Şablonu görüntüleme nasıl sahip fark bir `@model MvcMovie.Models.Movie` deyimini dosyanın üst — bu görünüm model türünde olmasını şablonu görüntüleme için beklediğini belirtir `Movie`.</span><span class="sxs-lookup"><span data-stu-id="936f4-147">Notice how the view template has a `@model MvcMovie.Models.Movie` statement at the top of the file — this specifies that the view expects the model for the view template to be of type `Movie`.</span></span>

<span data-ttu-id="936f4-148">İskele kurulmuş kodu birkaç kullanan *yardımcı yöntemler* HTML biçimlendirmesi kolaylaştırmak için.</span><span class="sxs-lookup"><span data-stu-id="936f4-148">The scaffolded code uses several *helper methods* to streamline the HTML markup.</span></span> <span data-ttu-id="936f4-149">[ `Html.LabelFor` ](https://msdn.microsoft.com/en-us/library/gg401864(VS.98).aspx) Yardımcı alanın adını görüntüler (&quot;başlık&quot;, &quot;ReleaseDate&quot;, &quot;Tarz&quot;, veya &quot;fiyatı &quot;).</span><span class="sxs-lookup"><span data-stu-id="936f4-149">The [`Html.LabelFor`](https://msdn.microsoft.com/en-us/library/gg401864(VS.98).aspx) helper displays the name of the field (&quot;Title&quot;, &quot;ReleaseDate&quot;, &quot;Genre&quot;, or &quot;Price&quot;).</span></span> <span data-ttu-id="936f4-150">[ `Html.EditorFor` ](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) Yardımcı işleyen bir HTML `<input>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="936f4-150">The [`Html.EditorFor`](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) helper renders an HTML `<input>` element.</span></span> <span data-ttu-id="936f4-151">[ `Html.ValidationMessageFor` ](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) Yardımcısı bu özellik ile ilişkili herhangi bir doğrulama iletisi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="936f4-151">The [`Html.ValidationMessageFor`](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) helper displays any validation messages associated with that property.</span></span>

<span data-ttu-id="936f4-152">Uygulamayı çalıştırın ve gidin */Movies* URL.</span><span class="sxs-lookup"><span data-stu-id="936f4-152">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="936f4-153">Tıklatın bir **Düzenle** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="936f4-153">Click an **Edit** link.</span></span> <span data-ttu-id="936f4-154">Tarayıcıda, sayfa için kaynağı görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="936f4-154">In the browser, view the source for the page.</span></span> <span data-ttu-id="936f4-155">HTML form öğesi için aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="936f4-155">The HTML for the form element is shown below.</span></span>

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

<span data-ttu-id="936f4-156">`<input>` Öğeleridir bir HTML `<form>` öğesi, `action` özniteliği postalamak için ayarlanmış */filmler/düzenleme* URL.</span><span class="sxs-lookup"><span data-stu-id="936f4-156">The `<input>` elements are in an HTML `<form>` element whose `action` attribute is set to post to the */Movies/Edit* URL.</span></span> <span data-ttu-id="936f4-157">Form verileri sunucuya nakledilir zaman **kaydetmek** düğmesine tıklandığında.</span><span class="sxs-lookup"><span data-stu-id="936f4-157">The form data will be posted to the server when the **Save** button is clicked.</span></span> <span data-ttu-id="936f4-158">İkinci satır gizli gösterir [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) tarafından oluşturulan belirteç `@Html.AntiForgeryToken()` çağırın.</span><span class="sxs-lookup"><span data-stu-id="936f4-158">The second line shows the hidden [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) token generated by the `@Html.AntiForgeryToken()` call.</span></span>

## <a name="processing-the-post-request"></a><span data-ttu-id="936f4-159">POST isteği işleme</span><span class="sxs-lookup"><span data-stu-id="936f4-159">Processing the POST Request</span></span>

<span data-ttu-id="936f4-160">Aşağıdaki liste gösterildiği `HttpPost` sürümü `Edit` eylem yöntemi.</span><span class="sxs-lookup"><span data-stu-id="936f4-160">The following listing shows the `HttpPost` version of the `Edit` action method.</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

<span data-ttu-id="936f4-161">[ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) özniteliği doğrular [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) tarafından oluşturulan belirteç `@Html.AntiForgeryToken()` görünümünde çağırın.</span><span class="sxs-lookup"><span data-stu-id="936f4-161">The [ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) attribute validates the [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) token generated by the `@Html.AntiForgeryToken()` call in the view.</span></span>

<span data-ttu-id="936f4-162">[ASP.NET MVC model bağlayıcı](https://msdn.microsoft.com/en-us/library/dd410405.aspx) gönderilen form değerleri alır ve oluşturan bir `Movie` olarak geçirilen nesne `movie` parametresi.</span><span class="sxs-lookup"><span data-stu-id="936f4-162">The [ASP.NET MVC model binder](https://msdn.microsoft.com/en-us/library/dd410405.aspx) takes the posted form values and creates a `Movie` object that's passed as the `movie` parameter.</span></span> <span data-ttu-id="936f4-163">`ModelState.IsValid` Yöntemi doğrular biçiminde gönderilen veriler (düzenleme veya güncelleştirme) değiştirmek için kullanılabilir bir `Movie` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="936f4-163">The `ModelState.IsValid` method verifies that the data submitted in the form can be used to modify (edit or update) a `Movie` object.</span></span> <span data-ttu-id="936f4-164">Veriler geçerliyse, film verileri kaydedilir `Movies` koleksiyonu `db(MovieDBContext` örnek).</span><span class="sxs-lookup"><span data-stu-id="936f4-164">If the data is valid, the movie data is saved to the `Movies` collection of the `db(MovieDBContext` instance).</span></span> <span data-ttu-id="936f4-165">Yeni film verileri çağırarak veritabanına kaydedilir `SaveChanges` yöntemi `MovieDBContext`.</span><span class="sxs-lookup"><span data-stu-id="936f4-165">The new movie data is saved to the database by calling the `SaveChanges` method of `MovieDBContext`.</span></span> <span data-ttu-id="936f4-166">Veriler kaydedildikten sonra kodu kullanıcı için yönlendiren `Index` eylem yöntemi `MoviesController` yaptığınız değişiklikler dahil film koleksiyon görüntüler sınıfı.</span><span class="sxs-lookup"><span data-stu-id="936f4-166">After saving the data, the code redirects the user to the `Index` action method of the `MoviesController` class, which displays the movie collection, including the changes just made.</span></span>

<span data-ttu-id="936f4-167">Bir alan değerlerini geçerli olmayan istemci tarafı doğrulama belirler hemen bir hata iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="936f4-167">As soon as the client side validation determines the values of a field are not valid, an error message is displayed.</span></span> <span data-ttu-id="936f4-168">JavaScript devre dışı bırakırsanız, istemci tarafı doğrulama olmaz ancak sunucu algılar gönderilen değerler geçerli değildir ve form değerleri hata iletileri ile görünürler.</span><span class="sxs-lookup"><span data-stu-id="936f4-168">If you disable JavaScript, you won't have client side validation but the server will detect the posted values are not valid, and the form values will be redisplayed with error messages.</span></span> <span data-ttu-id="936f4-169">Öğreticinin ilerleyen bölümlerinde daha ayrıntılı doğrulama inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="936f4-169">Later in the tutorial we examine validation in more detail.</span></span>

<span data-ttu-id="936f4-170">`Html.ValidationMessageFor` Yardımcıları içinde *Edit.cshtml* şablonu uygun hata iletilerini görüntüleme ilgilenebilmek görünümü.</span><span class="sxs-lookup"><span data-stu-id="936f4-170">The `Html.ValidationMessageFor` helpers in the *Edit.cshtml* view template take care of displaying appropriate error messages.</span></span>

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

<span data-ttu-id="936f4-172">Tüm `HttpGet` benzer bir desen yöntemleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="936f4-172">All the `HttpGet` methods follow a similar pattern.</span></span> <span data-ttu-id="936f4-173">Film nesnesini alın (veya durumunda nesnelerin listesini `Index`) ve görünüm model geçirin.</span><span class="sxs-lookup"><span data-stu-id="936f4-173">They get a movie object (or list of objects, in the case of `Index`), and pass the model to the view.</span></span> <span data-ttu-id="936f4-174">`Create` Yöntemi bir boş film nesnesi oluşturma görünümüne geçirir.</span><span class="sxs-lookup"><span data-stu-id="936f4-174">The `Create` method passes an empty movie object to the Create view.</span></span> <span data-ttu-id="936f4-175">Bu nedenle oluşturmak, düzenlemek, silmek veya aksi halde verileri değiştirme tüm yöntemleri yapmak `HttpPost` yönteminin.</span><span class="sxs-lookup"><span data-stu-id="936f4-175">All the methods that create, edit, delete, or otherwise modify data do so in the `HttpPost` overload of the method.</span></span> <span data-ttu-id="936f4-176">Bir HTTP GET yöntemi verileri değiştirme olan bir güvenlik riski blog gönderisine girişi açıklandığı gibi [ASP.NET MVC ipucu #46 – güvenlik açıklarını oluşturduğundan bağlantılarını sil kullanmayan](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span><span class="sxs-lookup"><span data-stu-id="936f4-176">Modifying data in an HTTP GET method is a security risk, as described in the blog post entry [ASP.NET MVC Tip #46 – Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span> <span data-ttu-id="936f4-177">GET yöntemi verileri değiştirme de ihlal HTTP en iyi yöntemler ve mimari [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) desen, GET istekleri uygulamanızın durumunu değiştirmemeniz gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="936f4-177">Modifying data in a GET method also violates HTTP best practices and the architectural [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) pattern, which specifies that GET requests should not change the state of your application.</span></span> <span data-ttu-id="936f4-178">Diğer bir deyişle, bir GET işlemi gerçekleştirilirken hiçbir yan etkisi olan ve kalıcı verilerinizi değiştirmeyen güvenli bir işlem olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="936f4-178">In other words, performing a GET operation should be a safe operation that has no side effects and doesn't modify your persisted data.</span></span>

<span data-ttu-id="936f4-179">ABD İngilizcesi bilgisayar kullanıyorsanız, bu bölüm atlayın ve sonraki öğretici gidin.</span><span class="sxs-lookup"><span data-stu-id="936f4-179">If you are using a US-English computer, you can skip this section and go to the next tutorial.</span></span> <span data-ttu-id="936f4-180">Bu öğretici Globalize sürümünü indirebilirsiniz [burada](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475).</span><span class="sxs-lookup"><span data-stu-id="936f4-180">You can download the Globalize version of this tutorial [here](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475).</span></span> <span data-ttu-id="936f4-181">Bir mükemmel iki bölümlü öğretici için uluslararası duruma getirme hakkında bkz [Nadeem'ın ASP.NET MVC 5 uluslararası](http://afana.me/post/aspnet-mvc-internationalization.aspx).</span><span class="sxs-lookup"><span data-stu-id="936f4-181">For an excellent two part tutorial on Internationalization, see [Nadeem's ASP.NET MVC 5 Internationalization](http://afana.me/post/aspnet-mvc-internationalization.aspx).</span></span>


> [!NOTE]
> <span data-ttu-id="936f4-182">bir virgül İngilizce dışındaki yerel ayarlar için jQuery doğrulamasına desteklemek için (&quot;,&quot;) ondalık ve ABD İngilizcesi dışındaki tarih biçimleri için içermelidir *globalize.js* ve özel  *cultures/globalize.cultures.js* dosyası (gelen [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) ve kullanmak için JavaScript'i `Globalize.parseFloat`.</span><span class="sxs-lookup"><span data-stu-id="936f4-182">to support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="936f4-183">JQuery İngilizce olmayan doğrulama Nuget'ten alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="936f4-183">You can get the jQuery non-English validation from NuGet.</span></span> <span data-ttu-id="936f4-184">(Bir İngilizce yerel ayar kullanıyorsanız Globalize yüklemeyin.)</span><span class="sxs-lookup"><span data-stu-id="936f4-184">(Don't install Globalize if you are using a English locale.)</span></span>


1. <span data-ttu-id="936f4-185">Gelen **Araçları** menüsünü tıklatın **NuGetLibrary Paket Yöneticisi**ve ardından **çözüm için NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="936f4-185">From the **Tools** menu click **NuGetLibrary Package Manager**, and then click **Manage NuGet Packages for Solution**.</span></span>  
  
    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. <span data-ttu-id="936f4-186">Sol bölmede seçin  **Gözat*.* ** (Aşağıdaki görüntü bakın.)</span><span class="sxs-lookup"><span data-stu-id="936f4-186">On the left pane, select **Browse*.***(See the image below.)</span></span>
3. <span data-ttu-id="936f4-187">Giriş kutusuna *Globalize**.</span><span class="sxs-lookup"><span data-stu-id="936f4-187">In the input box, enter *Globalize**.</span></span>  
  
    <span data-ttu-id="936f4-188">![](examining-the-edit-methods-and-edit-view/_static/image6.png)Seçin `jQuery.Validation.Globalize`, seçin `MvcMovie` tıklatıp **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="936f4-188">![](examining-the-edit-methods-and-edit-view/_static/image6.png) Choose `jQuery.Validation.Globalize`, choose `MvcMovie` and click **Install**.</span></span> <span data-ttu-id="936f4-189">*Scripts\jquery.globalize\globalize.js* dosyayı projenize eklenir.</span><span class="sxs-lookup"><span data-stu-id="936f4-189">The *Scripts\jquery.globalize\globalize.js* file will be added to your project.</span></span> <span data-ttu-id="936f4-190">*Scripts\jquery.globalize\cultures\* klasörü birçok kültür JavaScript dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="936f4-190">The *Scripts\jquery.globalize\cultures\* folder will contain many culture JavaScript files.</span></span> <span data-ttu-id="936f4-191">Not: Bu paket yüklemek için beş dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="936f4-191">Note, it may take five minutes to install this package.</span></span>

 <span data-ttu-id="936f4-192">Aşağıdaki kod Views\Movies\Edit.cshtml dosya için yapılan değişiklikleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="936f4-192">The following code shows the modifications to the Views\Movies\Edit.cshtml file:</span></span> 

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

<span data-ttu-id="936f4-193">Bu kodu her düzenleme görünümü, yinelenen önlemek için Düzen dosyasına taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="936f4-193">To avoid repeating this code in every Edit view, you can move it to the layout file.</span></span> <span data-ttu-id="936f4-194">Komut dosyası indirme en iyi duruma getirme my öğretici bkz [paketleme ve küçültme](../../performance/bundling-and-minification.md).</span><span class="sxs-lookup"><span data-stu-id="936f4-194">To optimize the script download, see my tutorial [Bundling and Minification](../../performance/bundling-and-minification.md).</span></span>

<span data-ttu-id="936f4-195">Daha fazla bilgi için bkz: [ASP.NET MVC 3 uluslararası hale getirme](http://afana.me/post/aspnet-mvc-internationalization.aspx) ve [ASP.NET MVC 3 uluslararası - Kısım 2 (NerdDinner)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="936f4-195">For more information see [ASP.NET MVC 3 Internationalization](http://afana.me/post/aspnet-mvc-internationalization.aspx) and [ASP.NET MVC 3 Internationalization - Part 2 (NerdDinner)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx).</span></span>

<span data-ttu-id="936f4-196">Geçici bir düzeltme olarak yerel çalışma doğrulama alınamıyor, bilgisayarınızı ABD İngilizcesi kullanacak şekilde zorlayabilirsiniz veya tarayıcınızın JavaScript devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="936f4-196">As a temporary fix, if you can't get validation working in your locale, you can force your computer to use US English or you can disable JavaScript in your browser.</span></span> <span data-ttu-id="936f4-197">Bilgisayarınızı ABD İngilizcesi kullanacak şekilde zorlamak için projeleri kök Genelleştirme öğesi ekleyebilirsiniz. *web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="936f4-197">To force your computer to use US English, you can add the globalization element to the projects root *web.config* file.</span></span> <span data-ttu-id="936f4-198">Aşağıdaki kod, ABD İngilizcesi olarak ayarlamak kültür ile Genelleştirme öğesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="936f4-198">The following code shows the globalization element with the culture set to United States English.</span></span>

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><span data-ttu-id="936f4-199"><a id="jQueryAjaxJSON"></a>Sonraki öğreticide biz arama işlevini uygulamanız.</span><span class="sxs-lookup"><span data-stu-id="936f4-199"><a id="jQueryAjaxJSON"></a> In the next tutorial, we'll implement search functionality.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="936f4-200">[Önceki](accessing-your-models-data-from-a-controller.md)
[sonraki](adding-search.md)</span><span class="sxs-lookup"><span data-stu-id="936f4-200">[Previous](accessing-your-models-data-from-a-controller.md)
[Next](adding-search.md)</span></span>