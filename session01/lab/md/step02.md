#Step 2 - classes Dvd & DvdApp

Create three classes in the <c1><b>ie.wit.dvd</b></c1> package, namely 
<b>

- Dvd, 

- DVDApp and 

- DVDManager (which we'll look at in more detail later)

</b>

The <c1><b>Dvd</b></c1> class should contain 

- an id, 

- a title and 

- a price. 

Supply all the necessary setter and getter methods as well as a constructor and a toString() method. You will be shown in later Labs how to generate all these methods automatically (if you don't know how to already) but for the moment (and as a refresher) code these methods manually.

The <c1><b>DVDApp</b></c1> class will basically be your void main() and execute the looping mechanism for the user menu.  To help you along, you can just replace your existing void main() method with the following - be aware that until you update your <c1><b>DvdManager</b></c1> class, a number of errors will exist in your project.

~~~java
public static void main( String args[] )
    {
    int option;

    DvdManager manager = new DvdManager();
    
    do {
        option = manager.menuMain();

        switch(option)
            {
            case 1 : manager.menuAddDvd();
                     break;
            case 2 : manager.menuPlayDvd();
                     break;
            case 3 : manager.menuListDvds();
                     break; 
            case 4 : break; 
            default : break;
            }
        } while(option != 4);
    } 
~~~