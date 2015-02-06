# message-endpoint
Demonstrating testing a user sessions endpoint. 

Install
 npm install message-endpoint --save-dev 

Usage
Create a test file 'message-endpoint/test.md' to test the 'message/get' endpoint, like this:
# message/get
## Setup
### messages of message board
    name: 'You Rock'
    value: 500
## Invalid request
### Post
    randomId()
### Out 400
    error:
        code: 200
## Valid request
### Post
    message.id
### Out
    name: message.name
    value: message.value

testing code:

require('message-endpoint')('message-endpoint/test.md', {
    sampleUri: 'sampledb://localhost:20000/message-endpoint',
    baseUrl: 'http://localhost:8000/'
})

Variables to be used in the test cases:
### _varName_ is
    _variableContent_

This will make varName available to every following object block.

Test cases
•  Post : the JSON body to send by POST.
•  Out : the expected JSON output. Default: no output checking. The statusCode is optional and defaults to 200

Object Definition:

user with name.first: 'Tester01'

•  baseUrl : the base API url. Every request url will be composed from this base and the test name.

Type checking
If you don't know the exact value for an API response or field in the collection, you can check for its type:
## Testing types
### Post
    ...
### Out
    token: String

The valid type values are:  String ,  Number ,  Boolean ,  Object ,  Array ,  Date ,  RegExp ,  ObjectId .

Custom context
if all endpoints return errors like this:  {error: {code: _code_, message: _aDebugString_}} , you can pass as context:

options.context = {
    error: function (code) {
        return {
            error: {
                code: code,
                message: String
            }
        }
    }
}

And then write a test case like this:
## Invalid message should give error 200
### Post
    name:
        message: randomMessage()
### Out
    error(200)


Run message-endpoint

