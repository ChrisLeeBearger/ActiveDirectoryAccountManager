# ActiveDirectoryAccountManager

This desktop application was created to allow IT engineers to quickly and effectively  change all their Active Directory passwords across multiple domains.

![Application Image](https://raw.githubusercontent.com/ChrisLeeBearger/ActiveDirectoryAccountManager/master/doc/app_image_01.png)

## How it Works

* Searches user accounts in all configured domains based on the [sAMAccountName](https://docs.microsoft.com/en-us/windows/win32/ad/naming-properties#samaccountname) of the user currently running the app. This means that relevant user accounts are only found in case there is a naming convention applied to the sAMAccountName across all domains. (e.g.  DOMAIN1\\**jdoe**, DOMAIN2\\**jdoe**, DOMAIN3\\**jdoe**,...)
* Current password and new password can be set either for all user accounts at once or individually.
* Password can only be changed before expiration. If an expired user account is found it will be automatically unchecked and ignored.
* The password change and search will be performed with the provided credentials. There is no super user required for the app to work.
* All credentials are held in Memory as [SecureString](https://docs.microsoft.com/en-us/dotnet/api/system.security.securestring).
* The initial search is performed with the currently logged in user, only if their is a domain trust setup user accounts within other domains are found immediately. If this is not in place the search will be performed again with domain local credentials as soon as a password has been provided.

## Technologies

* [PowerShell](https://docs.microsoft.com/en-us/PowerShell/)
* [XAML](https://docs.microsoft.com/en-us/visualstudio/xaml-tools/xaml-overview)
* [MahApps](https://mahapps.com/)

## Requirements
* [PowerShell](https://docs.microsoft.com/en-us/PowerShell/) 5.0 or later
* [Remote Server Administration Tools](https://docs.microsoft.com/en-us/windows-server/remote/remote-server-administration-tools) installed on the machine that will run the client
* Port 9389 for [Active Directory Web Services](https://docs.microsoft.com/en-us/troubleshoot/windows-server/networking/service-overview-and-network-port-requirements#system-services-ports) opened from the client to all domain controllers.

## Getting Started
1. Make sure that all points under requirements are in place.
2. Clone the repository and open the [config.csv](https://github.com/ChrisLeeBearger/ActiveDirectoryAccountManager/blob/master/config.csv) file.
3. Remove all of the example domains from the file.
4. Add the domains that should be searched for accounts.
5. You are done, start the app via adam.exe and begin searching for your user accounts.

## Configuration File
The domains need to be configured in the [config.csv](https://github.com/ChrisLeeBearger/ActiveDirectoryAccountManager/blob/master/config.csv) file located in the root folder of the app.

|Column| Description | Example |
| ------------- | ------------- | ------------- | 
| DomainName  | The name that is going to be displayed | Contoso |
| DomainController  | Hostname of the domain controller that will be used to change the password | contoso-dc1 |
| DomainBase  | The full qualified domain name  | contoso.lan |
