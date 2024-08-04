## Arikedb Variable

In Arikedb, **variables** are the root concept and the main unit where data is stored. An Arikedb variable has next metadata:
 - **name**: This property defines the name of the variable. It is a unique and human readable identifier in each collection ([See collections](./collection.md)). Any operation made over a variable will be referenced using its name.
 - **type**: Arikedb variables must have a well declared type. The variable type will be used to store values in memory using the amount of memory needed for it. Available types are:
   - **I8**: Integer numbers stored in 8 bits. The possible values are -2^7^ < x < 2^7^ - 1
   - **I16**: Integer numbers stored in 16 bits. The possible values are -32 768 < x < 32 767
   - **I32**: Integer numbers stored in 32 bits. The possible values are -2 147 483 648 < x < 2 147 483 647
   - **I64**: Integer numbers stored in 64 bits. The possible values are -9 223 372 036 854 776 000 < x < 127
   - **I128**: Integer numbers stored in 8 bits. The possible values are -128 < x < 127
   - **U8**: Integer numbers stored in 8 bits. The possible values are -128 < x < 127
   - **U16**: Integer numbers stored in 8 bits. The possible values are -128 < x < 127
   - **U32**: Integer numbers stored in 8 bits. The possible values are -128 < x < 127
   - **U64**: Integer numbers stored in 8 bits. The possible values are -128 < x < 127
   - **U128**: Integer numbers stored in 8 bits. The possible values are -128 < x < 127
   - F32
   - F64
   - STR
   - BOOL

[Back](../README.md)
