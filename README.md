# ToDo API realisiert mit IaaS (dummy backend)

## Before you begin
1. Open VS Code
2. Clone the following repo from Github:  https://github.com/modul346/iaas-todoapi-dummy-backend.git
3. Put it into the folder where you keep all the other projects of this module

## Steps for Setup in Azure

1. Create Resource Group with the name IaaS in the Region Switzerland North
2. Create a Virtual Machine (Azure virtual machine)
3. Set the Resource group to IaaS
4. Set the name of the VM to ToDoAPIServer
5. Region Switzerland North
6. Image = Windows Server 2022 Datacenter: Azure Edition - Gen2
7. Username: todoadmin
8. Password: LukeSkywalker2022
9. Select Would you like to use an existing license
10. And confirm your selection
11. Create VM (leaving all the other settings to their default values)
12. Goto the newly created VM
13. Click on Connect (on top of the page) 
14. Choose RDP
15. Download the RDP file
16. Click on the downloaded file to open it
17. Enter username and password
18. Wait until the server is initialized and the Server Manager Dashboard opens
19. Allow the computer to be discovered in the network
20. Click on Manage in the top right corner
21. Select Add Roles and Features
22. Click Next
23. Select Role-based or feature-based installation and click Next
24. Click Next
25. Select the Server Role Web Server (IIS)
26. Click Add Features
27. Click Next
28. Click Next
29. Click Next
30. Click Next
31. Click Install
32. Wait (ca. 5 minutes) for the installation to finish
33. Click Close
34. In order to get our API to run on the server we have to run a small update on it
35. Under our project folder in VS Code you find a folder called ServerUpdate. In it you find a file called dotnet-hosting-6.0.10-win.exe
36. Copy this file via Copy/Paste into the c:\Temp folder on the server
37. Execute the file and it will install (repair) the missing files on the server

Wir haben jetzt einen funktionierenden WebServer mit der typischen IIS Default Seite
Unsere nächste Aufgabe ist es zu überprüfen ob wir diese Seite aufrufen können.
Dazu müssen wir die Network Security Group (Firewall) anpassen.

38. Switch back to the Azure Portal and go into the IaaS Resource Group
39. There you will find ToDoAPIServer-nsg  (Network Security Group) - open it
40. On the left side you will find Inbound security rules - Click on it
41. Click on Add (on the top)
42. Leave all the default values only change the Destination port ranges to 80
43. Click Add
44. After the Inbound rule ist created click Refresch (on top) and the new rule should be there
45. Create another Inbound rule this time for port 443 (Https)
46. In the Azure Portal open the VM
47. Take notice of the public IP-Address and copy it to the clipboard (hover over)
48. Open a new browser tab and paste the IP-Address
49. The default IIS Webpage should appear
50. Now go back to your RDP Server Session
51. Click on Tools (top right) and select Internet Information Manager (IIS)
52. On the left side open the tree until you see Default Web Site.
53. Select it
54. On the right select Explore
55. An explorer window has opened and we see the two default files that we will replace now with the compiled files of our API
56. Now we switch back to VS Code where we have the directory of our API open
57. Open a terminal
58. Type "dotnet restore" to load the dependencies of our API
59. Type "dotnet build" to make sure that our API compiles without any errors 
60. Type "dotnet publish" to create the files that we will deploy to the server
61. Under the bin directory you will find a folder called publish
62. Right click on the folder and select Reveal in File Explorer
63. All these files in this folder now have to be copied into the wwwroot folder on the server
64. The easiest way to do is with Copy/Paste
65. Do you still have the IP-Address of your server? If not go get it again
66. Open the file apitest.http in the folder RestClient in VS Code
66. Set the @hosturl variable to the server IP-Address. It should look something like this  http://20.203.143.225  (http not https)
63. Now you can test the API!

### Remember to delete the resource group when you are finished





