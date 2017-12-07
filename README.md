# DBLogException
Aspectize Extension to automatically log exceptions

# 1 - Download

Download extension package from aspectize.com:
- in the portal, goto extension section
- browse extension, and find BootstrapSwitch
- download package and unzip it into your local WebHost Applications directory; you should have a DBLogException directory next to your app directory.

# 2 - Configuration

Add DBLogException as Shared Application in your application configuration file and configure app.
In your Visual Studio Project, find the file Application.js in the Configuration folder.

Add BootstrapSwitch in the Directories list :
```javascript
app.Directories = "DBLogException";

app.LogEnabled = true;
app.LogServiceName = "MyDbLogExceptionService";
```

Add a new configured service in your Application

In your Visual Studio Project, find the file Services.js in the Configuration folder.

```javascript
var myDbLogExceptionService = Aspectize.ConfigureNewService("MyDbLogExceptionService", aas.ConfigurableServices.DBLogException);
myDbLogExceptionService.DataServiceName = "MyDataService";
myDbLogExceptionService.FileServiceName = "MyFileService";
myDbLogExceptionService.MailServiceName = "MyMailService";
myDbLogExceptionService.MailTo = "recipient1@mycompany.com, recipient2@mycompany.com"; 
```

The Configurable Service has the following parameters:
DataServiceName; name of your DataBaseService used to store Exception Information.
FileServiceName; name of file Service to store Exception Information, in case Exception message is bigger than 32ko (yes, it happens...)
MailServiceName: name of your SMTPService to send an email
MailTo: recipients email adresses, separated by comma.

Each time an exception occured, the exception is logged into your DataBase (in a table LogException), and an email is sent to recipients; log report stack and error message.
