# Developing
## Requirements
- [Azure storage emulator](https://go.microsoft.com/fwlink/?linkid=717179)
- SQL Server 2019 with Full text index feature
- .NET core SDK version specified [here](/global.json)

## Getting Started in Visual Studio
### Developing
- Install Visual Studio 2019
- [Clone the Medical Imaging Server for DICOM repo](https://github.com/microsoft/dicom-server.git)
- Navigate to the cloned repository
- Open Microsoft.Health.Dicom.sln in VS
- Build
- Make sure the storage emulator is running
- Run all tests from the Test explorer

# Testing
- Set Microsoft.Health.Dicom.Web as your startup project
- Run the project
- Web server is now running at https://localhost:63838/

## Posting DICOM files using Fiddler
- [Install fiddler](https://www.telerik.com/download/fiddler)
- Go to Tools->Options->HTTPS on fiddler. Click protocols and add "tls1.2" to the list of protocols.

![Fiddler Config Image](/docs/images/FiddlerConfig.png)
- Download DCM example file from [here](/docs/dcms/RedTriangle.dcm) 
- Upload DCM file (use upload file button at request body section as shown in picture below) 
- Update request header:
   - Accept: application/dicom+json (don't change boundary part)
   - Content-Type: multipart/related
- Update request body:
   - Content-Type: application/dicom
   - Post the request to https://localhost:63838/studies

![Post A Dicom Image](/docs/images/FiddlerPost.png)
- If the POST is successful, you should be see an HTTP 200 response.

![Post Succeeds](/docs/images/FiddlerSucceedPost.png)
- Note: you cannot upload the same DCM file again unless it is first deleted. Doing so will result in an HTTP 409 Conflict error.

## Postman for Get
- [Install Postman](https://www.postman.com/downloads/)
- Example QIDO to get all studies
```http
GET https://localhost:63838/studies
accept: application/dicom+json
```