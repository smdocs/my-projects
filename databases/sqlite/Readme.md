#SQLite Notes

#### 1. The Architecture Of SQLite

![](http://www.sqlite.org/images/arch2.gif)

#####Key files:

<b> sqlite3.h </b>- This file defines the public interface to the SQLite library. Readers will need to be familiar with this interface before trying to understand how the library works internally.

<b>sqliteInt.h</b> - this header file defines many of the data objects used internally by SQLite.

<b>parse.y</b> - This file describes the LALR(1) grammer that SQLite uses to parse SQL statements, and the actions that are taken at each stop in the parsing process.

<b>vdbe.c</b> - This file implements the virtual machine that runs prepared statements. There are various helper files whose names begin with "vdbe". The VDBE has access to the vdbeInt.h header file which defines internal data objects. The rest of SQLite interacts with the VDBE through an interface defined by vdbe.h.

<b>where.c</b>. - This file analyzes the WHERE clause and generates virtual machine code to run queries efficiently. This file is sometimes called the "query optimizer". It has its own private header file, whereInt.h, that defines data objects used internally.

<b>btree.c </b>- This file contains the implementation of the B-Tree storage engine used by SQLite.

<b>pager.c</b> - This file contains the "pager" implementation, the module that implements transactions.

<b>os_unix.c and os_win.c </b>- These two files implement the interface between SQLite and the underlying operating system using the run-time pluggable VFS interface.

All of the individual C source code and header files (both manually-edited and automatically-generated) can be combined into a single big source file sqlite3.c called <b>"the amalgamation".</b>
