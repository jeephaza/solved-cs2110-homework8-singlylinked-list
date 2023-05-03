Download Link: https://assignmentchef.com/product/solved-cs2110-homework8-singlylinked-list
<br>
In this assignment, you will implement a list data structure whose underlying implementation is a singlylinked list. If you have taken CS 1332 (don’t worry if you haven’t), then you should be familiar with this data structure. Your linked list will be able to add and remove person structs, query the data that it stores, and even perform some additional library functions such as reverse and copy. <a href="https://en.wikipedia.org/wiki/Linked_list">https://en.wikipedia.org/wiki/Linked_list</a>

You have been given one C file, <strong>list.c</strong>, in which to implement the data structure. Implement all functions in this file. Each function has a block comment that describes exactly what it should do.

Be sure not to modify any other files. Doing so will result in point deductions that the tester will not reflect. You may feel free to modify the files for the tester however you like though for debugging purposes (namely <strong>list suite.c</strong>).

All #include directives have been included for you. Do not add any more includes. Doing so will result in point deductions that the tester will not reflect.

<h2><a name="_Toc5821"></a>1.1         Dependencies</h2>

There are some dependencies for running the tests.

If you are using Docker, re-run cs2110docker.sh to stop the old container, download updates to the image (which include these dependencies), and restart the container.

If you are using a VM, run

$ sudo apt install build-essential gdb valgrind pkg-config check

<h2><a name="_Toc5822"></a>1.2         Linked List Implementation</h2>

data pointer references what is being stored, and the next pointer references the next list node along the chain. <strong>Do not </strong>change the definition of the list node struct. <strong>Do not </strong>use sentinel or dummy nodes in your list.

<h1><a name="_Toc5823"></a>2           Deliverables</h1>

Submit ONLY list.c.

<strong>Your files must compile with our Makefile, which means it must compile with the following gcc flags:</strong>

-std=c99 -pedantic -Wall -Werror -Wextra -Wstrict-prototypes -Wold-style-definition

<strong>All non-compiling homeworks will receive a zero. </strong>If you want to avoid this, do not run gcc manually; use the Makefile as described below.

Please check your submission after you have uploaded it to gradescope to ensure you have submitted the correct file.

<h1><a name="_Toc5824"></a>3           Background</h1>

<h2><a name="_Toc5825"></a>3.1         Linked Lists, Continued</h2>

A linked list is an ordered list of nodes. Each node in the list is comprised of two consecutive values in memory: a pointer to the next node and a pointer to the data being stored by that node. Since both of these values are addresses, each value is 64 bits or 8 bytes on a 64-bit architecture.

Consider an example list with a head (starting node) at address x4000.

Address | Contents | Comments

———+———-+————–

<table width="216">

 <tbody>

  <tr>

   <td width="77">x4000 |</td>

   <td width="139">x4010 | Node 1: next</td>

  </tr>

  <tr>

   <td width="77">x4008 |</td>

   <td width="139">x0035 | Node 1: data</td>

  </tr>

  <tr>

   <td width="77">x4010 |</td>

   <td width="139">x4030 | Node 2: next</td>

  </tr>

  <tr>

   <td width="77">x4018 |</td>

   <td width="139">x0101 | Node 2: data</td>

  </tr>

  <tr>

   <td width="77">x4020 |</td>

   <td width="139">x0000 | Node 4: next</td>

  </tr>

  <tr>

   <td width="77">x4028 |</td>

   <td width="139">x9040 | Node 4: data</td>

  </tr>

  <tr>

   <td width="77">x4030 |</td>

   <td width="139">x4020 | Node 3: next</td>

  </tr>

  <tr>

   <td width="77">x4038 |</td>

   <td width="139">x7000 | Node 3: data</td>

  </tr>

 </tbody>

</table>

Observe that Node 1 points to Node 2 (at address x4010). Node 2 points to Node 3 (at address x4030). Node 3 points to Node 4 (at address x4020). Finally, Node 4 points to address x0000 (i.e. NULL), signaling that this node is the tail node at the end of the list!

Also notice that consecutive nodes need not be next to each other in memory. This quality is what makes it easy to dynamically allocate additional nodes without needing to reallocate the entire list when we need more space.

<h2><a name="_Toc5826"></a>3.2         Data Structure Design</h2>

The design of this list library is such that the person using your library does not have to deal with the details of the implementation of your library (i.e. the list node struct used to implement the list). None of these functions return a struct list node nor do any of these functions take in a struct list node. It is your responsibility to create the nodes and add them into the list yourself, not the user. When the user is done with the list, they will call empty list which removes all of the person structs from the list and frees the nodes that contained pointers to the person structs. Finally, you must free the list structure yourself so that no memory is leaked by your function.

<h2><a name="_Toc5827"></a>3.3         Testing &amp; Debugging</h2>

We have provided you with a test suite to check your linked list that you can run locally on your very own personal computer. You can run these using the Makefile.

<strong>Note: </strong>There is a file called test utils.o that contains some functions that the test suite needs. We are not providing you the source code for this, so make sure not to accidentally delete this file as you will need to redownload the assignment. Also keep in mind that this file does not have debugging symbols so you will not be able to step into it with gdb (which will be discussed shortly).

