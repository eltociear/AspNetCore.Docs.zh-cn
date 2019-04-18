---
title: 使用 ASP.NET Core 的 gRPC 服务
author: juntaoluo
description: 使用 ASP.NET Core 中编写 gRPC 服务时，请了解基本概念。
monikerRange: '>= aspnetcore-3.0'
ms.author: johluo
ms.date: 03/08/2019
uid: grpc/aspnetcore
ms.openlocfilehash: c99a499fad824c3ac026f6f390c826c0418fc069
ms.sourcegitcommit: 57a974556acd09363a58f38c26f74dc21e0d4339
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59515357"
---
# <a name="grpc-services-with-aspnet-core"></a><span data-ttu-id="eeb35-103">使用 ASP.NET Core 的 gRPC 服务</span><span class="sxs-lookup"><span data-stu-id="eeb35-103">gRPC services with ASP.NET Core</span></span>

<span data-ttu-id="eeb35-104">本文档演示如何使用 ASP.NET Core gRPC 服务入门。</span><span class="sxs-lookup"><span data-stu-id="eeb35-104">This document shows how to get started with gRPC services using ASP.NET Core.</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-3.0.md)]

## <a name="get-started-with-grpc-service-in-aspnet-core"></a><span data-ttu-id="eeb35-105">开始使用 ASP.NET Core 中的 gRPC 服务</span><span class="sxs-lookup"><span data-stu-id="eeb35-105">Get started with gRPC service in ASP.NET Core</span></span>

[!INCLUDE[View or download sample code](~/includes/grpc/download.md)]

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="eeb35-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eeb35-106">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="eeb35-107">请参阅[gRPC 服务入门](xref:tutorials/grpc/grpc-start)有关如何创建 gRPC 项目的详细说明。</span><span class="sxs-lookup"><span data-stu-id="eeb35-107">See [Get started with gRPC services](xref:tutorials/grpc/grpc-start) for detailed instructions on how to create a gRPC project.</span></span>

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="eeb35-108">Visual Studio Code / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="eeb35-108">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

<span data-ttu-id="eeb35-109">在命令行中运行 `dotnet new grpc -o GrpcGreeter`。</span><span class="sxs-lookup"><span data-stu-id="eeb35-109">Run `dotnet new grpc -o GrpcGreeter` from the command line.</span></span>

---

## <a name="add-grpc-services-to-an-aspnet-core-app"></a><span data-ttu-id="eeb35-110">将 gRPC 服务添加到 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="eeb35-110">Add gRPC services to an ASP.NET Core app</span></span>

<span data-ttu-id="eeb35-111">gRPC 需要以下程序包：</span><span class="sxs-lookup"><span data-stu-id="eeb35-111">gRPC requires the following packages:</span></span>

* [<span data-ttu-id="eeb35-112">Grpc.AspNetCore.Server</span><span class="sxs-lookup"><span data-stu-id="eeb35-112">Grpc.AspNetCore.Server</span></span>](https://www.nuget.org/packages/Grpc.AspNetCore.Server)
* <span data-ttu-id="eeb35-113">[Google.Protobuf](https://www.nuget.org/packages/Google.Protobuf/)为 protobuf 消息 Api。</span><span class="sxs-lookup"><span data-stu-id="eeb35-113">[Google.Protobuf](https://www.nuget.org/packages/Google.Protobuf/) for protobuf message APIs.</span></span>
* [<span data-ttu-id="eeb35-114">Grpc.Tools</span><span class="sxs-lookup"><span data-stu-id="eeb35-114">Grpc.Tools</span></span>](https://www.nuget.org/packages/Grpc.Tools/)

### <a name="configure-grpc"></a><span data-ttu-id="eeb35-115">配置 gRPC</span><span class="sxs-lookup"><span data-stu-id="eeb35-115">Configure gRPC</span></span>

<span data-ttu-id="eeb35-116">使用启用 gRPC`AddGrpc`方法：</span><span class="sxs-lookup"><span data-stu-id="eeb35-116">gRPC is enabled with the `AddGrpc` method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcGreeter/Startup.cs?name=snippet&highlight=5)]

<span data-ttu-id="eeb35-117">每个 gRPC 服务添加到路由通过管道`MapGrpcService`方法：</span><span class="sxs-lookup"><span data-stu-id="eeb35-117">Each gRPC service is added to the routing pipeline through the `MapGrpcService` method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcGreeter/Startup.cs?name=snippet&highlight=21)]

<span data-ttu-id="eeb35-118">ASP.NET Core 中间件和功能共享路由管道，因此配置应用以提供额外的请求处理程序。</span><span class="sxs-lookup"><span data-stu-id="eeb35-118">ASP.NET Core middlewares and features share the routing pipeline, therefore an app can be configured to serve additional request handlers.</span></span> <span data-ttu-id="eeb35-119">与配置的 gRPC 服务同时工作的其他请求处理程序，如 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="eeb35-119">The additional request handlers, such as MVC controllers, work in parallel with the configured gRPC services.</span></span>

