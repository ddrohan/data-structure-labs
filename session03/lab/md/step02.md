#Step 2 - class InvalidPriceException

You need to create just 1 new class, namely <c1><b>InvalidPriceException</b></c1>, and refactor the other classes that already exist in the project to <c1>throw</c1> and <c1>catch</c1> this exception.

Refer to the notes if you're not sure where to start but note the following

- This new <c1><b>InvalidPriceException</b></c1> class should simply inform the user that an invalid price (< 0.0) has been entered for the price of a <c1><b>Device</b></c1>

- This class should inherit from a suitable <c1><b>Exception</b></c1> superclass

- the class should have at least 1 constructor (but preferably 2, similar to what we covered in the lectures)