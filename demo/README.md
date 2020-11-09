---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831350"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="38dc0-101">Выполнение завершенного проекта</span><span class="sxs-lookup"><span data-stu-id="38dc0-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38dc0-102">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="38dc0-102">Prerequisites</span></span>

<span data-ttu-id="38dc0-103">Чтобы запустить завершенный проект в этой папке, вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="38dc0-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="38dc0-104">[Node.js](https://nodejs.org/en/download/releases/) версии 10. x</span><span class="sxs-lookup"><span data-stu-id="38dc0-104">[Node.js](https://nodejs.org/en/download/releases/) version 10.x</span></span>
- [<span data-ttu-id="38dc0-105">Gulp</span><span class="sxs-lookup"><span data-stu-id="38dc0-105">Gulp</span></span>](https://gulpjs.com/)
- <span data-ttu-id="38dc0-106">Рабочая или учебная учетная запись Майкрософт, которая получает доступ к учетной записи глобального администратора в той же организации.</span><span class="sxs-lookup"><span data-stu-id="38dc0-106">A Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="38dc0-107">Если у вас нет учетной записи Майкрософт, вы можете [зарегистрироваться в программе для разработчиков office 365](https://developer.microsoft.com/office/dev-program) , чтобы получить бесплатную подписку на Office 365.</span><span class="sxs-lookup"><span data-stu-id="38dc0-107">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>
- <span data-ttu-id="38dc0-108">Прежде чем приступить к работе с этим руководством, клиент Microsoft 365 должен быть [настроен для разработки SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)с каталогом приложений и тестовым сайтом, созданным ранее.</span><span class="sxs-lookup"><span data-stu-id="38dc0-108">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

### <a name="deploy-the-web-part"></a><span data-ttu-id="38dc0-109">Развертывание веб-части</span><span class="sxs-lookup"><span data-stu-id="38dc0-109">Deploy the web part</span></span>

1. <span data-ttu-id="38dc0-110">Выполните две следующие команды в утилите CLI, чтобы создать и упаковать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="38dc0-110">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="38dc0-111">Откройте браузер и перейдите к каталогу приложений SharePoint клиента.</span><span class="sxs-lookup"><span data-stu-id="38dc0-111">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="38dc0-112">Выберите пункт меню **приложения для SharePoint** в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="38dc0-112">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="38dc0-113">Отправьте файл **./шарепоинт/солутион/граф-туториал.сппкг** .</span><span class="sxs-lookup"><span data-stu-id="38dc0-113">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="38dc0-114">В приглашении **доверять...** убедитесь, что в запросе указаны 4 разрешения Microsoft Graph, заданные в **package-solution.jsдля** файла.</span><span class="sxs-lookup"><span data-stu-id="38dc0-114">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="38dc0-115">Выберите **сделать это решение доступным для всех сайтов в Организации** , а затем нажмите кнопку **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="38dc0-115">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="38dc0-116">Откройте [центр администрирования SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) с помощью учетной записи администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="38dc0-116">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="38dc0-117">В левом меню выберите **Дополнительно** , а затем — **доступ к API**.</span><span class="sxs-lookup"><span data-stu-id="38dc0-117">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="38dc0-118">Выберите каждый из ожидающих запросов в пакете **Graph – Tutorial — клиентский — на стороне решения** и нажмите кнопку **утвердить**.</span><span class="sxs-lookup"><span data-stu-id="38dc0-118">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![Снимок экрана со страницей доступа к API центра администрирования SharePoint](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="38dc0-120">Тестирование веб-части</span><span class="sxs-lookup"><span data-stu-id="38dc0-120">Test the web part</span></span>

1. <span data-ttu-id="38dc0-121">Перейдите на сайт SharePoint, на котором необходимо протестировать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="38dc0-121">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="38dc0-122">Создайте новую страницу для тестирования веб-части.</span><span class="sxs-lookup"><span data-stu-id="38dc0-122">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="38dc0-123">С помощью средства выбора веб-части найдите веб-часть **графтуториал** и добавьте ее на страницу.</span><span class="sxs-lookup"><span data-stu-id="38dc0-123">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Снимок экрана: веб-часть Графтуториал в средстве выбора веб-частей](../tutorial/images/add-web-part.png)
