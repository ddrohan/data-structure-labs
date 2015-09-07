#Step 4 - Refactoring DvdManager

A bit of work needs to be done in the <c1><b>DvdManager</b></c1> class to complete this Lab. You need to

- create an instance of a <c1><b>FileHandler</b></c1> object (call it <c1><i>filehandler</i></c1>)

- implement a new method (<c1><i>writeToFile</i></c1>) which will write a <c1><b>Device</b></c1> array to a file. Hint : this method should basically call the <c1><i>FileHandler.writeToFile(..)</i></c1> method.

- refactor the <c1><b>DvdManager</b></c1> constructor to either open the file and load the stored <c1><b>Device</b></c1> data or, if the file is empty, add two <c1><b>Device</b></c1> objects to the empty array (ala previous labs) - again, everything you need is in the lecture notes.