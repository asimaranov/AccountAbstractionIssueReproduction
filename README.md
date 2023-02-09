# An abstract account deployment issue after network regenesis

This project demonstrates an abstract account deployment issue. 
To reproduce 
Set up test .env file
Run `yarn hardhat deploy-zksync --script deploy-factory.ts` to deploy test factory
Add new factory address to the `deploy/deploy-account.ts` address
Run `yarn hardhat deploy-zksync --script deploy-account.ts`

The account contract based on node_modules/@matterlabs/zksync-contracts/l2/system-contracts/DefaultAccount.sol
The factory contract based on the factory from https://v2-docs.zksync.io/dev/tutorials/custom-aa-tutorial.html#account-abstraction

Expected behaviour: Account deployed
Actual error: 
```shell
<ref *1> Error: cannot estimate gas; transaction may fail or may require manual gas limit [ See: https://links.ethers.org/v5-errors-UNPREDICTABLE_GAS_LIMIT ] (error={"reason":"processing response error","code":"SERVER_ERROR","body":"{\"jsonrpc\":\"2.0\",\"error\":{\"code\":3,\"message\":\"Failed to submit transaction: cannot estimate transaction: out of gas.\",\"data\":{\"code\":104,\"message\":\"cannot estimate transaction: out of gas.\"}},\"id\":50}\n","error":{"code":3,"data":{"code":104,"message":"cannot estimate transaction: out of gas."}},"requestBody":"{\"method\":\"eth_estimateGas\",\"params\":[{\"gasPrice\":\"0x393b6ec0\",\"type\":\"0x0\",\"from\":\"0x2836ec28c32e232280f984d3980ba4e05d6bf68f\",\"to\":\"0xdcebe3f7d16f39d83c4db6fc95df9b5ca9f68c6e\",\"data\":\"0xd01a9cae0000000000000000000000000000000000000000000000000000000000000000\"}],\"id\":50,\"jsonrpc\":\"2.0\"}","requestMethod":"POST","url":"https://zksync2-testnet.zksync.dev"}, tx={"data":"0xd01a9cae0000000000000000000000000000000000000000000000000000000000000000","to":{},"from":"0x2836eC28C32E232280F984d3980BA4e05d6BF68f","type":0,"gasPrice":{},"nonce":{},"gasLimit":{},"chainId":{}}, code=UNPREDICTABLE_GAS_LIMIT, version=abstract-signer/5.7.0)
    at Logger.makeError (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/logger/src.ts/index.ts:269:28)
    at Logger.throwError (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/logger/src.ts/index.ts:281:20)
    at /Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/abstract-signer/src.ts/index.ts:301:31
    at processTicksAndRejections (node:internal/process/task_queues:96:5)
    at async Promise.all (index 6) {
  reason: 'cannot estimate gas; transaction may fail or may require manual gas limit',
  code: 'UNPREDICTABLE_GAS_LIMIT',
  error: Error: processing response error (body="{\"jsonrpc\":\"2.0\",\"error\":{\"code\":3,\"message\":\"Failed to submit transaction: cannot estimate transaction: out of gas.\",\"data\":{\"code\":104,\"message\":\"cannot estimate transaction: out of gas.\"}},\"id\":50}\n", error={"code":3,"data":{"code":104,"message":"cannot estimate transaction: out of gas."}}, requestBody="{\"method\":\"eth_estimateGas\",\"params\":[{\"gasPrice\":\"0x393b6ec0\",\"type\":\"0x0\",\"from\":\"0x2836ec28c32e232280f984d3980ba4e05d6bf68f\",\"to\":\"0xdcebe3f7d16f39d83c4db6fc95df9b5ca9f68c6e\",\"data\":\"0xd01a9cae0000000000000000000000000000000000000000000000000000000000000000\"}],\"id\":50,\"jsonrpc\":\"2.0\"}", requestMethod="POST", url="https://zksync2-testnet.zksync.dev", code=SERVER_ERROR, version=web/5.7.1)
      at Logger.makeError (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/logger/src.ts/index.ts:269:28)
      at Logger.throwError (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/logger/src.ts/index.ts:281:20)
      at /Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/src.ts/index.ts:341:28
      at step (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/lib/index.js:33:23)
      at Object.next (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/lib/index.js:14:53)
      at fulfilled (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/lib/index.js:5:58)
      at processTicksAndRejections (node:internal/process/task_queues:96:5) {
    reason: 'processing response error',
    code: 'SERVER_ERROR',
    body: '{"jsonrpc":"2.0","error":{"code":3,"message":"Failed to submit transaction: cannot estimate transaction: out of gas.","data":{"code":104,"message":"cannot estimate transaction: out of gas."}},"id":50}\n',
    error: Error: Failed to submit transaction: cannot estimate transaction: out of gas.
        at getResult (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/providers/src.ts/json-rpc-provider.ts:142:28)
        at processJsonFunc (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/src.ts/index.ts:383:22)
        at /Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/src.ts/index.ts:320:42
        at step (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/lib/index.js:33:23)
        at Object.next (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/lib/index.js:14:53)
        at fulfilled (/Users/andrey/projects/zkSyncAccountAbstractionIssueReproduction/node_modules/@ethersproject/web/lib/index.js:5:58)
        at processTicksAndRejections (node:internal/process/task_queues:96:5) {
      code: 3,
      data: [Object]
    },
    requestBody: '{"method":"eth_estimateGas","params":[{"gasPrice":"0x393b6ec0","type":"0x0","from":"0x2836ec28c32e232280f984d3980ba4e05d6bf68f","to":"0xdcebe3f7d16f39d83c4db6fc95df9b5ca9f68c6e","data":"0xd01a9cae0000000000000000000000000000000000000000000000000000000000000000"}],"id":50,"jsonrpc":"2.0"}',
    requestMethod: 'POST',
    url: 'https://zksync2-testnet.zksync.dev'
  },
  tx: {
    data: '0xd01a9cae0000000000000000000000000000000000000000000000000000000000000000',
    to: Promise { '0xDcEbE3F7D16F39D83c4dB6fc95DF9b5Ca9F68c6E' },
    from: '0x2836eC28C32E232280F984d3980BA4e05d6BF68f',
    type: 0,
    gasPrice: Promise { [BigNumber] },
    nonce: Promise { 66 },
    gasLimit: Promise { <rejected> [Circular *1] },
    chainId: Promise { 280 }
  }
}
```

Seems to revert on ```require(success, "Deployment failed");```

Tried: add ```isSystem: true``` to zksolc config
Still not worked