# MayaPythonDebuggingHowTo
A little how to for how to debug code in Maya Python

Note: this how to is summarized from this link: https://www.aleksandarkocic.com/2020/12/25/debugging-in-maya-with-debugpy-and-vscode/

1. Install the official Python extension for Visual Studio (https://marketplace.visualstudio.com/items?itemName=ms-python.python)
2. Download the latest source code zip of debugpy from https://github.com/microsoft/debugpy/releases/
3. Unzip the folder and copy it to the Maya script location (maybe /users/animation/[USERNAME]/maya/[VERSION_YEAR]/scripts for BYU students)
4. Open Maya and run:
```
import os
import debugpy
mayapy_exe = os.path.join(os.environ.get("MAYA_LOCATION"), "bin", "mayapy")
debugpy.configure(python=mayapy_exe)
debugpy.listen(5678)
```
5. In VS Code, create a `.vscode` folder in the main workspace folder and then create a `launch.json` file in this folder:
 ![image](https://github.com/AnsonSavage/MayaPythonDebuggingHowTo/assets/12112399/d2dcf958-baf6-42ac-a6a8-31c59ae96fb5)

6. Copy this code into it (make usre that the port number matches the port that you asked debugpy to listen on):
```
{
 "version": "0.2.0",
 "configurations": [
     {
         "name": "Python Attach",
         "type": "python",
         "request": "attach",
         "port": 5678,
         "host": "127.0.0.1",
     }
 ]
}
```

7. Open the debugging panel in VS Code and click start debugging:
![image](https://github.com/AnsonSavage/MayaPythonDebuggingHowTo/assets/12112399/fb000d0a-2b88-48bc-8814-4e4faafeed2b)

8. Set breakpoints or whatever other debugging magic you want to do in VS Code.
9. Run the Code you are debugging in Maya. You can now step through it and debug it in VS Code!

Gotchas:
 - If you get an error about the Port not being available in VS Code or Maya, you can try the following:
   - Changing the port number or
   - If you are using Google Chrome:
     - Close all instances of Chrome
     - Run this command in your terminal ` google-chrome --remote-debugging-port=5678` (make usre the port number matches the port you are trying to connect to)
     - Leave the new Chrome that is started from this command open
     - Ensure that debugpy is listening by running command 4 in Maya
     - Click the debug button again in VS Code.
