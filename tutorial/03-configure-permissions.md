---
ms.openlocfilehash: 19bd57df9f349d67e9f10e7dd70f02231950b010
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823422"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="3b6a4-101">SharePoint Framework исключает необходимость регистрации приложения в Azure AD для получения маркеров доступа к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-101">The SharePoint Framework eliminates the need to register an application in Azure AD for getting access tokens to access Microsoft Graph.</span></span> <span data-ttu-id="3b6a4-102">Он обрабатывает проверку подлинности для пользователя, зарегистрированного в SharePoint, позволяя веб-части получать маркеры пользователей.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-102">It handles the authentication for the user that is logged into SharePoint, allowing your web part to get user tokens.</span></span> <span data-ttu-id="3b6a4-103">Веб-части необходимо указать, какие [области разрешений на доступ к графике](https://docs.microsoft.com/graph/permissions-reference) необходимы, а администратор клиента может утверждать эти разрешения во время установки.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-103">Your web part needs to indicate which [Graph permission scopes](https://docs.microsoft.com/graph/permissions-reference) it requires, and a tenant admin can approve those permissions during installation.</span></span>

## <a name="configure-permissions"></a><span data-ttu-id="3b6a4-104">Настройка разрешений</span><span class="sxs-lookup"><span data-stu-id="3b6a4-104">Configure permissions</span></span>

1. <span data-ttu-id="3b6a4-105">**package-solution.jsOpen./config/**.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-105">Open **./config/package-solution.json**.</span></span>

1. <span data-ttu-id="3b6a4-106">Добавьте следующий код в `solution` свойство.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-106">Add the following code to the `solution` property.</span></span>

    ```json
    "webApiPermissionRequests": [
      {
        "resource": "Microsoft Graph",
        "scope": "Calendars.ReadWrite"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "User.ReadBasic.All"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "Contacts.Read"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "People.Read"
      }
    ]
    ```

<span data-ttu-id="3b6a4-107">`Calendars.ReadWrite`Разрешение позволяет веб-части получать календарь пользователя и добавлять события с помощью Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-107">The `Calendars.ReadWrite` permission allows your web part to retrieve the user's calendar and add events using Microsoft Graph.</span></span> <span data-ttu-id="3b6a4-108">Остальные разрешения используются компонентами в наборе инструментов Microsoft Graph для отображения информации о участниках событий и организаторов.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-108">The other permissions are used by components in the Microsoft Graph Toolkit to render information about event attendees and organizers.</span></span>

## <a name="optional-test-token-acquisition"></a><span data-ttu-id="3b6a4-109">Необязательно: получение тестового маркера</span><span class="sxs-lookup"><span data-stu-id="3b6a4-109">Optional: Test token acquisition</span></span>

> [!NOTE]
> <span data-ttu-id="3b6a4-110">Остальные действия на этой странице являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-110">The rest of the steps on this page are optional.</span></span> <span data-ttu-id="3b6a4-111">Если вы предпочитаете немедленно вернуться к написанию кода Microsoft Graph, вы можете перейти к [просмотру календаря](/graph/tutorials/spfx?tutorial-step=3).</span><span class="sxs-lookup"><span data-stu-id="3b6a4-111">If you'd prefer to get to the Microsoft Graph coding right away, you can proceed to [Get a calendar view](/graph/tutorials/spfx?tutorial-step=3).</span></span>

<span data-ttu-id="3b6a4-112">Добавим в веб-часть временный код, чтобы проверить получение маркера.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-112">Let's add some temporary code to the web part to test token acquisition.</span></span>

1. <span data-ttu-id="3b6a4-113">Откройте **./СРК/вебпартс/графтуториал/графтуториалвебпарт.ТС** и добавьте приведенный ниже `import` оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-113">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { AadTokenProvider } from '@microsoft/sp-http';
    ```

1. <span data-ttu-id="3b6a4-114">Замените имеющуюся функцию `render` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-114">Replace the existing `render` function with the following.</span></span>

    ```typescript
    public render(): void {
    this.context.aadTokenProviderFactory
      .getTokenProvider()
      .then((provider: AadTokenProvider)=> {
      provider
        .getToken('https://graph.microsoft.com')
        .then((token: string) => {
          this.domElement.innerHTML = `
          <div class="${ styles.graphTutorial }">
            <div class="${ styles.container }">
              <div class="${ styles.row }">
                <div class="${ styles.column }">
                  <span class="${ styles.title }">Welcome to SharePoint!</span>
                  <p><code style="word-break: break-all;">${ token }</code></p>
                </div>
              </div>
            </div>
          </div>`;
        });
      });
    }
    ```

### <a name="deploy-the-web-part"></a><span data-ttu-id="3b6a4-115">Развертывание веб-части</span><span class="sxs-lookup"><span data-stu-id="3b6a4-115">Deploy the web part</span></span>

1. <span data-ttu-id="3b6a4-116">Выполните две следующие команды в утилите CLI, чтобы создать и упаковать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-116">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="3b6a4-117">Откройте браузер и перейдите к каталогу приложений SharePoint клиента.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-117">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="3b6a4-118">Выберите пункт меню **приложения для SharePoint** в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-118">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="3b6a4-119">Отправьте файл **./шарепоинт/солутион/граф-туториал.сппкг** .</span><span class="sxs-lookup"><span data-stu-id="3b6a4-119">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="3b6a4-120">В приглашении **доверять...** убедитесь, что в запросе указаны 4 разрешения Microsoft Graph, заданные в **package-solution.jsдля** файла.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-120">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="3b6a4-121">Выберите **сделать это решение доступным для всех сайтов в Организации** , а затем нажмите кнопку **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-121">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="3b6a4-122">Откройте [центр администрирования SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) с помощью учетной записи администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-122">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="3b6a4-123">В левом меню выберите **Дополнительно** , а затем — **доступ к API**.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-123">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="3b6a4-124">Выберите каждый из ожидающих запросов в пакете **Graph – Tutorial — клиентский — на стороне решения** и нажмите кнопку **утвердить**.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-124">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![Снимок экрана со страницей доступа к API центра администрирования SharePoint](images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="3b6a4-126">Тестирование веб-части</span><span class="sxs-lookup"><span data-stu-id="3b6a4-126">Test the web part</span></span>

1. <span data-ttu-id="3b6a4-127">Перейдите на сайт SharePoint, на котором необходимо протестировать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-127">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="3b6a4-128">Создайте новую страницу для тестирования веб-части.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-128">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="3b6a4-129">С помощью средства выбора веб-части найдите веб-часть **графтуториал** и добавьте ее на страницу.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-129">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Снимок экрана: веб-часть Графтуториал в средстве выбора веб-частей](images/add-web-part.png)

1. <span data-ttu-id="3b6a4-131">Маркер доступа печатается под знаком **Добро пожаловать в SharePoint!**</span><span class="sxs-lookup"><span data-stu-id="3b6a4-131">The access token is printed below the **Welcome to SharePoint!**</span></span> <span data-ttu-id="3b6a4-132">сообщение в веб-части.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-132">message in the web part.</span></span> <span data-ttu-id="3b6a4-133">Вы можете скопировать этот маркер и проанализировать его [https://jwt.ms/](https://jwt.ms/) , чтобы убедиться в том, что он содержит области разрешений, необходимые веб-части.</span><span class="sxs-lookup"><span data-stu-id="3b6a4-133">You can copy this token and parse it at [https://jwt.ms/](https://jwt.ms/) to confirm that it contains the permission scopes required by the web part.</span></span>

    ![Снимок экрана: веб-часть, отображающая маркер доступа](images/access-token.png)