Your process for doing this homework should be to write one function at a time and make sure all of the tests pass for that function. Then, you can make sure that you do not have any memory leaks using valgrind. It doesn’t pay to run valgrind on tests that you haven’t passed yet. Further down, there are instructions for running valgrind on an individual test under the Makefile section, as well as how to run it on all of your tests.

The given test cases are the same as the ones on Gradescope. Note that you will pass some of these tests by default. Your grade on Gradescope may not necessarily be your final grade as we reserve the right to adjust the weighting. However, if you pass all the tests and have no memory leaks according to valgrind, you can rest assured that you will get 100 as long as you did not cheat or hard code in values.

You will not receive credit for any tests you pass where valgrind detects memory leaks or memory errors. Gradescope will run valgrind on your submission, but you may also run the tester locally with valgrind for ease of use.

Printing out the contents of your structures can’t catch all logical and memory errors, which is why we also require you run your code through valgrind.

We certainly will be checking for memory leaks by using valgrind, so if you learn how to use it, you’ll catch any memory errors before we do.

Here are tutorials on valgrind:

<a href="http://cs.ecs.baylor.edu/~donahoo/tools/valgrind/">http://cs.ecs.baylor.edu/</a><a href="http://cs.ecs.baylor.edu/~donahoo/tools/valgrind/">~</a><a href="http://cs.ecs.baylor.edu/~donahoo/tools/valgrind/">donahoo/tools/valgrind/ </a><a href="http://valgrind.org/docs/manual/quick-start.html">http://valgrind.org/docs/manual/quick-start.html</a>

Your code must not crash, run infinitely, nor generate memory leaks/errors.

Any test we run for which valgrind reports a memory leak or memory error will receive no credit.

If you need help with debugging, there is a C debugger called gdb that will help point out problems. See instructions in the Makefile section for running an individual test with gdb.

If your code generates a segmentation fault then you should first run gdb before asking questions. We will not look at your code to find your segmentation fault. This is why gdb was written to help you find your segmentation fault yourself. Here are some tutorials on gdb:

<a href="https://www.cs.cmu.edu/~gilpin/tutorial/">https://www.cs.cmu.edu/</a><a href="https://www.cs.cmu.edu/~gilpin/tutorial/">~</a><a href="https://www.cs.cmu.edu/~gilpin/tutorial/">gilpin/tutorial/ </a><a href="http://www.cs.yale.edu/homes/aspnes/pinewiki/C%282f%29Debugging.html">http://www.cs.yale.edu/homes/aspnes/pinewiki/C%282f%29Debugging.html </a><a href="http://heather.cs.ucdavis.edu/~matloff/UnixAndC/CLanguage/Debug.html">http://heather.cs.ucdavis.edu/</a><a href="http://heather.cs.ucdavis.edu/~matloff/UnixAndC/CLanguage/Debug.html">~</a><a href="http://heather.cs.ucdavis.edu/~matloff/UnixAndC/CLanguage/Debug.html">matloff/UnixAndC/CLanguage/Debug.html </a><a href="http://heather.cs.ucdavis.edu/~matloff/debug.html">http://heather.cs.ucdavis.edu/</a><a href="http://heather.cs.ucdavis.edu/~matloff/debug.html">~</a><a href="http://heather.cs.ucdavis.edu/~matloff/debug.html">matloff/debug.html </a><a href="http://www.delorie.com/gnu/docs/gdb/gdb_toc.html">http://www.delorie.com/gnu/docs/gdb/gdb_toc.html</a>

Getting good at debugging will make your life with C that much easier.

<h2><a name="_Toc5828"></a>3.4         Makefile</h2>

We have provided a Makefile for this assignment that will build your project. Here are the commands you should be using with this Makefile:

<ol>

 <li>To clean your working directory (use this command instead of manually deleting the .o files): make clean</li>

 <li>To run the tests without valgrind or gdb: make run-tests</li>

 <li>To run your tests with valgrind: make run-valgrind</li>

 <li>To debug a specific test with valgrind: make TEST=test name run-valgrind</li>

 <li>To debug a specific test using gdb: make TEST=test name run-gdb Then, at the (gdb) prompt:

  <ul>

   <li>Set some breakpoints (if you need to — for stepping through your code you would, but you wouldn’t if you just want to see where your code is segfaulting) with b suites/list suite.c:420, or b list.c:69, or wherever you want to set a breakpoint</li>

   <li>Run the test with run</li>

   <li>If you set breakpoints: you can step line-by-line (including into function calls) with s or step over function calls with n</li>

   <li>If your code segfaults, you can run bt to see a stack trace</li>

  </ul></li>

</ol>

For more information on gdb, please see one of the many tutorials linked above.

To get an individual test name, you can look at the output produced by the tester. For example, the following failed test is test list size empty:

suites/list_suite.c:906:F:test_list_size_empty:test_list_size_empty:0: Assertion failed… ^^^^^^^^^^^^^^^^^^^^

Beware that segfaulting tests will show the line number of the last test assertion made before the segfault, not the segfaulting line number itself. This is a limitation of the testing library we use. To see what line in your code (or in the tests) is segfaulting, follow the “To debug a specific test using gdb” instructions above