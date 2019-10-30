## Welcome
This is an example project showing how to allow react native project to use node.js core modules.

### 1. Integration

#### Create project with react native cli
```bash
react-native init projectname
```

#### Install latest rn-nodeify
```bash
npm i --save-dev rn-nodeify@latest
```

#### Install node core shims and recursively hack package.json files
#### In ./node_modules to add/update the "browser"/"react-native" field with relevant mappings
```bash
./node_modules/.bin/rn-nodeify --hack --install
```

#### Import shim.js in project index.js
```js
import './shim.js'
import {AppRegistry} from 'react-native';
import App from './App';
import {name as appName} from './app.json';
```

#### Test modules in project app.js
```js
import crypto from 'crypto'

console.log(crypto.randomBytes(32).toString('hex'));
```

#### Update package.json in script section
```json
{
  "scripts": {
    "android": "react-native run-android",
    "ios": "react-native run-ios",
    "start": "react-native start",
    "test": "jest",
    "lint": "eslint .",
    "install_modules": "npm install && ./node_modules/.bin/rn-nodeify --hack --install && cd ios && pod install && cd .."
  }
}
```

### 2. Usage

After integration is done, later on when finishing cloning project from git repository then just enter project directory and run command below in terminal
```bash
npm run install_modules
```
