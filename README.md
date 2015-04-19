# SentimentMap_WebServer

This is a team project finished by MINGFEI GE & YUAN FENG @ Columbia University in the course of Cloud Computing & Big Data
(@2015.4)

<h4>Note:</h4>

1. The website can only be accessed before May 2015 because of the pricing issue for AWS service. After that, you can only access our code. The App server code can be accessed at: https://github.com/GoMADAO/SentimentMap.git

2. The frontend JSP code is under WEB_CONTENT, which named "fake_mainpage.jsp", because we cannot put the DB keys in public. But all the other parts remained functional.

3. As mentioned in (1), the subscribed EC2 endpoint would be shut down afterwhile, so the endpoint defined in SNSChannel would be useless. And the SNSChannel in this server is only for testing. The real sending process happens in App server.

<h4>How this works:</h4>

This web server mainly focusing on SNS sevlet, i.e. the server subscribed to a SNS topic as an endpoint so as to get real-time publishment fron the topic, and push those content to the client ends.

The servlet based on the message type it received from the SNS topic to extract the real messages, which are of the type "Notification". And it stacks those messages to be sent. At the client end, we use AJAX to poll the message every second, and clan that stack at the servlet. The message is in JSON format, which includes location information and analyzed sentiment information for each twit.

At the client end, each time the page is loaded, the data already in DB will be fetched out and painted on Google Heatmap. And based on the polling mechanism, new points would be added to the map. And sentiment data would be processed and visualized use Chart.js. There are three forms of the data visualization--the radar, the pie, and the line chart, where the former two show the ratio of each range of sentiment(extremely negative, negative, netral, positive, extremely positive); while the last one dynamically shows the trend of the overall sentiment which is the current average of the sentiments scores received.
