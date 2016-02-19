# Draw API


            // Draw
            config.Routes.MapHttpRoute(
                name: "DrawLogin",
                routeTemplate: "api/draw/1/authentication",
                defaults: new
                {
                    controller = "Draw",
                    action = "Login"
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawSetFlowActivationAndDefault",
                routeTemplate: "api/draw/1/flow/activation/{flowId}/{flowVersionId}/{isDefault}/{isActivated}",
                defaults: new
                {
                    controller = "Draw",
                    action = "SetFlowActivationAndDefault",
                    flowId = RouteParameter.Optional,
                    flowVersionId = RouteParameter.Optional,
                    isDefault = RouteParameter.Optional,
                    isActivated = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawSnapShotFlow",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/draw/1/flow/snap/{flowId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "SnapShotFlow",
                    flowId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawGetFlowSnapShotImageVersions",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/flow/snap/{flowId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "GetFlowSnapShotImageVersions",
                    flowId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawGetFlowSnapShotImage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/flow/snap/{flowId}/{flowVersionId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "GetFlowSnapShotImage",
                    flowId = RouteParameter.Optional,
                    flowVersionId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawSaveFlowGraph",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/draw/1/graph/flow",
                defaults: new
                {
                    controller = "Draw",
                    action = "SaveFlowGraph"
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawLoadFlowGraph",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/graph/flow/{flowId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "LoadFlowGraph",
                    flowId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawFlowGraphChangeAvailable",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/graph/ping/flow/{flowId}/{editingToken}",
                defaults: new
                {
                    controller = "Draw",
                    action = "FlowGraphChangeAvailable",
                    flowId = RouteParameter.Optional,
                    editingToken = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                            name: "DrawRevertFlow",
                            constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                            routeTemplate: "api/draw/1/flow/revert/{flowId}/{flowVersionId}",
                            defaults: new
                            {
                                controller = "Draw",
                                action = "RevertFlow",
                                flowId = RouteParameter.Optional,
                                flowVersionId = RouteParameter.Optional
                            }
            );


            config.Routes.MapHttpRoute(
                name: "DrawRemoveElementFromFlow",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/draw/1/element/flow/{flowId}/{elementType}/{elementId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "RemoveElementFromFlow",
                    flowId = RouteParameter.Optional,
                    elementType = RouteParameter.Optional,
                    elementId = RouteParameter.Optional
                }
            );


            config.Routes.MapHttpRoute(
                name: "DeleteDuplicateTypesFromService",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/draw/1/element/service/{serviceElementId}/duplicateTypes",
                defaults: new
                {
                    controller = "Draw",
                    action = "DeleteDuplicateTypesFromService",
                    serviceElementId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawLoadSharedElementReferences",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/element/value/reference",
                defaults: new
                {
                    controller = "Draw",
                    action = "LoadSharedElementReferences",
                    filter = RouteParameter.Optional
                }
            );



            config.Routes.MapHttpRoute(
                name: "DrawLoadMacroElements",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/element/macro",
                defaults: new
                {
                    controller = "Draw",
                    action = "LoadMacroElements",
                    filter = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawSaveMacroElement",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/draw/1/element/macro",
                defaults: new
                {
                    controller = "Draw",
                    action = "SaveMacroElement"
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawDeleteMacroElement",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/draw/1/element/macro/{macroElementId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "DeleteMacroElement",
                    macroElementId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawLoadMacroElement",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/element/macro/{macroElementId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "LoadMacroElement",
                    macroElementId = RouteParameter.Optional
                }
            );


            config.Routes.MapHttpRoute(
                name: "DrawGetFlows",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/flow",
                defaults: new
                {
                    controller = "Draw",
                    action = "GetFlows",
                    filter = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawGetLatestFlow",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/draw/1/flow/{flowId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "GetLatestFlow",
                    flowId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawDeleteFlow",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/draw/1/flow/{flowId}",
                defaults: new
                {
                    controller = "Draw",
                    action = "DeleteFlow",
                    flowId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "DrawSaveFlow",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/draw/1/flow",
                defaults: new
                {
                    controller = "Draw",
                    action = "SaveFlow"
                }
            );