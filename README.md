# EpicChain SDK Express Test

## Overview

**EpicChain SDK Express Test** provides a streamlined Express server environment specifically designed for testing and developing with the EpicChain JavaScript SDK (`epichain-sdk.js`). This repository addresses common challenges encountered with traditional servers, such as issues with serving `.wasm` metadata, by offering a more robust solution tailored to handle these needs effectively.

## Why Use This?

Traditional servers like `python2 -m SimpleHTTPServer` often struggle with serving `.wasm` files and their associated metadata correctly. This limitation can hinder development and testing processes, especially when working with modern web technologies that require accurate file serving and metadata handling.

**EpicChain SDK Express Test** overcomes these challenges by using Express version `4.17`, which provides improved support for serving `.wasm` files and metadata. This ensures a smoother development experience and more reliable testing outcomes.

## Features

- **Express Server**: A simple yet powerful Express server setup to facilitate testing and development with the EpicChain SDK.
- **Improved `.wasm` Handling**: Designed to address issues with serving WebAssembly modules and metadata, which are not adequately handled by some traditional servers.
- **Modular JavaScript Support**: Integration of necessary libraries and scripts for seamless interaction with the EpicChain SDK.

## Dependencies

To ensure proper functionality, the server relies on a few key modules:

- **Bower**: A package manager for managing front-end libraries.
- **Crypto-JS**: A library for cryptographic functions.

### Installation

1. **Install Bower Globally**:
   ```bash
   sudo npm install -g bower
   ```

2. **Install Dependencies**:
   Navigate to the `public` directory and install the required libraries using Bower:
   ```bash
   cd public && bower install crypto-js
   ```

## Working Example

As of now, ES6 modularization is not fully supported, so dependencies must be loaded manually. Here’s how you can include them in your HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>EpicChain SDK Express Test</title>
</head>
<body>
    <script src="https://unpkg.com/csbiginteger/dist/csbiginteger"></script>
    <script src="./bower_components/crypto-js/crypto-js.js"></script>
    <script src="./neopt-lib-cpp-web/neopt-lib-cpp-web.js"></script>
    <script>
        function testConversionToVerification() {
            var vx = csbiginteger.csBigInteger("92417421609284060097852441734141491128266387380656748836951019715045385777354", 10);
            var vy = csbiginteger.csBigInteger("81306213973968698003399946097148256829885864908442466985789085263601870844340", 10);
            var ecpoint = {
                "X": vx.toHexString(),
                "Y": vy.toHexString(),
                "curve": "secp256r1"
            };
            var strJson = JSON.stringify(ecpoint);

            var vout = Module.cpp_SmartContract_Contract_CreateSignatureRedeemScript(strJson);
            console.log(vout);
        }
    </script>
</body>
</html>
```

**Note:** Ensure that the `emscripten` output naming convention matches the expected module name (`Module`) for compatibility with the SDK functions.

## Contributing

We welcome contributions to enhance and extend the functionality of this project. For guidelines on contributing, please refer to the [Contributing Guidelines](CONTRIBUTING.md).

## License

This project is licensed under the [MIT License](LICENSE).

