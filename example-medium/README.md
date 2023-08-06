# [Medium mountebank Example](https://medium.com/digio-australia/mock-it-with-mountebank-88762dadac1f)  

## Instructions  

1 - Install it:  
<code>npm install -g mountebank</code>  

2 - Create this folder structure and files:  
```
example-medium/
├── imposters/
│ ├── sampleImposter.ejs
├── stubs/
│ ├── sampleStub.json
├── imposters.ejs
└── package.json
```

3 - In the example-medium folder run:  
<code>npm init</code>  

4 - Change the package.json according to the tutorial  

5 - Run:  
<code>npm run mock</code>  

6 - Test it (you can use curl or Postman):  
<code>curl -i -X POST -H 'Content-Type: application/json' http://localhost:4545/test</code>  
