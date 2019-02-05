---
layout: post
title:  "使用AWS Lambda调用Google Analytics Report API"
date:   2018-04-29 11:11:18 +1200
categories: aws lambda
---

如果你需要使用AWS Lambda调用Google Analytics Report API并以API的形式expose的话，你还将需要集成AWS API Gateway。  

以下是在AWS Lambda中使用Node.js调用Google Analytics Report API的示例代码：  
// index.handler
```javascript
var { google } = require('googleapis');
// 这里显示的输入google的service_account key json数据是为了方便阅读和调试，在实际中最好将该部分数据放在AWS Lambda function中一个单独文件中，然后再以import的形式调用该数据
const key = {
    type: "service_account",
    project_id: "你的project_id",
    private_key_id: "你的private_key_id",
    private_key: "你的private_key",
    client_email: "你的client_email",
    client_id: "你的client_id",
    auth_uri: "https://accounts.google.com/o/oauth2/auth",
    token_uri: "https://accounts.google.com/o/oauth2/token",
    auth_provider_x509_cert_url: "https://www.googleapis.com/oauth2/v1/certs",
    client_x509_cert_url: "你的client_x509_cert_url"
};
const VIEW_ID = '你的VIEW_ID';
var jwtClient = new google.auth.JWT(key.client_email, null, key.private_key, ['https://www.googleapis.com/auth/analytics.readonly'], null);

exports.handler = (event, context, callback) => {
    jwtClient.authorize(function(err, result) {
        if (err) {
            console.log(err);
            return;
        } else {
            console.log("Successfully connected!");
            console.log(result);
        }

        var analyticsreporting = google.analyticsreporting('v4');

        analyticsreporting.reports.batchGet({
            headers: {'Content-Type': 'application/json'},
            auth: jwtClient,
            resource: {
                reportRequests: [
                    {
                        viewId: VIEW_ID,
                        dateRanges: [
                            {
                                startDate: '2018-01-01',
                                endDate: 'today'
                            }
                        ],
                        metrics: [
                            {
                                expression: 'ga:sessions'
                            }
                        ]
                    }
                ]
            }
        }, (error, response) => {
            console.log(response.data.reports[0].data.totals[0].values)
            if (error) {
                console.log('request fail: ');
                console.log(error);
            } else {
                console.log('request succeed: ');
                console.log(response.data.reports[0].data);
            }
            callback(null, response.data.reports[0].data);
        });
    });
};
```
因为该程序使用google-api-nodejs-client库，文件过大所以不能以在线编辑形式上传代码，此时你需要把相关node_modules等文件一起压缩成zip文件再上传到AWS Lambda function里。  

AWS API Gateway：  
如果你需要以API形式expose该Lambda function的话，你还需要创建AWS API Gateway，然后在该Gateway下创建resource和method（在这一过程中关联Lambda function），最后一切就绪后Deploy API，则你会获取该API的endpoint，就可以在你的其他业务中使用该endpoint了。  

更多细节会在以后添加...