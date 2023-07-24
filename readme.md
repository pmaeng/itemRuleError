# Feed Error Action Rule
Based on marketplaceCode, feedType and errorDetails, The rule will return the error action. 

Once you have deployed feed-error-action rule on Kie-server, then it can be accessed 
through below Kie-server REST API. We can test this API using below payload

# URI: 
    http://<ip>/kie-server/services/rest/server/containers/instances/{MyContainer}
# Method: 
    POST
# Path Param: 
    You need to pass deployed container id in {MyContainer} placeholder
    Example: in our case deployed container id is feedErrorActionRule_1.0.2, so
    http://<IP>/kie-server/services/rest/server/containers/instances/feedErrorActionRule_1.0.2
# Headers: 
    Content-Type: application/json
    Authorization: Basic YWRtaW46YWRtaW4=

# Request Payload:       
    {
        "commands": [
            {
                "insert": {
                    "object": {
                        "ErrorAction": {
                            "errorDetails": "Data_Error",
                            "feedType": "MP_ITEM_MATCH",
                            "marketplaceCode": "walmart"
                        }
                    },
                    "disconnected": false,
                    "out-identifier": "Product",
                    "return-object": true,
                    "entry-point": "DEFAULT"
                }
            },
            {
                "fire-all-rules": {}
            }
        ],
        "lookup": null
    }

# Response Payload:
    {
        "type": "SUCCESS",
        "msg": "Container feed-error-action_1.0.4 successfully called.",
        "result": {
            "execution-results": {
                "results": [
                    {
                        "value": {
                            "com.integration.items.ErrorAction": {
                                "marketplaceCode": "walmart",
                                "feedType": "MP_ITEM_MATCH",
                                "errorDetails": "Data_Error",
                                "invokeAction": "CallCWSUpdateStatus"
                            }
                        },
                        "key": "Product"
                    }
                ],
                "facts": [
                    {
                        "value": {
                            "org.drools.core.common.DefaultFactHandle": {
                                "external-form": "0:1:1773345818:1773345818:1:DEFAULT:NON_TRAIT:com.integration.items.ErrorAction"
                            }
                        },
                        "key": "Product"
                    }
                ]
            }
        }
    }        




