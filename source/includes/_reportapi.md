 # Report API


            // Report
            config.Routes.MapHttpRoute(
                name: "ReportStates",
                routeTemplate: "api/report/1/states",
                defaults: new
                {
                    controller = "Report",
                    action = "States"
                }
            );