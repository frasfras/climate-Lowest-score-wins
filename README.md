# climate-Lowest-score wins

In the project directory, you should run:

npm install
And then to run an application with automatic virtual ngrok tunnel, run:

npm start
Visit http://localhost:4040/status and under "command_line section" find the URL. This is the public URL of your app, so you can use it to test it. F.e.: https://021eb6330099.ngrok.io

Download node-red

Install the json flows above if you need to duplicate Visual editoron local host copy:

Configure Monday App
Open monday.com, login to your account and go to a "Developers" section.
Create a new "QuickStart View Example App"
Open "OAuth & Permissions" section and add "boards:read" scope
Open "Features" section and create a new "Boards View" feature
Open "View setup" tab and fulfill in "Custom URL" field your ngrok public URL, which you got previously (f.e. https://021eb6330099.ngrok.io)
Click "Boards" button and choose one of the boards with some data in it.
Click "Preview button"
Enjoy the Quickstart View Example app!


Release your app
Run script
