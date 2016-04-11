---
layout: post-index
date: 2016-04-07
img: https://s3.amazonaws.com/images-mddalesio/Technologies/aws-lambda.jpg
alt: image-alt
tag: [AWS, Lambda, Groovy, Java]
category: [Cloud]
comments: true
---
For the past couple of weeks I have been experimenting with Amazon Web Services (AWS). In particular I have been evaluating the Lambda, API Gateway, and DynamoDB products. AWS Lambda is a serverless cloud computing product that enables developers to create scalable event-driven systems and application backends without maintaining servers and only paying for the compute time used. In this post I show an example of using a Java / Groovy lambda function.


Show below is the test JSON input that will be sent to the lambda function to be deserialized into a “People” object and processed.


The Hello class shown below is the sample  Java AWS lambda function used for testing. The function simply receives a “People” object as an input and returns a list of BSON documents as an output. The output is serialized as JSON by lambda.
{% highlight groovy %}
package testing
 
import com.amazonaws.services.lambda.runtime.Context
import org.bson.Document;
 
public class Hello {
        public List&lt;Document&gt; myHandler(People people, Context context) {
 
           def listOfPeople = []
            Document person1 = new Document().append(&quot;name&quot;, people.person1)
            listOfPeople.add(person1)
 
            Document person2 = new Document().append(&quot;name&quot;, people.person2)
            listOfPeople.add(person2)
 
            Document person3 = new Document().append(&quot;name&quot;, people.person3)
            listOfPeople.add(person3)
 
            return listOfPeople
        }
 
}
{% endhighlight %}