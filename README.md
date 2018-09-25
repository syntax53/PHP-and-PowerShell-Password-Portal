## PHP and PowerShell Password Portal
A combination of PHP and PowerShell scripts to allow users to change their Active Directory passwords.  This is NOT a self-service password reset tool.  The user must know their current username and password and this tool will allow them to change it.  Created on IIS 7.5 (2008 R2) using PowerShell 3.0 and PHP 5.6.  Also uses a MySQL database (built on MySQL 5.7) for logging of attempts and IP addresses (in addition to local text file log).

## Features
- Does not require any extravagant permissions to IIS or AD.  Passwords are changed by specifying a **correct** current password.  Therefore the users are basically changing their passwords themselves and only an account with read access to AD is required.
- Verification of valid characters in username, password length and matching for new and confirmed passwords.
- Escaping of all potentially hazardous/malicious username and password characters passed between web and powershell.
- Logging of web attempts to MySQL database along with lockouts after X and Y number of attempts per IP.  e.g. After X attempts in an hour or Y attempts per day they are locked out from making further requests.
- Logging of PowerShell script executions to text file.

## Setup
1. Verify PowerShell and PHP are installed and working under IIS.
1. Create an Active Directory user that has rights to **READ** (NOT write) to your AD forest.  e.g. Just create a new user and give it no additional access.
1. Create a new Application Pool in IIS and set it to run as this new user.
1. Create a folder in IIS (virtual or physical) and convert it to an application.  Set it to run under the newly created application pool.
1. Place the PHP script in this folder.
1. Place the PowerShell script anywhere you want.  I suppose for extra security it should be placed outside of your web site structure.
1. Create a "change_password.log" next to the powershell script and give your application pool user access to write to it.
1. Import the SQL to setup your database and tables.
1. Edit the PHP script and supply database username and password and correct pathing to the PowerShell script.


