# A-simple-DBMS
Data stored in DSDB system
We have provided the data to be stored in the DSDB along with this project. The data is pertaining to
the leading causes of deaths in different states of USA. Each tuple (or entry) in data comprises of the
following fields.
• ID (This field is unique for every row/record/tuple within data)
• Year
• Cause name
• State
• Deaths
• Age-adjusted death rate
Any one of the above fields can be used for creating the index.
Index Trees
DSDB must support B-tree, AVL tree and Red-Black tree -based indexing methods on the data. For
more detailed information about the working of Red-Black trees, students are recommended to read
pages 566 to 576 (i.e., section 12.2.) from the reference book “Data Structures and Algorithm Analysis

in C++” by Mark Allen Weiss (edition 4). The book also contains the C++ code for implementing Red-
Black tree, however, exact copy will be considered plagiarism.

For all trees, the root node will always reside in the heap (i.e., RAM). However, all other nodes will be
stored on the file system in separate files. In the Figure below, if the data with key 11 is searched, the
DSDB system will open the file D:\BInID\node2 and load the node data to proceed further with the
search. Similarly, if data with key 10 is searched, the DSDB will open the file D:\data\file1 and read
the required tuple from line 24.
Most importantly, all the files related to a tree index must be stored in a separate directory. For
example, in case B tree index is created on the data field “ID”, DSDB system will store the file related
to each node in the directory BInID (as shown in the Figure above). Likewise, if AVL tree index is
created on the data field “state” a directory with the name AVLState is used. Students can use their
own convention to name the directories, but a separate directory must exist for each index.
Indexing with duplicates
Indexing on data fields other than “ID” may result in duplicates, i.e., same key may point to multiple
tuples (or entries) in the data. The duplicates must be handled in the following manner.
There must be only one entry for each key in both B, AVL and Red-Black trees (even if key is pointing
to multiple tuples in the data). However, each key maintains the information about the file names and
line numbers of all relevant entries (i.e., entries with the same key).
When the node is loaded in the heap (i.e., RAM), a linked list (associated with each key) is created to
store the file names and line numbers of duplicate entries 
Operations supported by DSDB

• Create index: The user should be able to specify the following parameters:
o B tree index or AVL tree index or Red-Black tree index (at same time multiple indices can
reside).
o Order of B tree (i.e., value of m), in case B tree index is created.
o On which data field to perform indexing.
• Point search: The user can specify the key and DSDB system should be able to display the
corresponding tuple(s) from the data. For example, in case the indexing is performed on data field
“state” and user specifies “Michigan” as a key, the DSDB system returns all the data tuples
containing Michigan.
• Range search: The user can specify a range of key values and DSDB system should be able to
display all the relevant tuples.
• Update key, field, old value, new value: The user can specify the key, name of the field to be
modified along with its old value and new value. The DSDB system should be able to find the
tuple with the given key and change the value of the field to new value. For example, in case user
specifies: Update 5105, state Maryland, Michigan, the DSDB system will find the tuple with ID
5105 and change the state from Maryland to Michigan.
In case multiple tuples exist with the same key, the old value is used to break the ties. If old value
is insufficient to break the tie an error is displayed by the DSDB system.

• Delete key: In this case, DSDB system will delete all the tuples with the given key.
Additionally, the DSDB system should be able to display the performance of each operation in terms
of number of disk I/O operations performed.
