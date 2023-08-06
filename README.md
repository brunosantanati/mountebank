# [mountebank](http://www.mbtest.org/)  

## Getting started (including installation)

I just followed the instructions [here](http://www.mbtest.org/docs/gettingStarted) (just the HTTP example, not the TCP).  

1 - I installed it using the command:  
<code>npm install -g mountebank</code>  
In my case I needed to use sudo in front of the command.  

2 - I ran the mountebank using:  
<code>mb</code>  

3 - After that you can access the mountebank in the browser in this address below if you want to:  
http://localhost:2525/

4 - I created an HTTP imposter using curl:  
```
curl -i -X POST -H 'Content-Type: application/json' http://localhost:2525/imposters --data '{
  "port": 4545,
  "protocol": "http",
  "stubs": [{
    "responses": [
      { "is": { "statusCode": 400 }}
    ],
    "predicates": [{
      "and": [
        {
          "equals": {
            "path": "/test",
            "method": "POST",
            "headers": { "Content-Type": "application/json" }
          }
        },
        {
          "not": {
            "contains": { "body": "requiredField" },
            "caseSensitive": true
          }
        }
      ]
    }]
  }]
}'
```

5 - I tested the imposter using a request that matched the predicate in order to get a 400 response:  
<code>curl -i -X POST -H 'Content-Type: application/json' http://localhost:4545/test --data '{"optionalField": true}'</code>  

6 - I also tested the imposter using requests that didn't match the predicate and got the default response (200):  
<code>curl -i -X POST http://localhost:4545/test --data '{"optionalField": true}'</code>  
<code>curl -i -X POST -H 'Content-Type: application/json' http://localhost:4545/test --data '{"optionalField": true, "requiredField": true}'</code>  

7 - Additionally we may want to DELETE the imposter using:  
<code>curl -X DELETE http://localhost:2525/imposters/4545</code>  
