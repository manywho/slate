# Play API

            // Play
            config.Routes.MapHttpRoute(
                name: "PlayUpdatePlayer",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "{tenantId}/play/{manywhoSystemParameterNameOfPlayer}",
                defaults: new
                {
                    controller = "Play",
                    action = "UpdatePlayer",
                    tenantId = RouteParameter.Optional,
                    manywhoSystemParameterNameOfPlayer = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "PlayGetPlayer",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "play/{manywhoSystemParameterNameOfPlayer}",
                defaults: new
                {
                    controller = "Play",
                    action = "GetPlayer",
                    manywhoSystemParameterNameOfPlayer = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "PlayGetPlayerWithTenantId",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "{tenantId}/play/{manywhoSystemParameterNameOfPlayer}",
                defaults: new
                {
                    controller = "Play",
                    action = "GetPlayer",
                    manywhoSystemParameterNameOfPlayer = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "PlayGetPlayers",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "{tenantId}/player",
                defaults: new
                {
                    controller = "Play",
                    action = "GetPlayers"
                }
            );

            config.Routes.MapHttpRoute(
                name: "PlayDeletePlayer",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "{tenantId}/play/{name}",
                defaults: new
                {
                    controller = "Play",
                    action = "DeletePlayer",
                    tenantId = RouteParameter.Optional,
                    name = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                            name: "DrawGetCustomStyles",
                            routeTemplate: "css/tenant/{tenantId}/customstyles",
                            defaults: new
                            {
                                controller = "Draw",
                                action = "GetCustomStyles",
                                id = RouteParameter.Optional
                            }
            );
