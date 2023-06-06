# 常见报错提醒

代码端的报错提醒名称，更好的可以定位找到问题原因

| 错误原因                                          | 页面报错码 | PagePlug报错代码 | 标题显示                                                |
| --------------------------------------------- | ----- | ------------ | --------------------------------------------------- |
| INVALID\_PARAMETER                            | 400   | 4000         | Invalid parameter                                   |
| PLUGIN\_NOT\_INSTALLED                        | 400   | 4001         | Plugin not installed                                |
| PLUGIN\_ID\_NOT\_GIVEN                        | 400   | 4002         | Missing plugin id                                   |
| DATASOURCE\_NOT\_GIVEN                        | 400   | 4003         | Missing datasource                                  |
| PAGE\_ID\_NOT\_GIVEN                          | 400   | 4004         | Missing page id                                     |
| DUPLICATE\_KEY\_USER\_ERROR                   | 400   | 4005         | Name already used                                   |
| PAGE\_DOESNT\_BELONG\_TO\_USER\_WORKSPACE     | 400   | 4006         | Page doesn''t belong to this workspace              |
| UNSUPPORTED\_OPERATION                        | 400   | 4007         | Unsupported operation                               |
| DEPRECATED\_API                               | 400   | 4008         | Deprecated API                                      |
| USER\_DOESNT\_BELONG\_ANY\_WORKSPACE          | 400   | 4009         | User doesn''t belong to any workspace               |
| USER\_DOESNT\_BELONG\_TO\_WORKSPACE           | 400   | 4010         | User doesn''t belong to this workspace              |
| NO\_CONFIGURATION\_FOUND\_IN\_DATASOURCE      | 400   | 4011         | Datasource configuration is invalid                 |
| INVALID\_ACTION\_COLLECTION                   | 400   | 4038         | Collection configuration is invalid                 |
| INVALID\_ACTION                               | 400   | 4012         | Action configuration is invalid                     |
| INVALID\_DATASOURCE                           | 400   | 4013         | Datasource configuration is invalid                 |
| INVALID\_DATASOURCE\_CONFIGURATION            | 400   | 4015         | Datasource configuration is invalid                 |
| INVALID\_ACTION\_NAME                         | 400   | 4014         | Invalid action name                                 |
| NO\_CONFIGURATION\_FOUND\_IN\_ACTION          | 400   | 4016         | No configurations found in this action              |
| NAME\_CLASH\_NOT\_ALLOWED\_IN\_REFACTOR       | 400   | 4017         | Name already taken                                  |
| PAGE\_DOESNT\_BELONG\_TO\_APPLICATION         | 400   | 4018         | Page doesn''t belong to this application            |
| INVALID\_DYNAMIC\_BINDING\_REFERENCE          | 400   | 4022         | Invalid dynamic binding reference                   |
| USER\_ALREADY\_EXISTS\_IN\_WORKSPACE          | 400   | 4021         | User already exists in this workspace               |
| UNAUTHORIZED\_DOMAIN                          | 401   | 4019         | Invalid or unauthorized email domain                |
| USER\_NOT\_SIGNED\_IN                         | 401   | 4020         | User not signed in                                  |
| INVALID\_PASSWORD\_RESET                      | 400   | 4020         | Invalid password reset request                      |
| INVALID\_PASSWORD\_LENGTH                     | 400   | 4037         | Invalid password length                             |
| JSON\_PROCESSING\_ERROR                       | 400   | 4022         | Json processing error                               |
| INVALID\_CREDENTIALS                          | 200   | 4023         | Invalid credentials                                 |
| UNAUTHORIZED\_ACCESS                          | 403   | 4025         | Unauthorized access                                 |
| DUPLICATE\_KEY                                | 409   | 4024         | Duplicate key                                       |
| USER\_ALREADY\_EXISTS\_SIGNUP                 | 409   | 4025         | Account already exists with this email              |
| ACTION\_IS\_NOT\_AUTHORIZED                   | 403   | 4026         | Permission denied                                   |
| NO\_RESOURCE\_FOUND                           | 404   | 4027         | No resource found                                   |
| USER\_NOT\_FOUND                              | 404   | 4027         | No user found                                       |
| ACL\_NO\_RESOURCE\_FOUND                      | 404   | 4028         | No resource found or permission denied              |
| GENERIC\_BAD\_REQUEST                         | 400   | 4028         | Invalid request                                     |
| VALIDATION\_FAILURE                           | 400   | 4028         | Validation failed                                   |
| INVALID\_CURL\_COMMAND                        | 400   | 4029         | Invalid cURL command                                |
| INVALID\_LOGIN\_METHOD                        | 401   | 4030         | Invalid login method                                |
| INVALID\_GIT\_CONFIGURATION                   | 400   | 4031         | Invalid Git configuration                           |
| INVALID\_GIT\_SSH\_CONFIGURATION              | 400   | 4032         | SSH key not configured                              |
| INVALID\_GIT\_REPO                            | 400   | 4033         | Invalid Git repository                              |
| DEFAULT\_RESOURCES\_UNAVAILABLE               | 400   | 4034         | Default resources not found                         |
| GIT\_MERGE\_FAILED\_REMOTE\_CHANGES           | 406   | 4036         | Git merge failed for remote changes                 |
| GIT\_MERGE\_FAILED\_LOCAL\_CHANGES            | 406   | 4037         | Git merge failed for local changes                  |
| REMOVE\_LAST\_WORKSPACE\_ADMIN\_ERROR         | 400   | 4038         | Last admin cannot be removed                        |
| INVALID\_CRUD\_PAGE\_REQUEST                  | 400   | 4039         | Invalid page generation request                     |
| UNSUPPORTED\_OPERATION\_FOR\_REMOTE\_BRANCH   | 400   | 4040         | Unsupported Operation                               |
| ROLES\_FROM\_SAME\_WORKSPACE                  | 400   | 4041         | Roles already exist                                 |
| INTERNAL\_SERVER\_ERROR                       | 500   | 5000         | Internal server error                               |
| REPOSITORY\_SAVE\_FAILED                      | 500   | 5001         | Failed to save                                      |
| PLUGIN\_INSTALLATION\_FAILED\_DOWNLOAD\_ERROR | 500   | 5002         | Plugin installation failed                          |
| PLUGIN\_RUN\_FAILED                           | 500   | 5003         | Plugin execution failed                             |
| PLUGIN\_EXECUTION\_TIMEOUT                    | 504   | 5040         | Timeout in plugin execution                         |
| PLUGIN\_LOAD\_FORM\_JSON\_FAIL                | 500   | 5004         | Unable to load datasource form configuration        |
| PLUGIN\_LOAD\_TEMPLATES\_FAIL                 | 500   | 5005         | Unable to load datasource templates                 |
| IO\_ERROR                                     | 503   | 5003         | I/O error                                           |
| MARKETPLACE\_TIMEOUT                          | 504   | 5041         | Timeout in marketplace                              |
| DATASOURCE\_HAS\_ACTIONS                      | 409   | 4030         | Datasource cannot be deleted                        |
| WORKSPACE\_ID\_NOT\_GIVEN                     | 400   | 4031         | Missing workspace id                                |
| INVALID\_CURL\_METHOD                         | 400   | 4032         | Invalid method in cURL command                      |
| OAUTH\_NOT\_AVAILABLE                         | 500   | 5006         | Unsupported login method                            |
| MARKETPLACE\_NOT\_CONFIGURED                  | 500   | 5007         | Marketplace not configured                          |
| PAYLOAD\_TOO\_LARGE                           | 413   | 4028         | Payload exceeds max allowed size                    |
| SIGNUP\_DISABLED                              | 403   | 4033         | Signup disabled                                     |
| FAIL\_UPDATE\_USER\_IN\_SESSION               | 500   | 5008         | Unable to update user in session                    |
| APPLICATION\_FORKING\_NOT\_ALLOWED            | 403   | 4034         | Forking application not permitted                   |
| GOOGLE\_RECAPTCHA\_TIMEOUT                    | 504   | 5042         | Timeout in Google recaptcha verification            |
| GOOGLE\_RECAPTCHA\_FAILED                     | 401   | 4035         | Google recaptcha verification failed                |
| UNKNOWN\_ACTION\_RESULT\_DATA\_TYPE           | 500   | 5009         | Unexpected data type                                |
| INVALID\_CURL\_HEADER                         | 400   | 4036         | Invalid header in cURL command                      |
| AUTHENTICATION\_FAILURE                       | 500   | 5010         | Authentication failed                               |
| INSTANCE\_REGISTRATION\_FAILURE               | 500   | 5011         | Registration failed for this instance               |
| TOO\_MANY\_REQUESTS                           | 429   | 4039         | Too many requests                                   |
| INVALID\_JS\_ACTION                           | 400   | 4040         | Invalid action in JS object                         |
| CYCLICAL\_DEPENDENCY\_ERROR                   | 400   | 4041         | Cyclical Dependency in Page Load Actions            |
| CLOUD\_SERVICES\_ERROR                        | 500   | 5012         | Error in cloud services                             |
| GIT\_APPLICATION\_LIMIT\_ERROR                | 402   | 4043         | Maximum number of Git repo connection limit reached |
| GIT\_ACTION\_FAILED                           | 400   | 4044         | Git failed                                          |
| GIT\_FILE\_SYSTEM\_ERROR                      | 503   | 5013         | Git file system error                               |
| GIT\_EXECUTION\_TIMEOUT                       | 504   | 5014         | Timeout in Git command execution                    |
| INCOMPATIBLE\_IMPORTED\_JSON                  | 400   | 4045         | Incompatible Json file                              |
| GIT\_MERGE\_CONFLICTS                         | 400   | 4046         | Merge conflicts found                               |
| GIT\_PULL\_CONFLICTS                          | 400   | 4047         | Merge conflicts found during the pull operation     |
| SSH\_KEY\_GENERATION\_ERROR                   | 500   | 5015         | Failed to generate SSH keys                         |
| GIT\_GENERIC\_ERROR                           | 504   | 5016         | Git command execution error                         |
| GIT\_UPSTREAM\_CHANGES                        | 400   | 4048         | Git push failed for pending upstream changes        |
| GENERIC\_JSON\_IMPORT\_ERROR                  | 400   | 4049         | Unable to import application in workspace           |
| FILE\_PART\_DATA\_BUFFER\_ERROR               | 500   | 5017         | Failed to upload file                               |
| MIGRATION\_ERROR                              | 500   | 5018         | Action already migrated                             |
| INVALID\_GIT\_SSH\_URL                        | 400   | 4050         | Invalid SSH URL                                     |
| REPOSITORY\_NOT\_FOUND                        | 404   | 4051         | Repository not found                                |
| UNKNOWN\_PLUGIN\_REFERENCE                    | 400   | 4052         | Unknown plugin                                      |
| ENV\_FILE\_NOT\_FOUND                         | 500   | 5019         | Environment file not found                          |
| PUBLIC\_APP\_NO\_PERMISSION\_GROUP            | 500   | 5020         | Required permission missing for public access       |
| RTS\_SERVER\_ERROR                            | 500   | 5021         | RTS server error                                    |

