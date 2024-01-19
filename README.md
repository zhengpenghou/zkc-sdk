# zkc-sdk

The zkc-sdk is a free and open-source toolkit for building zkWasm-based web application with modular rollup.

It consists of the following components:

- rollup interface: a minimal set of interfaces that defines zkWasm rollup application.
- jsenv: A host environment for Wasm application to use module services.
- prover adaptor: Connect to zkWasm proving network.
- contract proxy: Communicate with on-chain settlement rollup smart contract.
- ...

# How to use zkc-sdk from a web application

## Step1: Install zkc-sdk
```
npm install zkc-sdk
```
## Step2: Import ZKCWasmService from zkc-sdk
```
import { ZKCWasmService } from 'zkc-sdk';
```
## Step3: Load wasm binary image using ZKCWasmService
```
// Get the URL of the wasm file for initializing the WebAssembly instance.
const helloWorldURL = new URL('./wasmsrc/c/hello-world.wasm', import.meta.url);

// load wasm module instance
const { wasm } = await ZKCWasmService.loadWasm(helloWorldURL);
```
## Step4: Call wasm function from web application
```
// Call the Add function export from wasm, save the result
const addResult = wasm.add(26, 26);

// Set the result onto the body
document.body.textContent = `Hello World! addResult: ${addResult}`;
```

## Full example code [index.js](https://github.com/zkcrossteam/zkc-by-example/blob/master/examples/hello-world/index.js)
```
import { ZKCWasmService } from 'zkc-sdk';

// Get the URL of the wasm file for initializing the WebAssembly instance.
const helloWorldURL = new URL('./wasmsrc/c/hello-world.wasm', import.meta.url);

const runWasmAdd = async () => {
  // load wasm module instance
  const { wasm } = await ZKCWasmService.loadWasm(helloWorldURL);

  // Call the Add function export from wasm, save the result
  const addResult = wasm.add(26, 26);

  // Set the result onto the body
  document.body.textContent = `Hello World! addResult: ${addResult}`;
};

runWasmAdd();
```

# More information
Check [zkc-by-example](https://github.com/zkcrossteam/zkc-by-example) for more details regarding how to generating a zero knowledge proof, verifying the zkProof on-chain and use other services e.g zkc state service using the zkc-sdk.
