 I followed below steps for the execution :-

● Ubuntu server/VM creation and ssh. 

●Configuring Ubuntu on remote VM

• Updating the outdated packages and dependencies - 

- sudo apt update


• Install Git - 

- sudo apt install git 


• Configure Node.js and npm (package manager) - 

- sudo apt install node.js

- sudo apt install npm


●Deploying the project on Azure

• Clone this project in the remote VM

git clone https://lnkd.in/g9x-eXX8 



Setup the following environment variables - (.env) file
DOMAIN= ""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY=""
SECRET_KEY=""

For this project , I used 'Stripe.com' for setting up publishable and secret api keys in .env file.

● Initialise and start the project

- npm install
- npm run start

"The server was listening at 3000"

The Challenge : 
After setting up the VM, installing Node.js, and running the app, I couldn’t access it via the browser using the VM’s public IP and port. The dreaded "Site Can’t Be Reached" error haunted me! 😅 

Root Causes : 
1️⃣ Azure Network Security Group (NSG): By default, Azure blocks all inbound traffic except SSH. 
2️⃣ Node.js Binding: My app was listening on `localhost` instead of `0.0.0.0`, blocking external requests. 
 

The Fix : 
✅ Azure NSG Inbound Rule: Added a custom inbound rule in Azure’s Networking tab to allow traffic on my app’s port (e.g., 3000). 
✅ Node.js Binding : Updated `app.listen()` to bind to `0.0.0.0` instead of `127.0.0.1`. 


Key Takeaways : 
- Cloud Security Layers: Azure’s NSG acts as a first line of defense—always configure it for your app’s needs! 
- 0.0.0.0 vs. localhost : A tiny code tweak can make or break external accessibility. 
- Persistence Pays Off : Debugging infrastructure issues is frustrating but rewarding once resolved! 

Tools Used : 
- Microsoft Azure (Ubuntu VM) 
- Node.js, PM2 (Process Manager) 
-Github


🔗 Why Share This?
Infrastructure setup is often overlooked in tutorials, but it’s where *real-world magic* (and headaches) happen! If you’re deploying to the cloud, double-check: 
1. Firewall/NSG Rules
2. Port Bindings
3. Logs, Logs, Logs!
