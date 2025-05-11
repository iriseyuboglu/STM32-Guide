Setting up a project in CubeMX:

1. New project
2. Select the board you're working with
3. Go to the Project Manager tab and give your project a name, remember to change the ToolChain/IDE to MakeFile
4. Change whatever pins are needed (can vary a lot) and click on "GENERATE CODE". (watch out: if only options were changed and not pins, the code won't be generated, so please if you haven't changed any, modify a pin to some role and then and undo it, as that will register as a modification and make the code actually generate)

Open the folder with the project on Visual Studio Code (the whole folder, don't go inside of it).
There's two mandatory steps you have to follow everytime you open a new project (wouldn't be necessary if CubeMX wasn't completely broken: java written applications in a nutshell):

1 - Change the launch.json file, adding this line somewhere between line 4 and line 15:

"gdbPath": "gdb-multiarch", //(remember the end comma)

2 - Changed the file STM32XXXXXXXX_FLASH.ld (you'll have your board number instead of the various 'X' characters), erasing all its content and swapping it with the file we have in this same directory with that same name (be careful, the file can have some minor differences depending on the board, but the latest CubeMX update should have sorted this out completely)

Now go on to code! :)
