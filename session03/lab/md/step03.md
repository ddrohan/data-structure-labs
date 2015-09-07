#Step 3 - Refactoring Existing classes

There are 2 classes that are affected

- The existing <c1><b>Device</b></c1> class needs to be refactored, specifically the <c1><i>setPrice(..)</i></c1> method, so that the method <c1>throws</c1> an <c1><b>InvalidPriceException</b></c1> exception if the price parameter is invalid.

- The <c1><b>DvdManager</b></c1> class also need to be refactored so that it can <c1>catch</c1> an <c1><b>InvalidPriceException</b></c1> exception. 

Can you identify the correct entry point for this refactoring? Also, make sure you order your <c1>catch</c1> clauses correctly, or you may find some errors pop up in your project.