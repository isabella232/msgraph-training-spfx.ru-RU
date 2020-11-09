---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823406"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="11d0d-101">В этом руководстве рассказывается, как создать [клиентскую веб-часть SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) , которая использует API Microsoft Graph для получения сведений о календаре для пользователя.</span><span class="sxs-lookup"><span data-stu-id="11d0d-101">This tutorial teaches you how to build a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="11d0d-102">Если вы предпочитаете просто скачать заполненный учебник, вы можете скачать или клонировать [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).</span><span class="sxs-lookup"><span data-stu-id="11d0d-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11d0d-103">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="11d0d-103">Prerequisites</span></span>

<span data-ttu-id="11d0d-104">Прежде чем приступить к работе с этим руководством, на компьютере для разработки должны быть установлены следующие средства.</span><span class="sxs-lookup"><span data-stu-id="11d0d-104">Before you start this tutorial, you should have the following tools installed on your development machine.</span></span>

- [<span data-ttu-id="11d0d-105">Node.js</span><span class="sxs-lookup"><span data-stu-id="11d0d-105">Node.js</span></span>](https://nodejs.org/en/download/releases/)
- [<span data-ttu-id="11d0d-106">Yeoman</span><span class="sxs-lookup"><span data-stu-id="11d0d-106">Yeoman</span></span>](https://yeoman.io/)
- [<span data-ttu-id="11d0d-107">Gulp</span><span class="sxs-lookup"><span data-stu-id="11d0d-107">Gulp</span></span>](https://gulpjs.com/)
- [<span data-ttu-id="11d0d-108">Генератор Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="11d0d-108">Yeoman SharePoint generator</span></span>](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

<span data-ttu-id="11d0d-109">Дополнительные сведения о требованиях для разработки SharePoint Framework можно найти в странице [Настройка среды разработки SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).</span><span class="sxs-lookup"><span data-stu-id="11d0d-109">You can find more details about requirements for SharePoint Framework development at [Set up your SharePoint Framework development environment](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11d0d-110">Для SharePoint Framework требуется Node.js версии 10. x.</span><span class="sxs-lookup"><span data-stu-id="11d0d-110">SharePoint Framework requires Node.js version 10.x.</span></span> <span data-ttu-id="11d0d-111">Обязательно установите правильную версию.</span><span class="sxs-lookup"><span data-stu-id="11d0d-111">Be sure to install the correct version.</span></span>

<span data-ttu-id="11d0d-112">Кроме того, у вас должна быть рабочая или учебная учетная запись Майкрософт с доступом к учетной записи глобального администратора в той же организации.</span><span class="sxs-lookup"><span data-stu-id="11d0d-112">You should also have a Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="11d0d-113">Если у вас нет учетной записи Майкрософт, вы можете [зарегистрироваться в программе для разработчиков office 365](https://developer.microsoft.com/office/dev-program) , чтобы получить бесплатную подписку на Office 365.</span><span class="sxs-lookup"><span data-stu-id="11d0d-113">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

<span data-ttu-id="11d0d-114">Прежде чем приступить к работе с этим руководством, клиент Microsoft 365 должен быть [настроен для разработки SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)с каталогом приложений и тестовым сайтом, созданным ранее.</span><span class="sxs-lookup"><span data-stu-id="11d0d-114">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="11d0d-115">Это руководство было написано в следующих версиях этих средств.</span><span class="sxs-lookup"><span data-stu-id="11d0d-115">This tutorial was written with the following versions of the above tools.</span></span> <span data-ttu-id="11d0d-116">Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.</span><span class="sxs-lookup"><span data-stu-id="11d0d-116">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="11d0d-117">Node.js 10.22.0</span><span class="sxs-lookup"><span data-stu-id="11d0d-117">Node.js 10.22.0</span></span>
> - <span data-ttu-id="11d0d-118">Yeoman 3.1.1</span><span class="sxs-lookup"><span data-stu-id="11d0d-118">Yeoman 3.1.1</span></span>
> - <span data-ttu-id="11d0d-119">Gulp 4.0.2</span><span class="sxs-lookup"><span data-stu-id="11d0d-119">Gulp 4.0.2</span></span>
> - <span data-ttu-id="11d0d-120">1.11.0 генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="11d0d-120">Yeoman SharePoint generator 1.11.0</span></span>

## <a name="feedback"></a><span data-ttu-id="11d0d-121">Отзывы</span><span class="sxs-lookup"><span data-stu-id="11d0d-121">Feedback</span></span>

<span data-ttu-id="11d0d-122">Сообщите о нем в [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).</span><span class="sxs-lookup"><span data-stu-id="11d0d-122">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>
