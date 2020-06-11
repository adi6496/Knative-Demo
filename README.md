# Knative-Demo
kubectl apply --filename https://github.com/knative/eventing-contrib/releases/download/v0.15.0/kafka-source.yaml
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

