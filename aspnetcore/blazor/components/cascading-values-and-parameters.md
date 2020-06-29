---
title: ASP.NET Core Blazor 级联值和参数
author: guardrex
description: 了解如何将数据从祖先组件流向子代组件。
monikerRange: '>= aspnetcore-3.1'
ms.author: riande
ms.custom: mvc
ms.date: 06/16/2020
no-loc:
- Blazor
- Identity
- Let's Encrypt
- Razor
- SignalR
uid: blazor/components/cascading-values-and-parameters
ms.openlocfilehash: 70f379b3b0e48dbb340f319f3346bbbf44588740
ms.sourcegitcommit: 490434a700ba8c5ed24d849bd99d8489858538e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85103205"
---
# <a name="aspnet-core-blazor-cascading-values-and-parameters"></a><span data-ttu-id="2e077-103">ASP.NET Core Blazor 级联值和参数</span><span class="sxs-lookup"><span data-stu-id="2e077-103">ASP.NET Core Blazor cascading values and parameters</span></span>

## <a name="cascading-values-and-parameters"></a><span data-ttu-id="2e077-104">级联值和参数</span><span class="sxs-lookup"><span data-stu-id="2e077-104">Cascading values and parameters</span></span>

<span data-ttu-id="2e077-105">在某些情况下，使用[组件参数](xref:blazor/components/index#component-parameters)将数据从祖先组件流向子代组件不太方便，尤其是在有多个组件层时。</span><span class="sxs-lookup"><span data-stu-id="2e077-105">In some scenarios, it's inconvenient to flow data from an ancestor component to a descendent component using [component parameters](xref:blazor/components/index#component-parameters), especially when there are several component layers.</span></span> <span data-ttu-id="2e077-106">级联值和参数提供了一种方便的方法，使祖先组件为其所有子代组件提供值，从而解决了此问题。</span><span class="sxs-lookup"><span data-stu-id="2e077-106">Cascading values and parameters solve this problem by providing a convenient way for an ancestor component to provide a value to all of its descendent components.</span></span> <span data-ttu-id="2e077-107">级联值和参数还提供了一种协调组件的方法。</span><span class="sxs-lookup"><span data-stu-id="2e077-107">Cascading values and parameters also provide an approach for components to coordinate.</span></span>

### <a name="theme-example"></a><span data-ttu-id="2e077-108">主题示例</span><span class="sxs-lookup"><span data-stu-id="2e077-108">Theme example</span></span>

<span data-ttu-id="2e077-109">在示例应用的以下示例中，`ThemeInfo` 类指定了要沿组件层次结构向下传递的主题信息，以便应用中给定部分内的所有按钮共享相同样式。</span><span class="sxs-lookup"><span data-stu-id="2e077-109">In the following example from the sample app, the `ThemeInfo` class specifies the theme information to flow down the component hierarchy so that all of the buttons within a given part of the app share the same style.</span></span>

<span data-ttu-id="2e077-110">UIThemeClasses/ThemeInfo.cs\*\*：</span><span class="sxs-lookup"><span data-stu-id="2e077-110">*UIThemeClasses/ThemeInfo.cs*:</span></span>

```csharp
public class ThemeInfo
{
    public string ButtonClass { get; set; }
}
```

<span data-ttu-id="2e077-111">祖先组件可以使用级联值组件提供级联值。</span><span class="sxs-lookup"><span data-stu-id="2e077-111">An ancestor component can provide a cascading value using the Cascading Value component.</span></span> <span data-ttu-id="2e077-112"><xref:Microsoft.AspNetCore.Components.CascadingValue%601> 组件包装组件层次结构的子树，并向该子树内的所有组件提供单个值。</span><span class="sxs-lookup"><span data-stu-id="2e077-112">The <xref:Microsoft.AspNetCore.Components.CascadingValue%601> component wraps a subtree of the component hierarchy and supplies a single value to all components within that subtree.</span></span>

<span data-ttu-id="2e077-113">例如，示例应用将应用布局之一中的主题信息 (`ThemeInfo`) 指定为组成 `@Body` 属性布局正文的所有组件的级联参数。</span><span class="sxs-lookup"><span data-stu-id="2e077-113">For example, the sample app specifies theme information (`ThemeInfo`) in one of the app's layouts as a cascading parameter for all components that make up the layout body of the `@Body` property.</span></span> <span data-ttu-id="2e077-114">在布局组件中为 `ButtonClass` 分配了 `btn-success` 的值。</span><span class="sxs-lookup"><span data-stu-id="2e077-114">`ButtonClass` is assigned a value of `btn-success` in the layout component.</span></span> <span data-ttu-id="2e077-115">任何子代组件都可以通过 `ThemeInfo` 级联对象使用此属性。</span><span class="sxs-lookup"><span data-stu-id="2e077-115">Any descendent component can consume this property through the `ThemeInfo` cascading object.</span></span>

<span data-ttu-id="2e077-116">`CascadingValuesParametersLayout` 组件：</span><span class="sxs-lookup"><span data-stu-id="2e077-116">`CascadingValuesParametersLayout` component:</span></span>

```razor
@inherits LayoutComponentBase
@using BlazorSample.UIThemeClasses

<div class="container-fluid">
    <div class="row">
        <div class="col-sm-3">
            <NavMenu />
        </div>
        <div class="col-sm-9">
            <CascadingValue Value="theme">
                <div class="content px-4">
                    @Body
                </div>
            </CascadingValue>
        </div>
    </div>
</div>

@code {
    private ThemeInfo theme = new ThemeInfo { ButtonClass = "btn-success" };
}
```

<span data-ttu-id="2e077-117">为了使用级联值，组件使用 [`[CascadingParameter]`](xref:Microsoft.AspNetCore.Components.CascadingParameterAttribute) 特性来声明级联参数。</span><span class="sxs-lookup"><span data-stu-id="2e077-117">To make use of cascading values, components declare cascading parameters using the [`[CascadingParameter]`](xref:Microsoft.AspNetCore.Components.CascadingParameterAttribute) attribute.</span></span> <span data-ttu-id="2e077-118">级联值按类型绑定到级联参数。</span><span class="sxs-lookup"><span data-stu-id="2e077-118">Cascading values are bound to cascading parameters by type.</span></span>

<span data-ttu-id="2e077-119">在示例应用中，`CascadingValuesParametersTheme` 组件将 `ThemeInfo` 级联值绑定到级联参数。</span><span class="sxs-lookup"><span data-stu-id="2e077-119">In the sample app, the `CascadingValuesParametersTheme` component binds the `ThemeInfo` cascading value to a cascading parameter.</span></span> <span data-ttu-id="2e077-120">该参数用于为组件显示的按钮之一设置 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="2e077-120">The parameter is used to set the CSS class for one of the buttons displayed by the component.</span></span>

<span data-ttu-id="2e077-121">`CascadingValuesParametersTheme` 组件：</span><span class="sxs-lookup"><span data-stu-id="2e077-121">`CascadingValuesParametersTheme` component:</span></span>

```razor
@page "/cascadingvaluesparameterstheme"
@layout CascadingValuesParametersLayout
@using BlazorSample.UIThemeClasses

<h1>Cascading Values & Parameters</h1>

<p>Current count: @currentCount</p>

<p>
    <button class="btn" @onclick="IncrementCount">
        Increment Counter (Unthemed)
    </button>
</p>

<p>
    <button class="btn @ThemeInfo.ButtonClass" @onclick="IncrementCount">
        Increment Counter (Themed)
    </button>
</p>

@code {
    private int currentCount = 0;

    [CascadingParameter]
    protected ThemeInfo ThemeInfo { get; set; }

    private void IncrementCount()
    {
        currentCount++;
    }
}
```

<span data-ttu-id="2e077-122">若要在同一子树内级联多个相同类型的值，请向每个 <xref:Microsoft.AspNetCore.Components.CascadingValue%601> 组件及其相应的 [`[CascadingParameter]`](xref:Microsoft.AspNetCore.Components.CascadingParameterAttribute) 特性提供唯一的 <xref:Microsoft.AspNetCore.Components.CascadingValue%601.Name%2A> 字符串。</span><span class="sxs-lookup"><span data-stu-id="2e077-122">To cascade multiple values of the same type within the same subtree, provide a unique <xref:Microsoft.AspNetCore.Components.CascadingValue%601.Name%2A> string to each <xref:Microsoft.AspNetCore.Components.CascadingValue%601> component and its corresponding [`[CascadingParameter]`](xref:Microsoft.AspNetCore.Components.CascadingParameterAttribute) attribute.</span></span> <span data-ttu-id="2e077-123">在下面的示例中，两个 <xref:Microsoft.AspNetCore.Components.CascadingValue%601> 组件按名称级联 `MyCascadingType` 的不同实例：</span><span class="sxs-lookup"><span data-stu-id="2e077-123">In the following example, two <xref:Microsoft.AspNetCore.Components.CascadingValue%601> components cascade different instances of `MyCascadingType` by name:</span></span>

```razor
<CascadingValue Value=@parentCascadeParameter1 Name="CascadeParam1">
    <CascadingValue Value=@ParentCascadeParameter2 Name="CascadeParam2">
        ...
    </CascadingValue>
</CascadingValue>

@code {
    private MyCascadingType parentCascadeParameter1;

    [Parameter]
    public MyCascadingType ParentCascadeParameter2 { get; set; }

    ...
}
```

<span data-ttu-id="2e077-124">在子代组件中，级联参数按名称从祖先组件中相应的级联值接收值：</span><span class="sxs-lookup"><span data-stu-id="2e077-124">In a descendant component, the cascaded parameters receive their values from the corresponding cascaded values in the ancestor component by name:</span></span>

```razor
...

@code {
    [CascadingParameter(Name = "CascadeParam1")]
    protected MyCascadingType ChildCascadeParameter1 { get; set; }
    
    [CascadingParameter(Name = "CascadeParam2")]
    protected MyCascadingType ChildCascadeParameter2 { get; set; }
}
```

### <a name="tabset-example"></a><span data-ttu-id="2e077-125">TabSet 示例</span><span class="sxs-lookup"><span data-stu-id="2e077-125">TabSet example</span></span>

<span data-ttu-id="2e077-126">级联参数还允许组件跨组件层次结构进行协作。</span><span class="sxs-lookup"><span data-stu-id="2e077-126">Cascading parameters also enable components to collaborate across the component hierarchy.</span></span> <span data-ttu-id="2e077-127">例如，请考虑示例应用中的以下 TabSet 示例\*\*。</span><span class="sxs-lookup"><span data-stu-id="2e077-127">For example, consider the following *TabSet* example in the sample app.</span></span>

<span data-ttu-id="2e077-128">该示例应用包含一个选项卡实现的 `ITab` 接口：</span><span class="sxs-lookup"><span data-stu-id="2e077-128">The sample app has an `ITab` interface that tabs implement:</span></span>

[!code-csharp[](../common/samples/3.x/BlazorWebAssemblySample/UIInterfaces/ITab.cs)]

<span data-ttu-id="2e077-129">`CascadingValuesParametersTabSet` 组件使用 `TabSet` 组件，其中包含多个 `Tab` 组件：</span><span class="sxs-lookup"><span data-stu-id="2e077-129">The `CascadingValuesParametersTabSet` component uses the `TabSet` component, which contains several `Tab` components:</span></span>

```razor
<TabSet>
    <Tab Title="First tab">
        <h4>Greetings from the first tab!</h4>

        <label>
            <input type="checkbox" @bind="showThirdTab" />
            Toggle third tab
        </label>
    </Tab>
    <Tab Title="Second tab">
        <h4>The second tab says Hello World!</h4>
    </Tab>

    @if (showThirdTab)
    {
        <Tab Title="Third tab">
            <h4>Welcome to the disappearing third tab!</h4>
            <p>Toggle this tab from the first tab.</p>
        </Tab>
    }
</TabSet>
```

<span data-ttu-id="2e077-130">子 `Tab` 组件不会作为参数显式传递给 `TabSet`。</span><span class="sxs-lookup"><span data-stu-id="2e077-130">The child `Tab` components aren't explicitly passed as parameters to the `TabSet`.</span></span> <span data-ttu-id="2e077-131">子 `Tab` 组件是 `TabSet` 的子内容的一部分。</span><span class="sxs-lookup"><span data-stu-id="2e077-131">Instead, the child `Tab` components are part of the child content of the `TabSet`.</span></span> <span data-ttu-id="2e077-132">但 `TabSet` 仍需要了解每个 `Tab` 组件，以便它可以呈现标头和活动选项卡。若要在不需要额外代码的情况下启用此协调，`TabSet` 组件可以将自身作为级联值提供，然后由子代 `Tab` 组件选取\*\*。</span><span class="sxs-lookup"><span data-stu-id="2e077-132">However, the `TabSet` still needs to know about each `Tab` component so that it can render the headers and the active tab. To enable this coordination without requiring additional code, the `TabSet` component *can provide itself as a cascading value* that is then picked up by the descendent `Tab` components.</span></span>

<span data-ttu-id="2e077-133">`TabSet` 组件：</span><span class="sxs-lookup"><span data-stu-id="2e077-133">`TabSet` component:</span></span>

[!code-razor[](../common/samples/3.x/BlazorWebAssemblySample/Components/TabSet.razor)]

<span data-ttu-id="2e077-134">子代 `Tab` 组件将包含的 `TabSet` 作为级联参数捕获，因此 `Tab` 组件会将其自身添加到 `TabSet` 并在处于活动状态的选项卡上进行协调。</span><span class="sxs-lookup"><span data-stu-id="2e077-134">The descendent `Tab` components capture the containing `TabSet` as a cascading parameter, so the `Tab` components add themselves to the `TabSet` and coordinate on which tab is active.</span></span>

<span data-ttu-id="2e077-135">`Tab` 组件：</span><span class="sxs-lookup"><span data-stu-id="2e077-135">`Tab` component:</span></span>

[!code-razor[](../common/samples/3.x/BlazorWebAssemblySample/Components/Tab.razor)]