## <a name="integration-with-aspnet-core-apis"></a><span data-ttu-id="eeb35-120">与 ASP.NET Core Api 集成</span><span class="sxs-lookup"><span data-stu-id="eeb35-120">Integration with ASP.NET Core APIs</span></span>

<span data-ttu-id="eeb35-121">gRPC 服务具有完全访问权限的 ASP.NET Core 功能，如[依赖关系注入](xref:fundamentals/dependency-injection)(DI) 和[日志记录](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="eeb35-121">gRPC services have full access to the ASP.NET Core features such as [Dependency Injection](xref:fundamentals/dependency-injection) (DI) and [Logging](xref:fundamentals/logging/index).</span></span> <span data-ttu-id="eeb35-122">例如，服务实现可能会解决从通过构造函数的 DI 容器的记录器服务：</span><span class="sxs-lookup"><span data-stu-id="eeb35-122">For example, the service implementation can resolve a logger service from the DI container via the constructor:</span></span>

```csharp
public class GreeterService : Greeter.GreeterBase
{
    public GreeterService(ILogger<GreeterService> logger)
    {
    }
}
```

<span data-ttu-id="eeb35-123">默认情况下，gRPC 服务实现可以解析任何生存期 （单一实例、 作用域内或暂时） 与其他 DI 服务。</span><span class="sxs-lookup"><span data-stu-id="eeb35-123">By default, the gRPC service implementation can resolve other DI services with any lifetime (Singleton, Scoped, or Transient).</span></span>

### <a name="resolve-httpcontext-in-grpc-methods"></a><span data-ttu-id="eeb35-124">GRPC 方法中解决 HttpContext</span><span class="sxs-lookup"><span data-stu-id="eeb35-124">Resolve HttpContext in gRPC methods</span></span>

<span data-ttu-id="eeb35-125">GRPC API 提供了访问某些 HTTP/2 消息数据，如方法、 主机、 标头和尾部。</span><span class="sxs-lookup"><span data-stu-id="eeb35-125">The gRPC API provides access to some HTTP/2 message data, such as the method, host, header, and trailers.</span></span> <span data-ttu-id="eeb35-126">访问是通过`ServerCallContext`自变量传递给每个 gRPC 方法：</span><span class="sxs-lookup"><span data-stu-id="eeb35-126">Access is through the `ServerCallContext` argument passed to each gRPC method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcGreeter/Services/GreeterService.cs?highlight=3-4&name=snippet)]

<span data-ttu-id="eeb35-127">`ServerCallContext` 不提供完全访问权限`HttpContext`所有 ASP.NET Api 中。</span><span class="sxs-lookup"><span data-stu-id="eeb35-127">`ServerCallContext` does not provide full access to `HttpContext` in all ASP.NET APIs.</span></span> <span data-ttu-id="eeb35-128">`GetHttpContext`扩展方法提供了全面的`HttpContext`表示 ASP.NET Api 中的基础 HTTP/2 消息：</span><span class="sxs-lookup"><span data-stu-id="eeb35-128">The `GetHttpContext` extension method provides full access to the `HttpContext` representing the underlying HTTP/2 message in ASP.NET APIs:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcGreeter/Services/GreeterService.cs?name=snippet1)]

### <a name="request-body-data-rate-limit"></a><span data-ttu-id="eeb35-129">请求正文数据速率限制</span><span class="sxs-lookup"><span data-stu-id="eeb35-129">Request body data rate limit</span></span>

<span data-ttu-id="eeb35-130">默认情况下，Kestrel 服务器施加[最小请求正文数据速率](
<xref:Microsoft.AspNetCore.Server.Kestrel.Core.KestrelServerLimits.MinRequestBodyDataRate>)。</span><span class="sxs-lookup"><span data-stu-id="eeb35-130">By default, the Kestrel server imposes a [minimum request body data rate](
<xref:Microsoft.AspNetCore.Server.Kestrel.Core.KestrelServerLimits.MinRequestBodyDataRate>).</span></span> <span data-ttu-id="eeb35-131">有关流式处理客户端和双工流式处理的调用，可能不满足此速率和连接可能超时。最小值请求的正文 gRPC 服务包含流式处理客户端和双工流式处理调用时，必须禁用数据速率限制：</span><span class="sxs-lookup"><span data-stu-id="eeb35-131">For client streaming and duplex streaming calls, this rate may not be satisfied and the connection may be timed out. The minimum request body data rate limit must be disabled when the gRPC service includes client streaming and duplex streaming calls:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
         Host.CreateDefaultBuilder(args)
    .ConfigureWebHostDefaults(webBuilder =>
    {
        webBuilder.UseStartup<Startup>();
        webBuilder.ConfigureKestrel((context, options) =>
        {
            options.Limits.MinRequestBodyDataRate = null;
        });
    });
}
```

## <a name="additional-resources"></a><span data-ttu-id="eeb35-132">其他资源</span><span class="sxs-lookup"><span data-stu-id="eeb35-132">Additional resources</span></span>

* <xref:tutorials/grpc/grpc-start>
* <xref:grpc/index>
* <xref:grpc/basics>
* <xref:grpc/migration>