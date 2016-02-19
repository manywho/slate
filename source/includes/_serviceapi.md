# Service API


            // Service Invoker
            config.Routes.MapHttpRoute("ServiceRequestsList", "api/service/1/requests", new
            {
                controller = "ServiceRequests",
                action = "List"
            });

            config.Routes.MapHttpRoute("ServiceRequestsGet", "api/service/1/requests/{id}", new
            {
                controller = "ServiceRequests",
                action = "Get"
            });

            config.Routes.MapHttpRoute("ServiceRequestsRetrySingle", "api/service/1/requests/{id}/retry", new
            {
                controller = "ServiceRequests",
                action = "RetrySingle"
            });

            config.Routes.MapHttpRoute("ServiceRequestsListByFlow", "api/service/1/requests/flow/{flowId}", new
            {
                controller = "ServiceRequests",
                action = "ListByFlow"
            });

            config.Routes.MapHttpRoute("ServiceRequestsListByFlowVersion", "api/service/1/requests/flow/{flowId}/{flowVersionId}", new
            {
                controller = "ServiceRequests",
                action = "ListByFlowVersion"
            });

            config.Routes.MapHttpRoute("ServiceRequestsListByState", "api/service/1/requests/state/{stateId}", new
            {
                controller = "ServiceRequests",
                action = "ListByState"
            });

            // Object Data
            config.Routes.MapHttpRoute(
                name: "ObjectDataLoad",
                routeTemplate: "api/service/1/data",
                defaults: new
                {
                    controller = "ObjectData",
                    action = "Load"
                }
            );

            // File Data
            config.Routes.MapHttpRoute(
                name: "FileDataLoadFiles",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/service/1/file",
                defaults: new
                {
                    controller = "FileData",
                    action = "LoadFiles"
                }
            );

            config.Routes.MapHttpRoute(
                name: "FileDataDeleteFile",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/service/1/file/delete",
                defaults: new
                {
                    controller = "FileData",
                    action = "DeleteFile"
                }
            );

            config.Routes.MapHttpRoute(
                name: "FileDataUploadFile",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/service/1/file/content",
                defaults: new
                {
                    controller = "FileData",
                    action = "UploadFile"
                }
            );