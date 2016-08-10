# Alfresco Mock Rest Api

Alfresco Mock API - is a suite of class to mock the alfresco-core-rest-api alfresco-auth-rest-api

Alfresco Mock API use [Nock](https://github.com/node-nock/nock) which is an HTTP mocking and expectations library for Node.js
                                                                

### Basic usage For node projects

```javascript
var AlfrescoMockJsApi = require('alfresco-js-api').Mock;
```

# Mock Auth Api

var AuthResponseMock = require('alfresco-js-api').Mock.Auth

authResponseMock = new AuthResponseMock(host);

Method | Description  |
------------- | ------------- |
authResponseMock.authResponseMock.get201Response(forceTicket);| | 
authResponseMock.get403Response()| | 
authResponseMock.get400Response()| | 
authResponseMock.get401Response()| | 
authResponseMock.get204ResponseLogout()| | 
authResponseMock.get404ResponseLogout()| | 
authResponseMock.rec()| | 
authResponseMock.play()| | 

##Example 

```javascript
var AlfrescoApi = require('alfresco-js-api');
var expect = require('chai').expect;
var AuthResponseMock = require('alfresco-js-api').Mock.Auth;

var host = 'http://127.0.0.1:8080';
var authResponseMock = new AuthResponseMock(host);

authResponseMock.get201Response('TICKET_4479f4d3bb155195879bfbb8d5206f433488a1b1');

var alfrescoJsApi = new AlfrescoApi({
    username: 'admin',
    password: 'admin',
    host: host
});

alfrescoJsApi.login().then((data) => {
    expect(data).to.be.equal('TICKET_4479f4d3bb155195879bfbb8d5206f433488a1b1');
    done();
});
```

# Mock Node Api

var NodeMock = require('alfresco-js-api').Mock.Node

nodeMock = new NodeMock(host);

Method | Description  |
------------- | ------------- |
nodeMock.get200ResponseChildren()| | 
nodeMock.get200ResponseSingleFileFolder()| | 
nodeMock.get404ChildrenNotExist()| | 
nodeMock.get404FileFolderNotExist()| | 
nodeMock.get204SuccessfullyDeleted()| | 
nodeMock.get403DeletePermissionDenied()| | 
nodeMock.get404DeleteNotFound()| | 
nodeMock.get404DeletePermanentlyNotFound() | | 
nodeMock.get200CreationFolder()| | 
nodeMock.get409CreationFolderNewNameClashes()| | 
nodeMock.get201CreationFolderNewNameNotClashes()| | 
nodeMock.rec();| | 
nodeMock.play();| | 

##Example 

```javascript
var AlfrescoApi = require('alfresco-js-api');
var expect = require('chai').expect;
var AuthResponseMock = require('alfresco-js-api').Mock.Auth;
var NodeMock = require('alfresco-js-api').Mock.Node;


var host = 'http://127.0.0.1:8080';
var authResponseMock = new AuthResponseMock(host);
var nodeMock = new NodeMock(host);

authResponseMock.get201Response();

var alfrescoJsApi = new AlfrescoApi({
    username: 'admin',
    password: 'admin',
    host: this.host
});

alfrescoJsApi.login();

nodeMock.get200CreationFolder();

alfrescoJsApi.node.createFolder('newFolder').then(function (data) {
    expect(data.entry.name).to.be.equal('newFolder');
    expect(data.entry.isFolder).to.be.equal(true);
    done();
});
```

# Mock Upload Api

var UploadMock = require('alfresco-js-api').Mock.Upload

uploadMock = new UploadMock(host);

Method | Description  |
------------- | ------------- |
uploadMock.get201CreationFile()| | 
uploadMock.get201CreationFileAutoRename()| | 
uploadMock.get409CreationFileNewNameClashes()| | 
uploadMock.get401Response()| | 
uploadMock.rec()| | 
uploadMock.play()| | 


```javascript
var AlfrescoApi = require('alfresco-js-api');
var expect = require('chai').expect;
var AuthResponseMock = require('alfresco-js-api').Mock.Auth;
var UploadMock = require('alfresco-js-api').Mock.Upload;


var host = 'http://127.0.0.1:8080';
var authResponseMock = new AuthResponseMock(host);
var uploadMock = new UploadMock(host);

authResponseMock.get201Response();

var alfrescoJsApi = new AlfrescoApi({
    username: 'admin',
    password: 'admin',
    host: this.host
});

alfrescoJsApi.login();

uploadMock.get201CreationFile();

var file = fs.createReadStream('./test/mockObjects/testFile.txt');

alfrescoJsApi.upload.uploadFile(file).then(function (data) {
    expect(data.entry.isFile).to.be.equal(true);
    expect(data.entry.name).to.be.equal('testFile.txt');
    done();
});

```


# WebScript Upload Api

var UploadMock = require('alfresco-js-api').Mock.WebScript

webScript = new WebScript(host);

Method | Description  |
------------- | ------------- |
WebScript.get404Response()| | 
WebScript.get401Response()| | 
WebScript.get200Response()| | 
uploadMock.rec()| | 
uploadMock.play()| | 


```javascript
var AlfrescoApi = require('alfresco-js-api');
var expect = require('chai').expect;
var AuthResponseMock = require('alfresco-js-api').Mock.Auth;
var WebScriptMock = require('alfresco-js-api').Mock.WebScript;

var host = 'http://127.0.0.1:8080';
var contextRoot = 'script';
var servicePath = 'alfresco';
var scriptPath = 'testWebScript';

var authResponseMock = new AuthResponseMock(host);
var uploadMock = new UploadMock(host);

authResponseMock.get201Response();

var alfrescoJsApi = new AlfrescoApi({
    username: 'admin',
    password: 'admin',
    host: this.host
});

var webScriptMock = new WebScriptMock(host, contextRoot, servicePath, scriptPath);

webScriptMock.get200Response();

alfrescoJsApi.webScript.executeWebScript('GET', scriptPath, null, contextRoot, servicePath)
.then((data)=> {
   expect(data).to.not.be.undefined;
});

```