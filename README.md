# Load and Smoke Testing for backend services

## Stack

- NodeJS  
- [Artillery](https://www.artillery.io/)


## Artillery

### Exemplo via linha de comando

- Quick command example: `artillery quick --count 20 --num 10 http://localhost:4000/api/v1/users`

Where:
- `--count 20`: total number of virtual users  
- `--num 10`: number of requests per user


### Scripts

```
config:
  target: "http://localhost:4000/api/v1"
  phases:
    - duration: 10
      arrivalRate: 2
      name: "Warm up - Retrieve data"

scenarios:
  - flow:
    - get:
        url: "/"
    - get:
        url: "/users"
```

Where: 
- `config` consists of the basic test settings such as the application URL  
- `config > phases` consists of the settings of the virtual users  
- `config > phases > duration` consists of the duration of the test, 30 seconds  
- `config > phases > arrivalRate` consists of the number of virtual users sent to the endpoints per second, 10 users per second  

- `scenarios` consists of the various operations that virtual users must perform  
- `scenarios > flow` where the operations that virtual users must perform are specified and controlled  

To run the test script, just run the command: `artillery run script.yml`

## References

- [Artillery](https://www.artillery.io/)  
- [A Guide to Load Testing Node.js APIs with Artillery](https://blog.appsignal.com/2021/11/10/a-guide-to-load-testing-nodejs-apis-with-artillery.html)  
- [Artillery Examples](https://github.com/artilleryio/artillery-examples)