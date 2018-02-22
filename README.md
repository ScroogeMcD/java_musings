# java_musings

I. Determining which core a thread is running on. [uses JNI calls]
   [The threads are created inherently using parallelStream(), which in turn uses the shared threadpool ForkJoinPool.commonPool()]
  Steps to build and execute:
  1. javac CpuTest.java
  2. javah CpuTest
  3. gcc -c -fPIC -I/usr/local/java/jdk1.8.0.60/include -I/usr/local/java/jdk1.8.0.60/include/linux CpuTest.c
  4. gcc -shared -o libprintcpu.so CpuTest.o [Note : the name of the shared object must start with the string 'lib']
  5. export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:<path_to_your_shared_object>  [To set java.library.path]
  6. java CpuTest -XshowSesstings:properties
