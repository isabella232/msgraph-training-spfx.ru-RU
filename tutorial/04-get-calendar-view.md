---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823414"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="62c83-101">Платформа SharePoint Framework предоставляет [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) для совершения вызовов в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="62c83-101">The SharePoint Framework provides the [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) for making calls to Microsoft Graph.</span></span> <span data-ttu-id="62c83-102">Этот класс служит оболочкой [клиентской библиотеки JavaScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript), предварительно прошедшему проверку подлинности в текущем вошедшем в систему пользователе.</span><span class="sxs-lookup"><span data-stu-id="62c83-102">This class wraps the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript), pre-authenticating it with the current logged on user.</span></span>

<span data-ttu-id="62c83-103">Так как он упаковывает существующую библиотеку JavaScript, ее использование одинаково и полностью совместимо с определениями TypeScript Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="62c83-103">Because it wraps the existing JavaScript library, its usage is the same, and it's fully compatible with the Microsoft Graph TypeScript definitions.</span></span>

## <a name="get-the-users-calendar"></a><span data-ttu-id="62c83-104">Получение календаря пользователя</span><span class="sxs-lookup"><span data-stu-id="62c83-104">Get the user's calendar</span></span>

1. <span data-ttu-id="62c83-105">Откройте **./СРК/вебпартс/графтуториал/графтуториалвебпарт.ТС** и добавьте приведенные ниже `import` операторы в начало файла.</span><span class="sxs-lookup"><span data-stu-id="62c83-105">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statements at the top of the file.</span></span>

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. <span data-ttu-id="62c83-106">Добавьте указанную ниже функцию в класс **графтуториалвебпарт** , чтобы отобразить сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="62c83-106">Add the following function to the **GraphTutorialWebPart** class to render an error.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. <span data-ttu-id="62c83-107">Добавьте указанную ниже функцию, чтобы распечатать события в календаре пользователя.</span><span class="sxs-lookup"><span data-stu-id="62c83-107">Add the following function to print out the events in the user's calendar.</span></span>

    ```typescript
    private renderCalendarView(events: MicrosoftGraph.Event[]) : void {
      const viewContainer = this.domElement.querySelector('#calendarView');
      let html = '';

      // Temporary: print events as a list
      for(const event of events) {
        html += `
          <p class="${ styles.description }">Subject: ${event.subject}</p>
          <p class="${ styles.description }">Organizer: ${event.organizer.emailAddress.name}</p>
          <p class="${ styles.description }">Start: ${event.start.dateTime}</p>
          <p class="${ styles.description }">End: ${event.end.dateTime}</p>
          `;
      }

      viewContainer.innerHTML = html;
    }
    ```

1. <span data-ttu-id="62c83-108">Замените имеющуюся функцию `render` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="62c83-108">Replace the existing `render` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    <span data-ttu-id="62c83-109">Обратите внимание на то, что делает этот код.</span><span class="sxs-lookup"><span data-stu-id="62c83-109">Notice what this code does.</span></span>

    - <span data-ttu-id="62c83-110">Он используется `this.context.msGraphClientFactory.getClient` для получения объекта **MSGraphClient** , прошедшего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="62c83-110">It uses `this.context.msGraphClientFactory.getClient` to get an authenticated **MSGraphClient** object.</span></span>
    - <span data-ttu-id="62c83-111">Он вызывает `/me/calendarView` конечную точку, устанавливая `startDateTime` `endDateTime` Параметры и параметры запроса в начало и конец текущей недели.</span><span class="sxs-lookup"><span data-stu-id="62c83-111">It calls the `/me/calendarView` endpoint, setting the `startDateTime` and `endDateTime` query parameters to the start and end of the current week.</span></span>
    - <span data-ttu-id="62c83-112">Он используется `select` для ограничения числа возвращаемых полей, запрашивая только те поля, которые использует приложение.</span><span class="sxs-lookup"><span data-stu-id="62c83-112">It uses `select` to limit which fields are returned, requesting only the fields the app uses.</span></span>
    - <span data-ttu-id="62c83-113">Он используется `orderby` для сортировки событий по времени начала.</span><span class="sxs-lookup"><span data-stu-id="62c83-113">It uses `orderby` to sort the events by their start time.</span></span>
    - <span data-ttu-id="62c83-114">Он используется `top` для ограничения результатов до 25 событий.</span><span class="sxs-lookup"><span data-stu-id="62c83-114">It uses `top` to limit the results to 25 events.</span></span>

## <a name="deploy-the-web-part"></a><span data-ttu-id="62c83-115">Развертывание веб-части</span><span class="sxs-lookup"><span data-stu-id="62c83-115">Deploy the web part</span></span>

1. <span data-ttu-id="62c83-116">Выполните две следующие команды в утилите CLI, чтобы создать и упаковать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="62c83-116">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="62c83-117">Откройте браузер и перейдите к каталогу приложений SharePoint клиента.</span><span class="sxs-lookup"><span data-stu-id="62c83-117">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="62c83-118">Выберите пункт меню **приложения для SharePoint** в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="62c83-118">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="62c83-119">Отправьте файл **./шарепоинт/солутион/граф-туториал.сппкг** .</span><span class="sxs-lookup"><span data-stu-id="62c83-119">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="62c83-120">В приглашении **доверять...** убедитесь, что в запросе указаны 4 разрешения Microsoft Graph, заданные в **package-solution.jsдля** файла.</span><span class="sxs-lookup"><span data-stu-id="62c83-120">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="62c83-121">Выберите **сделать это решение доступным для всех сайтов в Организации** , а затем нажмите кнопку **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="62c83-121">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="62c83-122">Если вы еще не утвердили разрешения графов для веб-части, сделайте это сейчас.</span><span class="sxs-lookup"><span data-stu-id="62c83-122">If you have not already approved the Graph permissions for your web part, do that now.</span></span>

    1. <span data-ttu-id="62c83-123">Откройте [центр администрирования SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) с помощью учетной записи администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="62c83-123">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

    1. <span data-ttu-id="62c83-124">В левом меню выберите **Дополнительно** , а затем — **доступ к API**.</span><span class="sxs-lookup"><span data-stu-id="62c83-124">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

    1. <span data-ttu-id="62c83-125">Выберите каждый из ожидающих запросов в пакете **Graph – Tutorial — клиентский — на стороне решения** и нажмите кнопку **утвердить**.</span><span class="sxs-lookup"><span data-stu-id="62c83-125">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

        ![Снимок экрана со страницей доступа к API центра администрирования SharePoint](images/api-access.png)

## <a name="test-the-web-part"></a><span data-ttu-id="62c83-127">Тестирование веб-части</span><span class="sxs-lookup"><span data-stu-id="62c83-127">Test the web part</span></span>

1. <span data-ttu-id="62c83-128">Перейдите на сайт SharePoint, на котором необходимо протестировать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="62c83-128">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="62c83-129">Создайте новую страницу для тестирования веб-части.</span><span class="sxs-lookup"><span data-stu-id="62c83-129">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="62c83-130">С помощью средства выбора веб-части найдите веб-часть **графтуториал** и добавьте ее на страницу.</span><span class="sxs-lookup"><span data-stu-id="62c83-130">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Снимок экрана: веб-часть Графтуториал в средстве выбора веб-частей](images/add-web-part.png)

1. <span data-ttu-id="62c83-132">Список событий за текущую неделю печатается в веб-части.</span><span class="sxs-lookup"><span data-stu-id="62c83-132">A list of events for the current week are printed in the web part.</span></span>

    ![Снимок экрана: веб-часть, отображающая список событий](images/calendar-list.png)
