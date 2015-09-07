#Step 3 - Refactoring Device & DvdApp

There's just one very small change required in the <c1><b>Device</b></c1> class - can you identify what it is? (before you refer to the notes?)

The <c1><b>DvdApp</b></c1> class will still be your void main() and still execute the looping mechanism for the user menu.  

To help you along, you can just replace your existing void main() method with the following (Don't forget to remove the comments!!) - be aware that until you refactor your <c1><b>DvdManager</b></c1> class, a number of errors will exist in your project.

~~~java
public static void main( String args[] )
    {
    int option;

    DvdManager manager = new DvdManager();
    
    do {
        option = manager.menuMain();

        switch(option)
            {
            case 1 : manager.menuAddDevice();
                     break;
            case 2 : manager.menuPlayDevice();
                     break;
            case 3 : manager.menuListDevices();
                     break; 
            case 4 : /* manager.writeToFile(); */
                     break; 
            default : break;
            }
        } while(option != 4);
    } 
~~~
