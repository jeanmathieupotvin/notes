# What is a bit

The fundamental unit of information in computer science. The name is a
contraction of the expression *binary digit*. A *bit* is a logical state
that has two possible values: either 0 or 1.

The unit that represents a bit is usually *bit* or *b*.

# What is a byte

Most commonly, an ordered sequence of 8 bits. Historically, a *byte* was
the number of bits used to encode a single character of text. For this
reason it is the smallest addressable unit of memory in many
architectures.

A byte is also composed by two nibbles. See dedicated section below.

Bit within a byte are usually labelled from 0 to 7, right to left. This
order is arbitrary, and a better way to label bits is from its MSB
(*Most Significant Bit*) to its LBS (*Least Significant Bit*).

      {1, 0}   {1, 0}   {1, 0}   {1, 0}   {1, 0}   {1, 0}   {1, 0}   {1, 0}
    |++++++++|++++++++|++++++++|++++++++|++++++++|++++++++|++++++++|++++++++|
      7 (MBS)    6        5        4        3        2        1      0 (LBS)
      MSB0       MSB1     MSB2     MSB3     MSB4     MSB5     MSB6   MSB7
      LSB7       LSB6     LSB5     LSB4     LSB3     LSB2     LSB1   LSB0

    |+++++++++++++++++++++++++++++++++++|+++++++++++++++++++++++++++++++++++|
                  Nibble 1                             Nibble 0                 

The unit that represents a byte is usually *B*.

## Size

The biggest byte is `11111111`, which is equal to `(2 ^ 8 - 1) = 255` in
decimal notation. Therefore, with one byte, you can represent any
integer in the set `[0, 255]`.

# What is a nibble

Simply, Half a byte. Most commonly, an ordered sequence of 4 bits. It
has many other names: semi-octet, semi-byte, nybble, quartet, etc.

      {1, 0}   {1, 0}   {1, 0}   {1, 0}
    |++++++++|++++++++|++++++++|++++++++|
      3 (MBS)    2        1      0 (LBS)

A nibble has no unit.

## Size

The biggest nibble is `1111`, which is equal to `(2 ^ 4 - 1) = 15` in
decimal notation. Therefore, with one nibble, you can represent any
integer in the set `[0, 15]`.

# What is an octet

An octet is an ordered group of 8 bits. This word is used to
disambiguate different implementation of the *byte* (that can be longer
or shorter than 8 bits. Bytes and octets are used as part of larger
collections / stream most of the time.

# Representing bits, nibbles and bytes

Hexadecimal numbers are numbers represented under base 16. It is similar
to other bases such as decimal (base 10) and binary (base 2). An
hexadecimal number is represented by *hexadecimal characters* taken from
the set `{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F }`. Letters
can be in upper case or in lower case, it does not matter.

We can map a single hexadecimal character to a decimal number and to a
nibble.

| Hexadecimal | Binary | Decimal |
|------------:|-------:|--------:|
|           0 |   0000 |       0 |
|           1 |   0001 |       1 |
|           2 |   0010 |       2 |
|           3 |   0011 |       3 |
|           4 |   0100 |       4 |
|           5 |   0101 |       5 |
|           6 |   0110 |       6 |
|           7 |   0111 |       7 |
|           8 |   1000 |       8 |
|           9 |   1001 |       9 |
|           A |   1010 |      10 |
|           B |   1011 |      11 |
|           C |   1100 |      12 |
|           D |   1101 |      13 |
|           E |   1110 |      14 |
|           F |   1111 |      15 |

Hexadecimal numbers are usually written as `0x<...>` or `<...>hex`.

    # Example.

    0xff = ( (0x0f + 0x1) ^ 0x1 ) * 0x0f + 0x0f,
         = ( (15   + 1  ) ^ 1   ) * 15   + 15,
         = ( 16 * 15 ) + 15,
         = 255.

## Using hexadecimal characters to represent bytes

A byte can be written as a sequence of 2 hexadecimal characters
(preceded by `0x`). Each character represents a nibble.

# Raw vectors in R

In R, a single `raw(1)` represents one byte written as two hexadecimal
characters and without the usual `0x` prefix. This notation is called
*packed 8 bits*. Therefore, when setting or replacing raw values, they
can only represent non-negative value lower than or equal to 255.

A single bit in R is always preceded by a `0` followed by the actual bit
value. Example: `01, 00`. Any NA value is converted to `00`, the nul
byte. Moreover, `ff = 0xff = 255` and `00 = 0x00 = 0`.

Functions to manipulate bytes and bits are (mostly) described in
`base::rawConversion`. **Beware! R orders bits and bytes from LSB to
MSB.**
