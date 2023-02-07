## Creating AWS CloudWatch Logs using .NET Console Application: A Step-by-Step Guide

Welcome to this comprehensive guide on creating AWS CloudWatch Logs using a .NET Console Application. In this article, we will go through the process of setting up CloudWatch and logging events from a .NET Console Application. Whether you are new to AWS or a seasoned user, this guide will provide you with a clear understanding of how to monitor and manage your application logs in the AWS Cloud. Let’s get started!

## Table of Contents

 1. [Create IAM Client in AWS](#42c9)

 2. [Generate IAM Client Credentials](#c4d8)

 3. [Configure AWS CloudWatch](#48c4)

 4. [Create .Net Console Application](#5d3e)

 5. [Add appsettings.json file](#6b69)

 6. [Access values inside appsettings.json file](#562c)

 7. [Configure AWS Cloudwatch in Console App](#d5ba)

 8. [CloudWatch Log Stream](#cb46)

### 1. Create IAM Client in AWS
>  Identity and Access Management (IAM) is a web service for securely controlling access to Amazon Web Services services. With IAM, you can centrally manage users, security credentials such as access keys, and permissions that control which Amazon Web Services resources users and applications can access.

 1. Login to [amazon](https://console.aws.amazon.com) with credentials

 2. From home select your preferred region

![AWS Console Home Page](https://cdn-images-1.medium.com/max/3840/1*fURAyj0xGI4Am1YCpaEwZg.png)

![Region selection list](https://cdn-images-1.medium.com/max/3840/1*OQFzTXKNXVoFbESVPr3NQA.png)
>  An AWS region is **a cluster of data centers in a specific geographic area**, such as the Northeastern United States or Western Europe. It is a best practice to choose a region that is geographically close to users. This reduces latency because the data reaches the users more quickly.

3. Go to IAM Services page

![IAM Page](https://cdn-images-1.medium.com/max/3784/1*KJ7KCac9nXjs9Tv7TSZk1Q.png)

4. Select Users from the left Access management panel

5. Click Add Users

6. Enter username => Next

7. Select Attach Policies Directly in Permission Options

8. Select CloudWatchFullAccess from Permission Policies

![Set Permissions to IAM Client](https://cdn-images-1.medium.com/max/3840/1*jwJAORaCPKWaevyYgE5vGQ.png)

![IAM client Creation](https://cdn-images-1.medium.com/max/3686/1*ncWsv6j3zb9Oti-F7oIerg.png)



9. Next => Create User

![Created client](https://cdn-images-1.medium.com/max/3054/1*LA2KHSkFAjV-qxqWv2NSkw.png)

10. Now you can see the created IAM User

### 2. Generate IAM Client Credentials

 1. Click on the created IAM user

 2. Navigate to security credentials

![Generate keys for client](https://cdn-images-1.medium.com/max/2918/1*qfKFMnMQ5m_LTzxTRigadQ.png)

3. Scroll down to Access Keys

![Generate keys for client](https://cdn-images-1.medium.com/max/2252/1*qP8jB-HGhhX38lSlyn5zUg.png)

4. Create access key => select other => Next

![Configure access key permission](https://cdn-images-1.medium.com/max/2558/1*2OrmPLrfoh67toTRdiUwAw.png)

5. Create an access key

6. Copy both the access key and the Secret access key for later use

![Access key and secret key](https://cdn-images-1.medium.com/max/2832/1*rexm6vl0vyIJHeXUiWgDiA.png)

7. Done

### 3. Configure AWS CloudWatch
>  CloudWatch Logs enables you to centralize the logs from all of your systems, applications, and AWS services that you use, in a single, highly scalable service. You can then easily view them, search them for specific error codes or patterns, filter them based on specific fields, or archive them securely for future analysis.

 1. Navigate CloudWatch in AWS Services

 2. Goto Log groups in the left panel (Make sure you have selected the correct AWS region)

![AWS CloudWatch logGroups](https://cdn-images-1.medium.com/max/3648/1*2SXqENTHpF2kW0t3g3B9Cg.png)

3. Click on create Log group
>  A CloudWatch Log Group is a container for log streams, which are collections of log events that share the same source. For example, you could create a log group for logs generated by an application, and then create separate log streams for each instance of the application.

4. Enter a suitable name and set the expiry date

![Log group Creation](https://cdn-images-1.medium.com/max/2194/1*Ep7HXjmRrV387ZjPHqKbEg.png)

5. Create

![Successfully created logGroup](https://cdn-images-1.medium.com/max/3008/1*VOCqZHkcktglUSyBqkorOw.png)

6. Go to Log Group

7. Create a Log Stream
>  A CloudWatch Log Stream is a sequence of log events that share the same source. Within a log group, each log stream has a unique name and stores events independently. You can view and search the log events in a stream, set up alarms to be triggered by specific patterns in the log data, and export the log data to other services for further analysis.

![LogStream Creation](https://cdn-images-1.medium.com/max/2368/1*8j6C9blTYjXduvCfCmsmkQ.png)

Enter log Stream Name => create

### 4. Create .Net Console Application

 1. Open Visual Studio

 2. Create a new project => Select the console app

![Select Console Application of Visual Studio](https://cdn-images-1.medium.com/max/2028/1*UEeMbnLvahqLWX1czhCr3w.png)

3. Next => Enter Project name => Next => .Net 6.0 => Create

![Sample code in Console App](https://cdn-images-1.medium.com/max/2928/1*RYKAhTUh9E1gyj5xdiQOEA.png)

### 5. Add appsettings.json file
>  The “appsettings.json” file in .NET projects is used to store configuration settings for an application. It allows you to store key-value pairs that represent various configuration options such as database connection strings, API keys, and other application-specific settings.

 1. Right-click on testAwsConsoleApp => Add => New item

![Add appsettings.json file](https://cdn-images-1.medium.com/max/3668/1*_UL-I073x6a5Bb8a06xjRw.png)

2. Search json in the search box

![File type selection](https://cdn-images-1.medium.com/max/2356/1*2LR1Y3GRk7jq0GQxsHHWkg.png)

3. Select json file and set the name to appsessings.json => Add

4. Add this code to appsettings.json file

    {
      "Client_id": "<your client Id>",
      "Client_secret": "<Your client secret>",
      "LogGroupName": "<Log group name>",
      "LogStreamName": "<Log stream name>",
    }

![Code on appsettings.json file](https://cdn-images-1.medium.com/max/3684/1*6pLt6iv2_2tB2RYyls75yQ.png)

5. Click appsettings.json file on the solution explorer and set its Copy to Output Directory value to Copy always

![appsettings.json file configuration](https://cdn-images-1.medium.com/max/2000/1*8qS1nhZZXzEoPsSgE9nLCw.png)

### 6. Access values inside appsettings.json file

 1. Go to Program.cs file

 2. Remove all the sample code

 3. Paste this code

    using Microsoft.Extensions.Configuration;
    
    namespace testAwsConsoleApp
    {
        class Program
        {
            static void Main(string[] args)
            {
                IConfigurationBuilder configBuilder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
                IConfiguration configuration = configBuilder.Build();
                Console.WriteLine(configuration["Client_id"]);
            }
        }
    }

4. Install these Nuget packages from Nuget package manager

![Nuget package manager](https://cdn-images-1.medium.com/max/2928/1*cQtP2ql0aNgYsdtl16t9Qg.png)

5. Run the program  Ctrl + F5 or green triangle on the top

![](https://cdn-images-1.medium.com/max/2000/1*tYwIxMY1H6PzOERj2sP7ug.png)

6. Now we can access the appsettings.json values from our code

### 7. Configure AWS Cloudwatch in Console App

 1. Create a new c# class AWSCloudWatch.cs

![Add new c# class](https://cdn-images-1.medium.com/max/2000/1*i9ryZFTy9hXb8ziLIbxRWg.png)

2. Select the class and set the name to AWSCloudWatch.cs

3. Add

![AWSCloudWatch.cs file](https://cdn-images-1.medium.com/max/3560/1*TkjWlQOIUL4b5dYI3zGwXw.png)

5. Install this Nuget package

![AWSSDK Nuget package](https://cdn-images-1.medium.com/max/2000/1*fLqRfEY54-VzUjdF4ehh4g.png)

6. Paste this code in AWSCloudWatch.cs
>  In RegionEndpoint make sure you select the accurate region in which you create the log group and log stream

    using Amazon.CloudWatchLogs;
    using Amazon.CloudWatchLogs.Model;
    using Microsoft.Extensions.Configuration;
    
    namespace testAwsConsoleApp
    {
        public class AWSCloudWatch
        {
            private readonly IConfiguration _configuration;
            private static System.Timers.Timer aTimer;
    
            public AWSCloudWatch(IConfiguration configuration)
            {
                _configuration = configuration;
            }
    
            public void TimerStart()
            {
                Console.WriteLine("\nPress the Enter key to exit the application...\n");
                Console.WriteLine("The application started at {0:HH:mm:ss.fff}", DateTime.Now.ToString("yyyy-MM-dd HH:mm:ss"));
    
                aTimer = new System.Timers.Timer(4000); // method executes every 4 seconds
                aTimer.Elapsed += (s, e) => CloudWatchLog();
                aTimer.AutoReset = true;
                aTimer.Enabled = true;
                Console.ReadLine();
                aTimer.Stop();
                aTimer.Dispose();
                Console.WriteLine("Terminating the application...");
    
                while (Console.Read() != 'q') ;
    
            }
    
            public async void CloudWatchLog()
            {
                try
                {
                    var credentials = new Amazon.Runtime.BasicAWSCredentials(_configuration["Client_id"], _configuration["Client_secret"]);
    
                    var config = new AmazonCloudWatchLogsConfig
                    {
                        RegionEndpoint = Amazon.RegionEndpoint.APSoutheast1
                    };
    
                    var logClient = new AmazonCloudWatchLogsClient(credentials, config);
    
                    await logClient.PutLogEventsAsync(new PutLogEventsRequest()
                    {
                        LogGroupName = _configuration["LogGroupName"],
                        LogStreamName = _configuration["LogStreamName"],
                        LogEvents = new List<InputLogEvent>()
                        {
                            new InputLogEvent()
                            {
                                Message = "error message from console app",
                                Timestamp = DateTime.UtcNow
                            }
                        }
    
                    });
                    Console.WriteLine("Logging successfull");
                }
                catch (Exception e)
                {
                    Console.WriteLine(e.Message, "Error occured");
                }
    
            }
        }
    }

Here we created a timer for cloud watch log execution and set the log as error message from console app . The timer calls the CloudWatchLog function every 4 seconds.

And you can set up custom error messages as well as API call error messages as InputLogEvent message. So you can log the API error messages to AWS cloudwatch.

7. Complete Program.cs code

    using Microsoft.Extensions.Configuration;
    
    namespace testAwsConsoleApp
    {
        class Program
        {        
            static void Main(string[] args)
            {
                IConfigurationBuilder configBuilder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
                IConfiguration configuration = configBuilder.Build();
    
                var cloudwatchParam = new AWSCloudWatch(configuration);
    
                cloudwatchParam.TimerStart();
            }
    
        }
    }

8. Run the program

![Console Application](https://cdn-images-1.medium.com/max/2000/1*EpxK4qMsPbDBD2v0J3qylA.png)

### 8. CloudWatch Log Stream

 1. Navigate to your cloud watch log stream

![Inside log stream](https://cdn-images-1.medium.com/max/2980/1*d1Hebn3ohIvfL0tXef2rUw.png)

These are the all logs that we send from .Net console application

### Source Code

[Github](https://github.com/DSmabulage/CloudWatch_ConsoleApp)

### Thank you….
