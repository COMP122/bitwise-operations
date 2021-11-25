# Bit-wise Operations

Practically every programming language provides a set of operators to manipulate binary values, Java is no exception.  When you program at the assembly level, you often use these operations to great advantage. That is to say, when you use the MIPS ISA, you will use these operators all the time.  Hence, understanding how these Java instructions work is key to programming at the assembly level.

In this exercise, you need to calculate the result of a number of Java assignment statements that utilize common bit-wise operations.  Understanding how these operations work is key to be be able to perform efficient operations at the assembly level.  Some simple examples include:

  1. to quickly multiple/divide by a power of two
     -  x * 4 == x << 2 
     -  x / 8 == x >> 3

  1. to separate a word into its individual bytes
     -  byte2 = (word >> 8) & 0x00F0 

  1. to determine if a particular bit is a one
     -  ( x & 8 ) != 0 : the fourth bit (from the right) is set

  1. to flip a single bit within a word
     -  x = x ^ 8  : the fourth bit (from the right) is flipped


### Signed Binary Representation
Recall that integers are encoded as a two's complement number. This encoding allows us to represent both positive and negative numbers.  To compute the two's complement of a number we first take's it one's complement and then add one.  Using 16-bit encoding, the values of 6 and -6 as follows:

   * 0000 0000 0000 0110 : 6  :
   * 1111 1111 1111 1001 :    : 1's complement of 6
   * 1111 1111 1111 1010 : -6 : 1's complement of 6 + 1 == 2's complement of 6 

### Java Bit-wise Complement (\~)
The Java bit-wise complement operator (\~) is used to compute the 1's complement of its operand.  E.g.,

   ```
   X = ~ 5
   ```
 The value of X is defined to be -6.  The following provides the 16-bit encoding of both the value of 5 and -6.

   - 5: 0000 0000 0000 0101
   - X: 1111 1111 1111 1010

For each of the following Java statements, provide:
   - the value of X
   - the 8-bit 2's complement encoding for the operand
   - the 8-bit complement of the operand

Use the first problem as an example on how to construct your answers.

  1. X = ~ 5 
     - X = -6                    <!-- answer -->
     - 5:   0000 0101            <!-- answer -->
     - \~5: 1111 1010            <!-- answer -->

  1. X = ~ 22 
     - X =                        <!-- answer -->
     - 22:                        <!-- answer -->
     -                            <!-- answer -->

  1. X = ~ -16 
     -                            <!-- answer -->
     -                            <!-- answer -->
     -                            <!-- answer -->
 
  1. X = ~ -12 
     -                            <!-- answer -->
     -                            <!-- answer -->
     -                            <!-- answer -->

   1. X = ~ 127 
     -                            <!-- answer -->
     -                            <!-- answer -->
     -                            <!-- answer -->
 
Hmm,   ~ X == - (X + 1) ?


### Java Shift Operators (<<, >>, >>>)
Java provides three operators to perform a bit-wise shift.  These operators are:

   | op  | Description          | MIPS: Description       | MIPS op |
   |-----|----------------------|-------------------------|---------|
   | <<  | Left Shift           | shift left logical      |   sll   |
   | >>  | Signed Right Shift   | shift right arithmetic  |   sra   |
   | >>> | Unsigned Right Shift | shift right logical     |   srl   |

In each of the following problems, you are provided with a Java statement that conforms to the following general pattern.

  * X = V << S  (sll X, V, S)
  * X = V >> S  (srl X, V, S)
  * X = V >>> S (sra X, V, S)

For each of these problems, provide the following information:

  1. the 8-bit 2's complement representation for V
  2. the 8-bit representation for X (i.e., V >> S)
  3. the 8-bit representation for \~X 
  3. the equivalent base 10 representation for X

Use the first problem as an example on how to construct your answers.

#### Left-Shift: 
1.  X = 5 << 2
  -   5: 0000 0101                 <!-- answer -->
  -   X: 0000 0001                 <!-- answer -->
  -  ~X: 1111 1110                 <!-- answer -->
  -   X= 1                         <!-- answer -->

1.  X = 4 << 3
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = 127 << 1
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = 1 << 7
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = -2 << 4
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->


#### Signed Shift-Right: Notice that the sign bit replicates itself

1.  X = -22 >> 2
  -  -22: 1110 1010                <!-- answer -->
  -   X:  1111 1010                <!-- answer -->
  -  ~X:  0000 0101                <!-- answer -->
  -   X=  -6                       <!-- answer -->

1.  X = 16 >> 4
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = 16 >> 2
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = 127 >> 6
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = -16 >> 2
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->


#### UnSigned Shift-Right: 

1.  X = -22 >>> 2
  -  -22: 1110 1010                <!-- answer -->
  -   X:  0011 1010                <!-- answer -->
  -  ~X:  1100 0101                <!-- answer -->
  -   X=  58                       <!-- answer -->

1.  X = 16 >>> 4
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = 16 >>> 2
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = -127 >>> 6
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

1.  X = -16 >>> 2
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->
  -                                <!-- answer -->

Hmm, as compared to the >> operator, only negative numbers work differently!

### Java Bit-wise Boolean operations
Java provides three operators to perform a bit-wise Boolean manipulations.  These operators are:

   | op  | Description          | MIPS op |
   |-----|----------------------|---------|
   |  &  | Bit-wise And          |   and   |
   |  |  | Bit-wise Or           |   or    |
   |  ^  | Bit-wise Xor          |   xor   |

In each of the following problems, you are provided with a Java statement that conforms to the following general pattern.

  *  X = A & B

For each of these problems, provide the following information:

  1. the 16-bit representation for A and B
  2. the 16-bit representation for X 

Use the first problem as an example on how to construct your answers.

1.  X = 0x4152 & 0xF0
  -  0x4512:  0100 0001 0101 0010       <!-- answer -->
  -  0x00F0:  0000 0000 1111 0000       <!-- answer -->
  -       X:  0000 0000 0101 0000       <!-- answer --> 

1. X = 0x4152 & 0xF00   
  -                                     <!-- answer -->
  -                                     <!-- answer -->
  -                                     <!-- answer -->

1. X = 0x4152 \| 0xAAA
  -                                     <!-- answer -->
  -                                     <!-- answer -->
  -                                     <!-- answer -->

1. X = 0640 \| 0137
  -                                     <!-- answer -->
  -                                     <!-- answer -->
  -                                     <!-- answer -->

1. X = 0x4152 ^ 0xF0
  -                                     <!-- answer -->        
  -                                     <!-- answer -->
  -                                     <!-- answer -->

1. X = 0x4152 ^ 0xAAAA
  -                                     <!-- answer -->
  -                                     <!-- answer -->
  -                                     <!-- answer -->

