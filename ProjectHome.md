
---

## NEWS ##
**17/07/12 - Released version 2.0 with package name update. Source available on [Github](https://github.com/kamranzafar/jtar)**

**01/05/12 - Released version 1.1 with bug fixes and updates**

**08/04/11 - Released version 1.0.4 with bug fixes and minor updates**

**13/10/10 - JTar is now available in Maven central repository**

---


**JTar from version 2.0 is available on [github](https://github.com/kamranzafar/jtar).**

## Overview ##
JTar is a simple Java Tar library, that provides an easy way to create and read tar files using IO streams. The API is very simple to use and similar to the java.util.zip package.

## Usage ##
**Tar example - using TarOutputStream**
```
   // Output file stream
   FileOutputStream dest = new FileOutputStream( "c:/test/test.tar" );

   // Create a TarOutputStream
   TarOutputStream out = new TarOutputStream( new BufferedOutputStream( dest ) );

   // Files to tar
   File[] filesToTar=new File[2];
   filesToTar[0]=new File("c:/test/myfile1.txt");
   filesToTar[1]=new File("c:/test/myfile2.txt");

   for(File f:filesToTar){
      out.putNextEntry(new TarEntry(f, f.getName()));
      BufferedInputStream origin = new BufferedInputStream(new FileInputStream( f ));

      int count;
      byte data[] = new byte[2048];
      while((count = origin.read(data)) != -1) {
         out.write(data, 0, count);
      }

      out.flush();
      origin.close();
   }

   out.close();
```

**Untar example - using TarInputStream**
```
   String tarFile = "c:/test/test.tar";
   String destFolder = "c:/test/myfiles";

   // Create a TarInputStream
   TarInputStream tis = new TarInputStream(new BufferedInputStream(new FileInputStream(tarFile)));
   TarEntry entry;
   while((entry = tis.getNextEntry()) != null) {
      int count;
      byte data[] = new byte[2048];

      FileOutputStream fos = new FileOutputStream(destFolder + "/" + entry.getName());
      BufferedOutputStream dest = new BufferedOutputStream(fos);

      while((count = tis.read(data)) != -1) {
         dest.write(data, 0, count);
      }

      dest.flush();
      dest.close();
   }
   
   tis.close();
```



---

**Tip: Always use buffered streams with jtar to speed up IO.**

---


**Examples and resources**

  * See _[JTarTest](http://code.google.com/p/jtar/source/browse/trunk/jtar/src/test/java/org/xeustechnologies/jtar/JTarTest.java)_ class, provided with the source, for more detailed examples.

  * Visit the wiki page for more details on _[Tar format](http://en.wikipedia.org/wiki/Tar_%28file_format%29)_

**Please report bugs to the project owner**