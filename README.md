# Knative-Demo

Prereqs: 
1. Knative serving operator installed (https://docs.openshift.com/container-platform/4.3/serverless/installing_serverless/installing-knative-serving.html)
2. Knative Eventing operator installed (https://docs.openshift.com/container-platform/4.3/serverless/installing_serverless/installing-knative-eventing.html#installing-knative-eventing)

Create a new project Knative Demo
```
oc new-project knative-demo
```

##Knative Serving Demo

We use python flask to create a sample application. This sample application prints "Hello world"

To deploy this service,
```
oc apply -f knative-serving/service.yaml
```

To find the URL for your service, use
```
oc get ksvc helloworld-python  --output=custom-columns=NAME:.metadata.name,URL:.status.url
```
Add this url to etc/hosts file 

Now you can make a request to your app and see the result. Replace the URL below with the URL returned in the previous command.
```
curl <url>
```


##Knative Eventing Demo

We use a Cronjob Event source to send events at regular intervals. The event data is sent to a configured sink. 

To deploy a event-source,
```
oc apply -f knative-eventing/event-source.yaml
```
To check the output, 
```
oc get cronjobsources.sources.eventing.knative.dev
NAME                           READY   AGE
event-greeter-cronjob-source   True    12m
```
Now we deploy a service which will display the events from the event source. 

```
oc apply -f event-display.yaml
```

You can watch the logs from the Openshift console. You will see the events displayed like this.

```
{
  "message" : "Thanks for doing Knative Tutorial",
  "host" : "Event  greeter => '9861675f8845' : 1",
  "time" : "17:17:02" 
}
```

Exercise: 
1. Now that we have setup Cronjob event source, try to setup a kafka source which sends data to event display using KafkaSource. (https://knative.dev/docs/eventing/samples/kafka/source/index.html)
2. After trying KafkaSource, you can try deploying http kafka bridge and connecting it to KafkaSource and then seeing the messages in event display pod. 





