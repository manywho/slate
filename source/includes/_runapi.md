# Run API

           config.Routes.MapHttpRoute(
                name: "RunAuthenticateWithOAuth2",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/oauth2",
                defaults: new
                {
                    controller = "Run",
                    action = "AuthenticateWithOAuth2"
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunGetNavigation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/navigation/{stateId}",
                defaults: new
                {
                    controller = "Run",
                    action = "GetNavigation",
                    stateId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunGetAuthenticationContext",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/authentication/{stateId}",
                defaults: new
                {
                    controller = "Run",
                    action = "GetAuthenticationContext",
                    stateId = RouteParameter.Optional,
                    serviceElementId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunAuthenticate",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/authentication/{stateId}",
                defaults: new
                {
                    controller = "Run",
                    action = "Authenticate",
                    stateId = RouteParameter.Optional,
                    serviceElementId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunGetFlowGraph",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/graph/flow/{stateId}",
                defaults: new
                {
                    controller = "Run",
                    action = "GetFlowGraph",
                    stateId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunLoadFlowByName",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/flow/name/{name}",
                defaults: new
                {
                    controller = "Run",
                    action = "LoadFlowByName",
                    name = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunLoadAllFlows",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/flow",
                defaults: new
                {
                    controller = "Run",
                    action = "LoadAllFlows",
                    filter = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunLoadFlowById",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/flow/{id}",
                defaults: new
                {
                    controller = "Run",
                    action = "LoadFlowById",
                    id = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunResponse",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/response",
                defaults: new
                {
                    controller = "Run",
                    action = "Response"
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunEvent",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/event",
                defaults: new
                {
                    controller = "Run",
                    action = "Event"
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunLoadAssignedUserPermissions",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/state/{stateId}/share",
                defaults: new
                {
                    controller = "Run",
                    action = "LoadAssignedUserPermissions",
                    stateId = RouteParameter.Optional,
                    filter = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunAddAssignedUserPermission",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/state/{stateId}/share",
                defaults: new
                {
                    controller = "Run",
                    action = "AddAssignedUserPermission",
                    stateId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunRemoveAssignedUserPermission",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/run/1/state/{stateId}/share/{userId}",
                defaults: new
                {
                    controller = "Run",
                    action = "RemoveAssignedUserPermission",
                    stateId = RouteParameter.Optional,
                    userId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunAddListener",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/state/{stateId}/listener",
                defaults: new
                {
                    controller = "Run",
                    action = "AddListener",
                    stateId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunRemoveListener",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/run/1/state/{stateId}/listener/{listenerId}",
                defaults: new
                {
                    controller = "Run",
                    action = "RemoveListener",
                    stateId = RouteParameter.Optional,
                    listenerId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunInitialize",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1",
                defaults: new
                {
                    controller = "Run",
                    action = "Initialize"
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunStateChangeHappened",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/state/{stateId}/ping/{stateToken}",
                defaults: new
                {
                    controller = "Run",
                    action = "StateChangeHappened",
                    stateId = RouteParameter.Optional,
                    stateToken = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunGetOut",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/state/out/{stateId}/{selectedOutcomeId}",
                defaults: new
                {
                    controller = "Run",
                    action = "GetOut",
                    stateId = RouteParameter.Optional,
                    selectedOutcomeId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunExecute",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/state/{stateId}",
                defaults: new
                {
                    controller = "Run",
                    action = "Execute",
                    stateId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunDelete",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/run/1/state/{stateId}",
                defaults: new
                {
                    controller = "Run",
                    action = "Delete",
                    stateId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunSetValues",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/state/{stateId}/values",
                defaults: new
                {
                    controller = "Run",
                    action = "SetValues",
                    stateId = RouteParameter.Optional,
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunGetValues",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/state/{stateId}/values",
                defaults: new
                {
                    controller = "Run",
                    action = "GetValues",
                    stateId = RouteParameter.Optional,
                }
            );
                        
            config.Routes.MapHttpRoute("RunGetValueByName", "api/run/1/state/{stateId}/values/name/{name}", new
            {
                controller = "Run",
                action = "GetValueByName"
            });

            config.Routes.MapHttpRoute("RunGetValueById", "api/run/1/state/{stateId}/values/{id}", new
            {
                controller = "Run",
                action = "GetValueById"
            });

            config.Routes.MapHttpRoute(
                name: "RunJoin",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/state/{stateId}",
                defaults: new
                {
                    controller = "Run",
                    action = "Join",
                    stateId = RouteParameter.Optional,
                    mode = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunImportState",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/run/1/state/package",
                defaults: new
                {
                    controller = "Run",
                    action = "ImportState"
                }
            );

            config.Routes.MapHttpRoute(
                name: "RunExportState",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/run/1/state/package/{stateId}",
                defaults: new
                {
                    controller = "Run",
                    action = "ExportState",
                    stateId = RouteParameter.Optional
                }
            );