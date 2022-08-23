Ethereum clients offer an application programming interface and a set of Remote Procedure Call (RPC) commands, which are encoded as JavaScript Object Notation (JSON). You will see this referred to as the _JSON-RPC API_. Essentially, the JSON-RPC API is an interface that allows us to write programs that use an Ethereum client as a _gateway_ to an Ethereum network and blockchain.

Usually, the RPC interface is offered as an HTTP service on port 8545. For security reasons it is restricted, by default, to only accept connections from localhost (the IP address of your own computer, which is 127.0.0.1).

To access the JSON-RPC API, you can use a specialized library (written in the programming language of your choice) that provides "stub" function calls corresponding to each available RPC command, or you can manually construct HTTP requests and send/receive JSON-encoded requests. You can even use a generic command-line HTTP client, like curl, to call the RPC interface. Let’s try that. First, ensure that you have Geth up and running, configured with --rpc to allow HTTP access to the RPC interface, then switch to a new terminal window (e.g., with Ctrl-Shift-N or Ctrl-Shift-T in an existing terminal window) as shown here:


````
curl -X POST -H "Content-Type: application/json" --data \
  '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}' \
  http://localhost:8545

{"jsonrpc":"2.0","id":1,
"result":"Geth/v1.9.11-unstable-0b284f6c-20200123/linux-amd64/go1.13.4"}

````


In this example, we use curl to make an HTTP connection to the address _http://localhost:8545_. We are already running geth, which offers the JSON-RPC API as an HTTP service on port 8545. We instruct curl to use the HTTP POST command and to identify the content as type application/json. Finally, we pass a JSON-encoded request as the data component of our HTTP request. Most of our command line is just setting up curl to make the HTTP connection correctly. The interesting part is the actual JSON-RPC command we issue:

````
{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}
````

The JSON-RPC request is formatted according to the [JSON-RPC 2.0 specification](https://www.jsonrpc.org/specification). Each request contains four elements:
- <b>jsonrpc</b>
<p>Version of the JSON-RPC protocol. This MUST be exactly "2.0".</p>
- <b>method</b>
<p>The name of the method to be invoked.</p>
- <b>params</b>
<p>A structured value that holds the parameter values to be used during the invocation of the method. This member MAY be omitted.</p>
- <b>id</b>
<p>An identifier established by the client that MUST contain a String, Number, or NULL value if included. The server MUST reply with the same value in the response object if included. This member is used to correlate the context between the two objects.</p>


> Tip
> 	The id parameter is used primarily when you are making multiple requests in a single JSON-RPC call, a practice called _batching_. Batching is used to avoid the overhead of a new HTTP and TCP connection for every request. In the Ethereum context, for example, we would use batching if we wanted to retrieve thousands of transactions over one HTTP connection. When batching, you set a different id for each request and then match it to the id in each response from the JSON-RPC server. The easiest way to implement this is to maintain a counter and increment the value for each request.

The response we receive is:

````
{"jsonrpc":"2.0","id":1,
"result":"Geth/v1.9.11-unstable-0b284f6c-20200123/linux-amd64/go1.13.4"}
````

This tells us that the JSON-RPC API is being served by Geth client version 1.9.11.

Let’s try something a bit more interesting. In the next example, we ask the JSON-RPC API for the current price of gas in wei:

````
$ **curl -X POST -H "Content-Type: application/json" --data \
  '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":4213}' \
  http://localhost:8545**

{"jsonrpc":"2.0","id":4213,"result":"0x430e23400"}
````

The response, 0x430e23400, tells us that the current gas price is 18 gwei (gigawei or billion wei). If, like us, you don’t think in hexadecimal, you can convert it to decimal on the command line with a little bash-fu:

````
$ **echo $((0x430e23400))**

18000000000
````

The full JSON-RPC API can be investigated on the [Ethereum wiki](https://github.com/ethereum/wiki/wiki/JSON-RPC).