# Social API


            // Social
            config.Routes.MapHttpRoute(
                name: "SocialCreateStream",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/social/1/{serviceElementId}",
                defaults: new
                {
                    controller = "Social",
                    action = "CreateStream",
                    serviceElementId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialGetCurrentUserInfo",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/social/1/stream/{streamId}/user/me",
                defaults: new
                {
                    controller = "Social",
                    action = "GetCurrentUserInfo",
                    streamId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialGetUserInfo",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/social/1/stream/{streamId}/user",
                defaults: new
                {
                    controller = "Social",
                    streamId = RouteParameter.Optional,
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialGetStreamFollowers",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/social/1/stream/{streamId}/follower",
                defaults: new
                {
                    controller = "Social",
                    action = "GetStreamFollowers",
                    streamId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialShareMessage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/social/1/stream/{streamId}/share",
                defaults: new
                {
                    controller = "Social",
                    action = "ShareMessage",
                    streamId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialPostNewMessage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/social/1/stream/{streamId}/message",
                defaults: new
                {
                    controller = "Social",
                    action = "PostNewMessage",
                    streamId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialLikeMessage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/social/1/stream/{streamId}/message/{messageId}",
                defaults: new
                {
                    controller = "Social",
                    action = "LikeMessage",
                    streamId = RouteParameter.Optional,
                    messageId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialDeleteMessage",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/social/1/stream/{streamId}/message/{messageId}",
                defaults: new
                {
                    controller = "Social",
                    action = "DeleteMessage",
                    streamId = RouteParameter.Optional,
                    messageId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialUploadFile",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/social/1/stream/{streamId}/file",
                defaults: new
                {
                    controller = "Social",
                    action = "UploadFile",
                    streamId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialDeleteUploadedFile",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Delete) },
                routeTemplate: "api/social/1/stream/{streamId}/file/{fileId}",
                defaults: new
                {
                    controller = "Social",
                    action = "DeleteUploadedFile",
                    streamId = RouteParameter.Optional,
                    fileId = RouteParameter.Optional
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialFollowStream",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Post) },
                routeTemplate: "api/social/1/stream/{streamId}",
                defaults: new
                {
                    controller = "Social",
                    action = "FollowStream",
                    streamId = RouteParameter.Optional,
                }
            );

            config.Routes.MapHttpRoute(
                name: "SocialGetStreamMessages",
                constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
                routeTemplate: "api/social/1/stream/{streamId}",
                defaults: new
                {
                    controller = "Social",
                    action = "GetStreamMessages",
                    streamId = RouteParameter.Optional
                }
            );