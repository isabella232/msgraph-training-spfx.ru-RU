---
ms.openlocfilehash: ee9addcbcf58fa971b3e67fb3d84cfb36bf275dd
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823426"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="3bfc9-101">В этом разделе описывается использование [набора средств Microsoft Graph](https://docs.microsoft.com/graph/toolkit/overview) для замены простого списка событий с богатым пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-101">In this section, you'll use the [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to replace the simple list of events with rich UI.</span></span>

<span data-ttu-id="3bfc9-102">Набор средств предоставляет [компонент повестки](https://docs.microsoft.com/graph/toolkit/components/agenda), который хорошо подходит для отображения нашего списка событий.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-102">The toolkit provides an [Agenda component](https://docs.microsoft.com/graph/toolkit/components/agenda), which is well-suited to render our list of events.</span></span>

## <a name="update-the-web-part"></a><span data-ttu-id="3bfc9-103">Обновление веб-части</span><span class="sxs-lookup"><span data-stu-id="3bfc9-103">Update the web part</span></span>

1. <span data-ttu-id="3bfc9-104">Открыть **./СРК/вебпартс/графтуториал/графтуториалвебпарт.модуле.СКСс**.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-104">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.module.scss**.</span></span> <span data-ttu-id="3bfc9-105">Измените значение `background-color` атрибута в `.row` записи на `$ms-color-white` .</span><span class="sxs-lookup"><span data-stu-id="3bfc9-105">Change the value of the `background-color` attribute in the `.row` entry to `$ms-color-white`.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="rowScssSnippet" highlight="4":::

1. <span data-ttu-id="3bfc9-106">Добавьте следующую запись в `.graphTutorial` запись.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-106">Add the following entry inside the `.graphTutorial` entry.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="addSocialBtnSnippet":::

1. <span data-ttu-id="3bfc9-107">Откройте **./СРК/вебпартс/графтуториал/графтуториалвебпарт.ТС** и добавьте приведенный ниже `import` оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-107">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { Providers, SharePointProvider, MgtAgenda } from '@microsoft/mgt';
    ```

1. <span data-ttu-id="3bfc9-108">Добавьте указанную ниже функцию в класс **графтуториалвебпарт** , чтобы инициализировать набор инструментов.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-108">Add the following function to the **GraphTutorialWebPart** class to initialize the toolkit.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="onInitSnippet":::

1. <span data-ttu-id="3bfc9-109">Замените имеющуюся функцию `renderCalendarView` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-109">Replace the existing `renderCalendarView` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderCalendarViewSnippet":::

    <span data-ttu-id="3bfc9-110">Этот базовый список заменяется компонентом **повестки** из набора инструментов.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-110">This replaces the basic list with the **Agenda** component from the toolkit.</span></span>

1. <span data-ttu-id="3bfc9-111">Выполните построение, упаковку и повторную отправку веб-части, а затем обновите страницу, на которой она тестируется.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-111">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

    ![Снимок экрана: веб-часть с компонентом повестки](images/mgt-agenda.png)

## <a name="an-alternate-approach"></a><span data-ttu-id="3bfc9-113">Альтернативный подход</span><span class="sxs-lookup"><span data-stu-id="3bfc9-113">An alternate approach</span></span>

<span data-ttu-id="3bfc9-114">На этом шаге у вас есть код, который:</span><span class="sxs-lookup"><span data-stu-id="3bfc9-114">At this point, you have code that:</span></span>

- <span data-ttu-id="3bfc9-115">Использование **MSGraphClient** для получения представления календаря пользователя за текущую неделю из Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-115">Uses the **MSGraphClient** to get the user's calendar view for the current week from Microsoft Graph.</span></span>
- <span data-ttu-id="3bfc9-116">Добавьте эти события в компонент **повестку** из набора средств Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-116">Add those events to the **Agenda** component from the Microsoft Graph Toolkit.</span></span>

<span data-ttu-id="3bfc9-117">Благодаря этому подходу вы получите полный контроль над вызовом API Graph и можете выполнить любую обработку событий перед отображением.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-117">With this approach, you have full control over the Graph API call and can do any processing of the events prior to rendering that you want.</span></span> <span data-ttu-id="3bfc9-118">Тем не менее, если это не требуется, вы можете упростить, разрешив компоненту **повестки** работать.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-118">However, if that isn't required, you can simplify by letting the **Agenda** component do the work for you.</span></span>

<span data-ttu-id="3bfc9-119">Все компоненты набора средств Microsoft Graph могут выполнять все подходящие вызовы API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-119">All Microsoft Graph Toolkit components are capable of making all of the relevant API calls to the Microsoft Graph.</span></span> <span data-ttu-id="3bfc9-120">Например, просто добавив компонент **повестки** в веб-часть, а не устанавливая свойства, веб-часть будет использовать параметры по умолчанию для получения событий за текущий день.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-120">For example, by just adding the **Agenda** component to the web part, and not setting any properties, the web part would use its default settings to get events for the current day.</span></span> <span data-ttu-id="3bfc9-121">Рассмотрим, как можно добиться того же результата (события за текущую неделю).</span><span class="sxs-lookup"><span data-stu-id="3bfc9-121">Let's look at how we can achieve the same results we currently have (events for the current week).</span></span>

1. <span data-ttu-id="3bfc9-122">Замените существующий `render` метод на приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-122">Replace the existing `render` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="alternateRenderSnippet":::

    <span data-ttu-id="3bfc9-123">Теперь, вместо вызова API в `render` , просто добавьте `mgt-agenda` элемент непосредственно в HTML.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-123">Now, instead of making an API call in `render`, you simply add an `mgt-agenda` element directly into the HTML.</span></span> <span data-ttu-id="3bfc9-124">При установке `date` на начало недели и `days` до 7 компонент будет выполнять тот же вызов API, что и Предыдущая версия `render` .</span><span class="sxs-lookup"><span data-stu-id="3bfc9-124">By setting `date` to the start of the week, and `days` to 7, the component will make the same API call the previous version of `render` was making.</span></span>

1. <span data-ttu-id="3bfc9-125">Добавьте следующую пустую функцию в класс **графтуториалвебпарт** .</span><span class="sxs-lookup"><span data-stu-id="3bfc9-125">Add the following empty function to the **GraphTutorialWebPart** class.</span></span>

    ```typescript
    private async addSocialToCalendar() {}
    ```

    > [!NOTE]
    > <span data-ttu-id="3bfc9-126">Мы также добавили в веб-часть кнопку **Добавить группу социального контента** и добавили метод в `addSocialToCalendar` качестве прослушивателя событий.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-126">We also added an **Add team social** button to the web part, and added the `addSocialToCalendar` method as an event listener.</span></span>  <span data-ttu-id="3bfc9-127">Вы реализуете код, приведенный в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-127">You'll implement the code behind that in the next section.</span></span> <span data-ttu-id="3bfc9-128">Пока хотите, чтобы код был скомпилирован.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-128">For now, we just want the code to compile.</span></span>

1. <span data-ttu-id="3bfc9-129">Выполните построение, упаковку и повторную отправку веб-части, а затем обновите страницу, на которой она тестируется.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-129">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span> <span data-ttu-id="3bfc9-130">Представление должно совпадать с предыдущим тестом.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-130">The view should be the same as your previous test.</span></span>

### <a name="using-the-toolkit-vs-making-api-calls"></a><span data-ttu-id="3bfc9-131">Использование вызовов API для набора средств и совершения вызовов API</span><span class="sxs-lookup"><span data-stu-id="3bfc9-131">Using the toolkit vs making API calls</span></span>

<span data-ttu-id="3bfc9-132">На этом шаге вы, возможно, захотите узнать, почему у вас возникли проблемы с использованием **MSGraphClient** , когда набор инструментов выполняет свою работу.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-132">At this point you may be wondering why you went through the trouble of using the **MSGraphClient** at all, when the toolkit does the work for you.</span></span> <span data-ttu-id="3bfc9-133">Набор средств разработки предназначен для отображения результатов, которые вы запрашиваете из Microsoft Graph, например списка событий.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-133">The toolkit is designed for rendering results that you query from Microsoft Graph, such as a list of events.</span></span> <span data-ttu-id="3bfc9-134">Однако существуют сценарии, в которых необходимо самостоятельно совершать вызовы API.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-134">However, there are scenarios where making API calls yourself is necessary.</span></span>

- <span data-ttu-id="3bfc9-135">Все вызовы API, которые не являются `GET` запросами.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-135">Any API calls that are not a `GET` request.</span></span> <span data-ttu-id="3bfc9-136">Например, создание нового события в календаре или обновление номера телефона пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-136">For example, creating a new event on the calendar, or updating a user's phone number.</span></span>
- <span data-ttu-id="3bfc9-137">Вызовы API для получения данных, которые предназначены для использования в фоновом режиме и не отображаются напрямую.</span><span class="sxs-lookup"><span data-stu-id="3bfc9-137">API calls to get data that's intended to be used "behind the scenes" and not rendered directly.</span></span>
