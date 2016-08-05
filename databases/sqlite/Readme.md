#SQLite Notes

#### 1. Main Features
- Serverless - SQLite does not require a separate server process or system to operate. The SQLite library accesses its storage files directly.

- Zero Configuration - No server means no setup. Creating an SQLite database instance is as easy as opening file.

- Cross-Platform - The entire database instance resides in a single cross-platform file, requiring no  administration.

- Self-ContainedA single library contains the entire database system, which integrates directly into a host                   application.

- Small Runtime Footprint - The default build is less than a megabyte of code and requires only a few megabytes of memory. With some adjustments, both the library size and memory use can be significantly reduced.

- Transactional - SQLite transactions are fully ACID-compliant, allowing safe access from multiple processes or                   threads.Full-FeaturedSQLite supports most of the query language features found in the SQL92 (SQL2) standard.

- Highly Reliable - The SQLite development team takes code testing and verification very seriously.

#### 2. The Architecture Of SQLite

![](http://soft-dev.org/pubs/html/bolz_kurilova_tratt__making_an_embedded_dbms_jit_friendly/sqlite-architecture.png)

SQLite is modular in design. See the [architectural description](http://www.sqlite.org/arch.html) for details. Other documents that are useful in (helping to understand how SQLite works include the [file format description](http://www.sqlite.org/fileformat2.html), the [virtual machine](http://www.sqlite.org/opcode.html) that runs prepared statements, the description of [how transactions work](http://www.sqlite.org/atomiccommit.html), and the [overview of the query planner](http://www.sqlite.org/optoverview.html).

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
