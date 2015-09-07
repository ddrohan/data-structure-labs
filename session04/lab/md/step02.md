#Step 2 - class FileHandler

Similar to the previous lab, you just need to create one new class, namely <c1><b>FileHandler</b></c1> and refactor the other classes that already exist in the project.

The new <c1><b>FileHandler</b></c1> class should contain two methods which will write our <c1><b>Device</b></c1> array to a file and read our data back from the file.

~~~java
public void writeToFile(Device[] devices)

public Device[] readFromFile()
~~~

You should refer to the lecture notes to write these methods, as everything you need to complete this step is in there, but to refresh your memory, here are the two methods from the notes we used to read/write 'Person' objects

~~~java
public void writeOut(Person[] p) throws FileNotFoundException, IOException
  {
    oos = new ObjectOutputStream(new FileOutputStream(myFile));
    oos.writeInt(size);
    oos.writeObject(p);
    oos.close();
  }
  
  public Person[] readIn() throws FileNotFoundException, IOException, ClassNotFoundException
  {
    Person[] temp = null;
      ois = new ObjectInputStream(new FileInputStream(myFile));
      size = ois.readInt();
      temp = (Person[]) ois.readObject(); 
      ois.close();
    return temp;
  }
~~~
