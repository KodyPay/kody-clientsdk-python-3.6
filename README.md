# Kody Python gRPC client

## Description
The Kody gRPC Client is an SDK generated from protobuf protocols to facilitate communication with the Kody Payments Gateway. This library provides a simple and efficient way to integrate Kody payment functionalities into your applications.

## Installation
Add to your `requirements.txt` any package from the release list
`https://github.com/KodyPay/kody-clientsdk-python-3.6/releases/download/v<version>/kody_clientsdk_python-<version>.tar.gz`

## Sample usage
```python
import logging

import grpc
import kody_clientsdk_python.pay.v1.pay_pb2 as pay_model
import kody_clientsdk_python.pay.v1.pay_pb2_grpc as pay_grpc_client

host = "grpc.kodypay.com:443"
storeId = "<YOUR_STORE_ID>"
key = "<YOUR_KEY>"

def run():
    with grpc.secure_channel(target=host,
                             credentials=grpc.ssl_channel_credentials()) as channel:
        stub = pay_grpc_client.KodyPayTerminalServiceStub(channel)
        response = stub.Terminals(
            pay_model.TerminalsRequest(store_id=storeId),
            metadata=[("x-api-key", key)]
        )

    logging.info(f"Response received: {response.terminals}")


if __name__ == "__main__":
    logging.basicConfig(level=logging.DEBUG)
    run()
``` 