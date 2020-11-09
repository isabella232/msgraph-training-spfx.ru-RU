---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823386"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ac3a5-101">В этом разделе вы обновите веб-часть, чтобы позволить пользователю добавить событие в свой календарь для еженедельного социальныхого часа группы.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-101">In this section you'll update the web part to allow the user to add an event to their calendar for the team's weekly social hour.</span></span> <span data-ttu-id="ac3a5-102">В этом сценарии у группы есть еженедельный социальный час с 4 по пятницу.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-102">In this scenario, the team has a weekly social hour at 4 PM on Friday.</span></span>

1. <span data-ttu-id="ac3a5-103">Откройте **./СРК/вебпартс/графтуториал/графтуториалвебпарт.ТС** и замените существующий `addSocialToCalendar()` метод на приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-103">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and replace the existing `addSocialToCalendar()` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    <span data-ttu-id="ac3a5-104">Рассмотрите, что делает этот код.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-104">Consider what this code does.</span></span>

    - <span data-ttu-id="ac3a5-105">Он определяет следующую предстоящую пятницу и создает **дату** для 4 РМ в этот день.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-105">It determines the next upcoming Friday and constructs a **Date** for 4 PM on that day.</span></span>
    - <span data-ttu-id="ac3a5-106">Он создает новый объект **MicrosoftGraph. Event** , устанавливая для него значение **даты** и заканчивая на час позже.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-106">It constructs a new **MicrosoftGraph.Event** object, setting the start to the value of the **Date** , and the end for one hour later.</span></span>
    - <span data-ttu-id="ac3a5-107">Он использует **MSGraphClient** для публикации нового события в `/me/events` конечной точке.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-107">It uses the **MSGraphClient** to POST the new event to the `/me/events` endpoint.</span></span>
    - <span data-ttu-id="ac3a5-108">Он повторно отрисовывает веб-часть, чтобы представление обновлялось с новым событием.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-108">It re-renders the web part so the view is updated with the new event.</span></span>

1. <span data-ttu-id="ac3a5-109">Выполните построение, упаковку и повторную отправку веб-части, а затем обновите страницу, на которой она тестируется.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-109">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

1. <span data-ttu-id="ac3a5-110">Нажмите кнопку **Добавить группу социального контента** .</span><span class="sxs-lookup"><span data-stu-id="ac3a5-110">Click the **Add team social** button.</span></span> <span data-ttu-id="ac3a5-111">После обновления страницы прокрутите окно вниз до пункта пятница и найдите новое событие.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-111">Once the page refreshes, scroll down to Friday and find the new event.</span></span>

    ![Снимок экрана: вновь созданное событие, отображаемое в веб-части](images/new-event.png)
