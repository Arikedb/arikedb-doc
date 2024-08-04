## Arikedb Variable

In Arikedb, **variables** are the root concept and the main unit where data is stored. An Arikedb variable has next metadata:

 - **name**: This property defines the name of the variable. It is a unique and human readable identifier in each collection ([See collections](./collection.md)). Any operation made over a variable will be referenced using its name.
 - **type**: Arikedb variables must have a well declared type. The variable type will be used to store values in memory using the amount of memory needed for it. Available types are:
   - **I8**: Integer numbers stored in 8 bits. The possible values are -2^7 <= x <= 2^7 - 1
   - **I16**: Integer numbers stored in 16 bits. The possible values are -2^15 <= x <= 2^15 - 1
   - **I32**: Integer numbers stored in 32 bits. The possible values are -2^31 <= x <= 2^31 - 1
   - **I64**: Integer numbers stored in 64 bits. The possible values are -2^63 <= x <= 2^63 - 1
   - **I128**: Integer numbers stored in 128 bits. The possible values are -2^127 <= x <= 2^127 - 1
   - **U8**: Natural numbers (positive integers) stored in 8 bits. The possible values are 0 <= x <= 2^8 - 1
   - **U16**: Natural numbers (positive integers) stored in 8 bits. The possible values are 0 <= x <= 2^16 - 1
   - **U32**: Natural numbers (positive integers) stored in 8 bits. The possible values are 0 <= x <= 2^32 - 1
   - **U64**: Natural numbers (positive integers) stored in 8 bits. The possible values are 0 <= x <= 2^64 - 1
   - **U128**: Natural numbers (positive integers) stored in 8 bits. The possible values are 0 <= x <= 2^128 - 1
   - **F32**: Float number based on IEEE 754-2008 "binary32"
   - **F64**: Float number based on IEEE 754-2008 "binary64"
   - **STR**: String conformed by UTF-8 characters
   - **BOOL**: Boolean value. The possible values are true and false
 - **buffer**: Arikedb is a real-time database and any time you request a variable, the returned value will always be the current one, it means the last value given for any connected client. However, arikedb allows you to query variable derivative, providing the derivative order you want to consult. For example, if you want to know the rate a variable value is changing over time, you can ask for that variable with a derivative order = 1. In order to calculate derivatives, arikedb variables store a windowed set of the latest historical values. For example, to get the derivative of order 1, arikedb needs the latest 2 values with their timestamps; to calculate the derivative of order 3, it needs latest 4 values and so on. The buffer size you define for variables will stablish how many historical values will be stored, use that buffer size taking into account two factors:
   - Bigger buffers means more data stored and more memory usage
   - Buffer size defines the limit of derivative order you will be able to query from a variable 

[Back](../README.md)
