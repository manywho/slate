# Log API

            // Logging
            config.Routes.MapHttpRoute(
                name: "Log",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/log/{flowId}/{stateId}",
                defaults: new
                {
                    controller = "Log",
                    action = "GetLog",
                    flowId = RouteParameter.Optional,
                    stateId = RouteParameter.Optional
                }
            );
