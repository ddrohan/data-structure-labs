#Step 2 - Adding classes Device & Cd

You need to create two new classes, namely 

- Cd

- Device

and refactor the other classes that already exist in the project.

The new <c1><b>Cd</b></c1> class should contain an 

- id

- title

- price (similar to the <c1><b>Dvd</b></c1> class) 

and also hold an 

- artist 

property. 

Supply all the necessary setter and getter methods as well as a constructor and a toString() method. This class should also inherit from the <c1><b>Device</b></c1> class.

The new <c1><b>Device</b></c1> class should contain all properties and behaviour common to both the <c1><b>Cd</b></c1> class and the <c1><b>Dvd</b></c1> class, so you might have to take some time to decide what methods and properties go where.

Also, there are a number of abstract methods that need to be declared in this class, which are as follows

~~~java
public abstract void play();

public abstract String decoder();
~~~

so implementing these will involve moving around and refactoring some more code. The decoder() method should just return either the text ".avi" or ".mp3" depending on which object it's called on.

The existing <c1><b>Dvd</b></c1> class needs to be refactored to reflect the fact that it inherits from the <c1><b>Device</b></c1> class and also adds a 

- region 

property.

The <c1><b>DvdApp</b></c1> class will still be your void main() and execute the looping mechanism for the user menu.  To help you along, you can just replace your existing void main() method with the following - be aware that until you refactor your <c1><b>DvdManager</b></c1> class, a number of errors will exist in your project.

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
            case 4 : break; 
            default : break;
            }
        } while(option != 4);
    } 
~~~
