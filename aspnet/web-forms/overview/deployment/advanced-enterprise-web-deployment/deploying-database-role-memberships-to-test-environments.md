---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: "Test ortamları için veritabanı rolü üyeliği dağıtma | Microsoft Docs"
author: jrjlee
description: "Bu konu, veritabanı rolleri bir test ortamı için çözüm dağıtımının bir parçası olarak kullanıcı hesaplarını eklemek açıklar. İçeren bir çözümü dağıttığınızda..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: ac780c6cd522f9216cafe3b5f23772ef6ebf5d11
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
<a name="deploying-database-role-memberships-to-test-environments"></a><span data-ttu-id="91508-104">Test ortamları için veritabanı rolü üyeliği dağıtma</span><span class="sxs-lookup"><span data-stu-id="91508-104">Deploying Database Role Memberships to Test Environments</span></span>
====================
<span data-ttu-id="91508-105">tarafından [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="91508-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="91508-106">PDF indirin</span><span class="sxs-lookup"><span data-stu-id="91508-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="91508-107">Bu konu, veritabanı rolleri bir test ortamı için çözüm dağıtımının bir parçası olarak kullanıcı hesaplarını eklemek açıklar.</span><span class="sxs-lookup"><span data-stu-id="91508-107">This topic describes how to add user accounts to database roles as part of a solution deployment to a test environment.</span></span>
> 
> <span data-ttu-id="91508-108">Bir hazırlık veya üretim ortamı için bir veritabanı proje içeren bir çözümü dağıttığınızda, kullanıcı hesapları veritabanı rolleri için eklenmesi otomatikleştirmek için geliştirici genellikle istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="91508-108">When you deploy a solution containing a database project to a staging or production environment, you typically don't want the developer to automate the addition of user accounts to database roles.</span></span> <span data-ttu-id="91508-109">Çoğu durumda, geliştirici hangi veritabanı rolleri eklenmesi gereken hangi kullanıcı hesaplarının bilemezsiniz ve bu gereksinimleri dilediğiniz zaman değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91508-109">In most cases, the developer won't know which user accounts need to be added to which database roles, and these requirements could change at any time.</span></span> <span data-ttu-id="91508-110">Bir geliştirme için bir veritabanı proje içeren bir çözümü dağıtmak veya sınama ortamında, ancak genellikle yerine farklı durumdur:</span><span class="sxs-lookup"><span data-stu-id="91508-110">However, when you deploy a solution containing a database project to a development or test environment, the situation is usually rather different:</span></span>
> 
> - <span data-ttu-id="91508-111">Geliştirici genellikle düzenli olarak çözüm günde genellikle birkaç kez yeniden dağıtır.</span><span class="sxs-lookup"><span data-stu-id="91508-111">The developer typically re-deploys the solution on a regular basis, often several times a day.</span></span>
> - <span data-ttu-id="91508-112">Veritabanı genellikle veritabanı kullanıcıları oluşturulmalı ve her dağıtım sonrası rollere eklenen, yani her dağıtımda yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="91508-112">The database is typically re-created on every deployment, which means that database users must be created and added to roles after every deployment.</span></span>
> - <span data-ttu-id="91508-113">Geliştirici genellikle hedef geliştirme veya test ortamı üzerinde tam denetime sahiptir.</span><span class="sxs-lookup"><span data-stu-id="91508-113">The developer typically has full control over the target development or test environment.</span></span>
> 
> <span data-ttu-id="91508-114">Bu senaryoda, otomatik olarak veritabanı kullanıcıları oluşturun ve dağıtım işleminin bir parçası veritabanı rolü üyeliği atamak faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="91508-114">In this scenario, it's often beneficial to automatically create database users and assign database role memberships as part of the deployment process.</span></span>
> 
> <span data-ttu-id="91508-115">Bu işlem koşullu hedef ortamına bağlı gerektiğini anahtar faktördür.</span><span class="sxs-lookup"><span data-stu-id="91508-115">The key factor is that this operation needs to be conditional based on the target environment.</span></span> <span data-ttu-id="91508-116">Bir hazırlık veya üretim ortamı dağıtıyorsanız, işlemi atlamak istiyor.</span><span class="sxs-lookup"><span data-stu-id="91508-116">If you're deploying to a staging or a production environment, you want to skip the operation.</span></span> <span data-ttu-id="91508-117">Bir geliştirici dağıtıyorsunuz veya sınama ortamında, rol üyeliklerini daha fazla müdahalesi olmadan dağıtmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="91508-117">If you're deploying to a developer or test environment, you want to deploy role memberships without further intervention.</span></span> <span data-ttu-id="91508-118">Bu konuda, bu sorunu gidermek için kullanabileceğiniz bir yaklaşım açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="91508-118">This topic describes one approach you can use to address this challenge.</span></span>


<span data-ttu-id="91508-119">Bu konuda eğitim serileri Fabrikam Ltd. adlı kurgusal bir şirket kurumsal dağıtım gereksinimleri dayalı parçası formlar Bu öğretici serisi örnek çözümü & #x 2014; kullanır [Contact Manager çözüm](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& Windows bir ASP.NET MVC 3 uygulama da dahil olmak üzere karmaşıklıkta gerçekçi düzeyine sahip bir web uygulamasını temsil eden #x 2014; Communication Foundation (WCF) hizmetini ve veritabanı projesi.</span><span class="sxs-lookup"><span data-stu-id="91508-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="91508-120">Bu öğreticileri merkezinde dağıtım yöntemi, açıklanan bölünmüş proje dosyası yaklaşım dayalı [proje dosyası anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md), hangi derleme süreci tarafından denetlenen içinde iki dosyaları & #x 2014; proje bir içeren Her hedef ortam ve ortama özgü derleme ve dağıtım ayarları içeren bir için geçerli olan yönergeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91508-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="91508-121">Derleme zamanında ortama özgü proje dosyası oluşturma yönergeleri eksiksiz bir kümesini oluşturmak için ortam belirsiz proje dosyasına birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="91508-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="91508-122">Görev genel bakış</span><span class="sxs-lookup"><span data-stu-id="91508-122">Task Overview</span></span>

<span data-ttu-id="91508-123">Bu konuda, varsayılır:</span><span class="sxs-lookup"><span data-stu-id="91508-123">This topic assumes that:</span></span>

- <span data-ttu-id="91508-124">Bölünmüş proje dosyası yaklaşımı Çözüm dağıtımı açıklandığı gibi kullandığınız [proje dosyası anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="91508-124">You use the split project file approach to solution deployment, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span>
- <span data-ttu-id="91508-125">VSDBCMD açıklandığı gibi veritabanı projenizi dağıtmanın proje dosyasından çağrılmasına [oluşturma işlemini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span><span class="sxs-lookup"><span data-stu-id="91508-125">You call VSDBCMD from the project file to deploy your database project, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

<span data-ttu-id="91508-126">Veritabanı kullanıcıları oluşturun ve bir test ortamı için bir veritabanı projesi dağıttığınızda rol üyeliklerini atamak için yapmanız:</span><span class="sxs-lookup"><span data-stu-id="91508-126">To create database users and assign role memberships when you deploy a database project to a test environment, you'll need to:</span></span>

- <span data-ttu-id="91508-127">Gerekli veritabanı değişiklikleri yapar Transact yapılandırılmış sorgu dili (Transact-SQL) komut dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91508-127">Create a Transact Structured Query Language (Transact-SQL) script that makes the necessary database changes.</span></span>
- <span data-ttu-id="91508-128">SQL komut dosyasını çalıştırmak için sqlcmd.exe yardımcı programını kullanan bir Microsoft Build Engine (MSBuild) hedef oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91508-128">Create a Microsoft Build Engine (MSBuild) target that uses the sqlcmd.exe utility to run the SQL script.</span></span>
- <span data-ttu-id="91508-129">Çözümünüz için bir test ortamı dağıtıyorsanız hedef çağırmak için proje dosyalarınıza yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="91508-129">Configure your project files to invoke the target when you're deploying your solution to a test environment.</span></span>

<span data-ttu-id="91508-130">Bu konuda her bu yordamları gerçekleştirmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="91508-130">This topic will show you how to perform each of these procedures.</span></span>

## <a name="scripting-the-database-role-memberships"></a><span data-ttu-id="91508-131">Veritabanı rol üyeliklerini komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="91508-131">Scripting the Database Role Memberships</span></span>

<span data-ttu-id="91508-132">Seçtiğiniz herhangi bir konuma ve farklı şekillerde çok miktarda bir Transact-SQL komut dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91508-132">You can create a Transact-SQL script in a lot of different ways, and in any location you choose.</span></span> <span data-ttu-id="91508-133">En kolay yaklaşım, Visual Studio 2010'komut dosyası, çözümünüz içinde oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="91508-133">The easiest approach is to create the script within your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="91508-134">**Bir SQL betiği oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="91508-134">**To create a SQL script**</span></span>

1. <span data-ttu-id="91508-135">İçinde **Çözüm Gezgini** penceresi, veritabanı projesi düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="91508-135">In the **Solution Explorer** window, expand your database project node.</span></span>
2. <span data-ttu-id="91508-136">Sağ **betikleri** klasörünü **Ekle**ve ardından **yeni klasör**.</span><span class="sxs-lookup"><span data-stu-id="91508-136">Right-click the **Scripts** folder, point to **Add**, and then click **New Folder**.</span></span>
3. <span data-ttu-id="91508-137">Tür **Test** klasör adı ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="91508-137">Type **Test** as the folder name, and then press Enter.</span></span>
4. <span data-ttu-id="91508-138">Sağ **Test** klasörünü **Ekle**ve ardından **betik**.</span><span class="sxs-lookup"><span data-stu-id="91508-138">Right-click the **Test** folder, point to **Add**, and then click **Script**.</span></span>
5. <span data-ttu-id="91508-139">İçinde **Yeni Öğe Ekle** iletişim kutusunda, kodunuzu anlamlı bir ad verin (örneğin, **AddRoleMemberships.sql**) ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="91508-139">In the **Add New Item** dialog box, give your script a meaningful name (for example, **AddRoleMemberships.sql**), and then click **Add**.</span></span>

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. <span data-ttu-id="91508-140">İçinde *AddRoleMemberships.sql* dosya, Transact-SQL deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="91508-140">In the *AddRoleMemberships.sql* file, add Transact-SQL statements that:</span></span>

    1. <span data-ttu-id="91508-141">Bir veritabanı kullanıcısı, veritabanına erişecek SQL Server oturumu açma oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91508-141">Create a database user for the SQL Server login that will access your database.</span></span>
    2. <span data-ttu-id="91508-142">Veritabanı kullanıcı için tüm gerekli veritabanı rolleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="91508-142">Add the database user to any required database roles.</span></span>
7. <span data-ttu-id="91508-143">Dosya şuna benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="91508-143">The file should resemble this:</span></span>

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. <span data-ttu-id="91508-144">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="91508-144">Save the file.</span></span>

## <a name="executing-the-script-on-the-target-database"></a><span data-ttu-id="91508-145">Hedef veritabanı komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="91508-145">Executing the Script on the Target Database</span></span>

<span data-ttu-id="91508-146">İdeal olarak, veritabanı projenizi dağıttığınızda bir dağıtım sonrası komut dosyasının bir parçası gerekli herhangi bir Transact-SQL betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="91508-146">Ideally, you'd run any required Transact-SQL scripts as part of a post-deployment script when you deploy your database project.</span></span> <span data-ttu-id="91508-147">Ancak, dağıtım sonrası komut dosyalarını, çözüm yapılandırmaları veya derleme özellikleri koşullu temel mantığı yürütmek izin verme.</span><span class="sxs-lookup"><span data-stu-id="91508-147">However, post-deployment scripts don't allow you to execute logic conditionally based on solution configurations or build properties.</span></span> <span data-ttu-id="91508-148">Alternatiftir oluşturarak MSBuild proje dosyası ' doğrudan SQL komut dosyaları çalıştırmak için bir **hedef** sqlcmd.exe komutu yürütür öğesi.</span><span class="sxs-lookup"><span data-stu-id="91508-148">The alternative is to run your SQL scripts directly from the MSBuild project file, by creating a **Target** element that executes a sqlcmd.exe command.</span></span> <span data-ttu-id="91508-149">Hedef veritabanında kodunuzu çalıştırmak için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="91508-149">You can use this command to run your script on the target database:</span></span>


[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]


> [!NOTE]
> <span data-ttu-id="91508-150">Sqlcmd komut satırı seçenekleri hakkında daha fazla bilgi için bkz: [sqlcmd yardımcı programını](https://msdn.microsoft.com/en-us/library/ms162773.aspx).</span><span class="sxs-lookup"><span data-stu-id="91508-150">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/en-us/library/ms162773.aspx).</span></span>


<span data-ttu-id="91508-151">Bu komut bir MSBuild hedef katıştırmak önce komut dosyasının çalışmasını istediğiniz hangi koşullarda dikkate almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="91508-151">Before you embed this command in an MSBuild target, you need to consider under what conditions you want the script to run:</span></span>

- <span data-ttu-id="91508-152">Rol üyeliklerini değiştirmeden önce hedef veritabanının mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="91508-152">The target database must exist before you change its role memberships.</span></span> <span data-ttu-id="91508-153">Bu nedenle, bu komut dosyasını çalıştırmak gereken *sonra* veritabanı dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="91508-153">As such, you need to run this script *after* the database deployment.</span></span>
- <span data-ttu-id="91508-154">Komut yalnızca test ortamları için yürütülebilir bir koşul içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="91508-154">You need to include a condition so that the script is only executed for test environments.</span></span>
- <span data-ttu-id="91508-155">Diğer bir deyişle, bir "," dağıtım & #x 2014; çalıştırıyorsanız dağıtım betikleri oluşturma ancak aslında bunları & #x 2014; çalışan SQL betiği çalıştırma döndürmemelidir.</span><span class="sxs-lookup"><span data-stu-id="91508-155">If you're running a "what if" deployment&#x2014;in other words, if you're generating deployment scripts but not actually running them&#x2014;you shouldn't run the SQL script.</span></span>

<span data-ttu-id="91508-156">Açıklanan bölünmüş proje dosyası yaklaşım kullanıyorsanız [proje dosyası anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md), kişinin Yöneticisi örnek çözümü tarafından gösterildiği gibi bu gibi SQL betiği için yapı yönergeleri bölebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="91508-156">If you're using the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), as demonstrated by the Contact Manager sample solution, you can split the build instructions for your SQL script like this:</span></span>

- <span data-ttu-id="91508-157">Ortama özgü özellikleri, izinler, dağıtılıp dağıtılmayacağını belirler özelliği ortama özgü proje dosyasında gitmesini gerekli (örneğin, *Env Dev.proj*).</span><span class="sxs-lookup"><span data-stu-id="91508-157">Any required environment-specific properties, together with the property that determines whether to deploy permissions, should go in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>
- <span data-ttu-id="91508-158">MSBuild hedef kendisini hedef ortamlar arasında değiştirmez herhangi bir özellik birlikte Evrensel proje dosyasında gitmesi gereken (örneğin, *Publish.proj*).</span><span class="sxs-lookup"><span data-stu-id="91508-158">The MSBuild target itself, together with any properties that will not change between destination environments, should go in the universal project file (for example, *Publish.proj*).</span></span>

<span data-ttu-id="91508-159">Ortama özgü proje dosyasında veritabanı sunucusu adı, hedef veritabanı adı ve rol üyeliklerini dağıtılıp dağıtılmayacağını belirtin kullanıcı olanak sağlayan bir Boolean özelliği tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91508-159">In the environment-specific project file, you need to define the database server name, the target database name, and a Boolean property that lets the user specify whether to deploy role memberships.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]


<span data-ttu-id="91508-160">Evrensel proje dosyasında yürütülebilir sqlcmd konumunu ve çalıştırmak istediğiniz SQL komut dosyası konumunu sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91508-160">In the universal project file, you need to provide the location of the sqlcmd executable and the location of the SQL script you want to run.</span></span> <span data-ttu-id="91508-161">Bu özellikler, hedef ortam bakılmaksızın aynı kalır.</span><span class="sxs-lookup"><span data-stu-id="91508-161">These properties will remain the same regardless of the destination environment.</span></span> <span data-ttu-id="91508-162">Ayrıca sqlcmd komutu çalıştırmak için bir MSBuild hedef oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91508-162">You also need to create an MSBuild target to execute the sqlcmd command.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]


<span data-ttu-id="91508-163">Bu diğer hedefler için yararlı olabilecek gibi bir statik özellik olarak yürütülebilir sqlcmd konumunu ekleyin dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="91508-163">Notice that you add the location of the sqlcmd executable as a static property, as this could be useful to other targets.</span></span> <span data-ttu-id="91508-164">Hedef yürütülmeden önce gerekli olmayacak buna karşılık, SQL komut dosyasının konumunu ve sqlcmd komut sözdizimi hedef içinde dinamik özellikleri olarak tanımladığınız.</span><span class="sxs-lookup"><span data-stu-id="91508-164">In contrast, you define the location of your SQL script and the syntax of the sqlcmd command as dynamic properties within the target, as they will not be required before the target is executed.</span></span> <span data-ttu-id="91508-165">Bu durumda, **DeployTestDBPermissions** hedef, yalnızca bu Koşullar karşılanıyorsa yürütülür:</span><span class="sxs-lookup"><span data-stu-id="91508-165">In this case, the **DeployTestDBPermissions** target will only be executed if these conditions are met:</span></span>

- <span data-ttu-id="91508-166">**DeployTestDBRoleMemberships** özelliği ayarlanmış **doğru**.</span><span class="sxs-lookup"><span data-stu-id="91508-166">The **DeployTestDBRoleMemberships** property is set to **true**.</span></span>
- <span data-ttu-id="91508-167">Kullanıcı belirtilen kurmadı bir **whatIf = true** bayrağı.</span><span class="sxs-lookup"><span data-stu-id="91508-167">The user hasn't specified a **WhatIf=true** flag.</span></span>

<span data-ttu-id="91508-168">Son olarak, hedef çağrılacak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="91508-168">Finally, don't forget to invoke the target.</span></span> <span data-ttu-id="91508-169">İçinde *Publish.proj* dosya, bunu yapabilirsiniz varsayılan bağımlılık listesine hedef ekleyerek **FullPublish** hedef.</span><span class="sxs-lookup"><span data-stu-id="91508-169">In the *Publish.proj* file, you can do this by adding the target to the dependency list for the default **FullPublish** target.</span></span> <span data-ttu-id="91508-170">Emin olmak gereken **DeployTestDBPermissions** hedef yürütülmez kadar **PublishDbPackages** hedef yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="91508-170">You need to ensure that the **DeployTestDBPermissions** target is not executed until the **PublishDbPackages** target has been executed.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]


## <a name="conclusion"></a><span data-ttu-id="91508-171">Sonuç</span><span class="sxs-lookup"><span data-stu-id="91508-171">Conclusion</span></span>

<span data-ttu-id="91508-172">Bu konuda bir yolu, bir veritabanı projesi dağıttığınızda, veritabanı kullanıcıları ve rol üyeliklerini bir dağıtım sonrası eylemi olarak ekleyebileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="91508-172">This topic described one way in which you can add database users and role memberships as a post-deployment action when you deploy a database project.</span></span> <span data-ttu-id="91508-173">Bu, düzenli olarak test ortamında bir veritabanını yeniden oluşturun, ancak genellikle hazırlık veya üretim ortamları için veritabanları dağıttığınızda kaçınılmalıdır genelde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="91508-173">This is typically useful when you regularly re-create a database in a test environment, but it should usually be avoided when you deploy databases to staging or production environments.</span></span> <span data-ttu-id="91508-174">Bu nedenle, böylece bunu yapmak, uygun olduğunda veritabanı kullanıcıları ve rol üyeliklerini yalnızca oluşturulur gerekli koşullu mantık kullanmak emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="91508-174">As such, you should ensure that you use the necessary conditional logic so that database users and role memberships are only created when it's appropriate to do so.</span></span>

## <a name="further-reading"></a><span data-ttu-id="91508-175">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="91508-175">Further Reading</span></span>

<span data-ttu-id="91508-176">Veritabanı projeleri dağıtmak için VSDBCMD kullanma hakkında daha fazla bilgi için bkz: [dağıtma veritabanı projeleri](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span><span class="sxs-lookup"><span data-stu-id="91508-176">For more information on using VSDBCMD to deploy database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="91508-177">Farklı bir hedef ortamlar için veritabanı dağıtımlarını özelleştirme ile ilgili yönergeler için bkz: [veritabanı dağıtımlarını özelleştirme birden çok ortamları](customizing-database-deployments-for-multiple-environments.md).</span><span class="sxs-lookup"><span data-stu-id="91508-177">For guidance on customizing database deployments for different target environments, see [Customizing Database Deployments for Multiple Environments](customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="91508-178">Dağıtım işlemi denetlemek için özel MSBuild proje dosyalarını kullanma hakkında daha fazla bilgi için bkz: [proje dosyası anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md) ve [oluşturma işlemini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span><span class="sxs-lookup"><span data-stu-id="91508-178">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="91508-179">Sqlcmd komut satırı seçenekleri hakkında daha fazla bilgi için bkz: [sqlcmd yardımcı programını](https://msdn.microsoft.com/en-us/library/ms162773.aspx).</span><span class="sxs-lookup"><span data-stu-id="91508-179">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/en-us/library/ms162773.aspx).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="91508-180">[Önceki](customizing-database-deployments-for-multiple-environments.md)
[sonraki](deploying-membership-databases-to-enterprise-environments.md)</span><span class="sxs-lookup"><span data-stu-id="91508-180">[Previous](customizing-database-deployments-for-multiple-environments.md)
[Next](deploying-membership-databases-to-enterprise-environments.md)</span></span>