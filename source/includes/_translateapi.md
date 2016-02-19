# Translate API




            // Translate
            config.Routes.MapHttpRoute(
                name: "TranslateGetFlows",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/translate/1/flow",
                defaults: new
                {
                    controller = "Translate",
                    action = "GetFlows",
                    filter = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateGetFlowTranslationImage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/translate/1/flow/{flowId}",
                defaults: new
                {
                    controller = "Translate",
                    action = "GetFlowTranslationImage",
                    flowId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateLoadContentValueCultures",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/translate/1/culture",
                defaults: new
                {
                    controller = "Translate",
                    action = "LoadContentValueCultures",
                    filter = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateLoadContentValueCulture",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/translate/1/culture/{cultureId}",
                defaults: new
                {
                    controller = "Translate",
                    action = "LoadContentValueCulture",
                    cultureId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateDeleteContentValueCulture",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/translate/1/culture/{cultureId}",
                defaults: new
                {
                    controller = "Translate",
                    action = "DeleteContentValueCulture",
                    cultureId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateSaveContentValueCulture",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/translate/1/culture",
                defaults: new
                {
                    controller = "Translate",
                    action = "SaveContentValueCulture"
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateSaveValueElementTranslation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/translate/1/element/value",
                defaults: new
                {
                    controller = "Translate",
                    action = "SaveValueElementTranslation"
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateLoadValueElementTranslation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/translate/1/element/value/{valueElementId}",
                defaults: new
                {
                    controller = "Translate",
                    action = "LoadValueElementTranslation",
                    valueElementId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateSavePageElementTranslation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/translate/1/element/page",
                defaults: new
                {
                    controller = "Translate",
                    action = "SavePageElementTranslation"
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateLoadPageElementTranslation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/translate/1/element/page/{pageElementId}",
                defaults: new
                {
                    controller = "Translate",
                    action = "LoadPageElementTranslation",
                    pageElementId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateSaveMapElementTranslation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/translate/1/flow/{flowId}/{editingToken}/element/map",
                defaults: new
                {
                    controller = "Translate",
                    action = "SaveMapElementTranslation",
                    flowId = RouteParameter.Optional,
                    editingToken = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateLoadMapElementTranslation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/translate/1/flow/{flowId}/{editingToken}/element/map/{id}",
                defaults: new
                {
                    controller = "Translate",
                    action = "LoadMapElementTranslation",
                    id = RouteParameter.Optional,
                    flowId = RouteParameter.Optional,
                    editingToken = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateSaveNavigationElementTranslation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/translate/1/flow/{flowId}/{editingToken}/element/navigation",
                defaults: new
                {
                    controller = "Translate",
                    action = "SaveNavigationElementTranslation",
                    flowId = RouteParameter.Optional,
                    editingToken = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "TranslateLoadNavigationElementTranslation",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/translate/1/flow/{flowId}/{editingToken}/element/navigation/{id}",
                defaults: new
                {
                    controller = "Translate",
                    action = "LoadNavigationElementTranslation",
                    id = RouteParameter.Optional,
                    flowId = RouteParameter.Optional,
                    editingToken = RouteParameter.Optional
                }
            );
            

