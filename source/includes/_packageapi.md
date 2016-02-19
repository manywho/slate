# Package API

            config.Routes.MapHttpRoute(
                name: "GetLatestFlowPackagePackage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/package/1/flow/{flowId}",
                defaults: new
                {
                    controller = "Package",
                    action = "GetLatestFlowPackage",
                    flowId = RouteParameter.Optional,
                    nullPasswords = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "ExportFlowPackagePackage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/package/1/flow/{flowId}/{flowVersionId}",
                defaults: new
                {
                    controller = "Package",
                    action = "ExportFlowPackage",
                    flowId = RouteParameter.Optional,
                    flowVersionId = RouteParameter.Optional,
                    nullPasswords = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "ImportFlowPackagePackage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/package/1/flow",
                defaults: new
                {
                    controller = "Package",
                    action = "ImportFlowPackage",
                    isActive = RouteParameter.Optional,
                    isDefault = RouteParameter.Optional,
                    uriMapping = RouteParameter.Optional
                }
            );
