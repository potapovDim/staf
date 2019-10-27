# Simple Test Automation Framework
## Quick start
All quickstart code is stored in repo: https://github.com/geokur/staf-examples
### Install Simple Test Automation Framework
```shell
npm install -g staf
```
### Create simple test
Create test class, save into 'first-test.js' in 'test' folder
```javascript
const assert = require('assert').strict

class SimpleTest {
    mySimpleTest() {
        return () => {
            assert.ok(true)
        }
    }
}

module.exports = SimpleTest
```
And configuration file for test runner in file 'test-config.js'
```javascript
module.exports = {
    testPath: 'test'
}
```
Project structure should look like this:
```
project
+-- test
    +-- simple-test.js
+-- test-config.js
```
Execute the test:
```shell
staf test-config.js
```
Create test with properties
```javascript
const assert = require('assert').strict

class PropertyTest {
    myPositiveTest(properties) {
        properties.type = 'positive'
        return () => {
            assert.ok(true)
        }
    }
    myNegativeTest(properties) {
        properties.type = 'negative'
        return () => {
            assert.ok(false)
        }
    }
}

module.exports = PropertyTest
```
And configuration file for test runner in file 'positive-test-config.js'. Notice method 'schedule'. It is used to filter only 'positive' tests.
```javascript
module.exports = {
    testPath: 'test',
    schedule(tests) {
        const onlyPositive = tests.filter(test => test.testProperties.type === 'positive')
        return onlyPositive
    }
}
```
Execute the test:
```shell
staf positive-test-config.js
```