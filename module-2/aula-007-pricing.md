
# AWS Lambda Pricing

Lambda's free tier allows you to use 1 million requests and
400,000GB seconds per month.

The main components of Lambda pricing are the number
of requests and Gigabit Seconds.

A Lambda request starts each time it executes the
function in response to an event trigger.

Gigabit seconds are the amount of time your function runs
multiplied by the amount of memory it uses.

The amount of memory you allocate to the function
determines the amount of CPU power allocated by
Lambda.

There are additional costs for including ephemeral storage
and provisioned concurrency to your Lambda functions.



### Pontos-chave

- Quanto mais Memoria, mais CPU será alocada
proporcional