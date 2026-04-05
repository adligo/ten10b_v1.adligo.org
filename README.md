# Text Encoded Base 10 Numbers (Ten10b)

# Abstract

Text Encoded Base 10 Numbers (Ten10b), is a [positional number system](#positional-number-systems-wikipedia) designed to be encoded in [UTF-8](#utf-8-rfc-3629) text, based on the system you likely learned in elementary school and used throughout your mathematics courses.  It is a [discrete system](#discrete-system-wikipedia) designed to provide the maximum clarity for the serialization of numbers (which fit on a single line of text) across the internet.  Although the numbers encoded by the Ten10b system MAY represent a point on a continuous curve (aka an [integral](#integral-wikipedia) or simply [analog](#analog-wikipedia)), the text itself is a [discreet system](#discrete-system-wikipedia).  In addition, it should be noted that since all [binary number systems](#binary-number-systems-wikipedia) are discrete, by proxy all number systems built on top of them are by proxy [discrete number systems](#discrete-system-wikipedia).  This includes [floating point numbers](#ieee-754) which MAY introduce rounding issues.

Ten10b codifies five types of numbers which MAY be represented in text [integers](#integers), [integer fractions](#integer-fractions), [integer loops](#integer-loops), [decimals](#decimals), and [decimal loops](#decimal-loops).  Ten10b Allows for numbers to be of any size, any number of characters.  However, since Ten10b numbers MUST be parsable from a single line of text, [line wrapping](#line-wrapping-wikipedia) SHOULD NOT be used with Ten10b.  To improve human-readability, we suggest using [Ten64](#ten64) for numbers that do NOT fit on a single line.

# Introduction




## Natural Number Alphabet

| [UTF-8 Character](#utf-8-rfc-3629) |
|------------------------------------|
| 0                                  |
| 1                                  |
| 2                                  |
| 3                                  |
| 4                                  |
| 5                                  |
| 6                                  |
| 7                                  |
| 8                                  |
| 9                                  |

## Ten10b Alphabet

| [UTF-8 Character](#utf-8-rfc-3629)           |
|----------------------------------------------|
| 0                                            |
| 1                                            |
| 2                                            |
| 3                                            |
| 4                                            |
| 5                                            |
| 6                                            |
| 7                                            |
| 8                                            |
| 9                                            |
| -                                            |
| +                                            |
| .                                            |
| ,                                            |
| /                                            |
| [u0305 / Compart (aka. Overline) ](#compart) |


# The Five Number Types

### Integers

Integers are built in the [Modern Western Numeral System](#modern-western-numeral-system) and are well-known and have many identical definitions, [i.e. Wikipedia](#integers-wikipedia).  Integers are arranged in descending order ([aka. little ending](#endianness-wikipedia)).  Integers MUST
consist of only the [Natural Numbers](#natural-number-alphabet).  Integers MUST NOT have one or more zeros on their left side.  Integers MAY contain commas between characters in the [Natural Number Alphabet](#natural-number-alphabet).

### Integer Fractions

Integer Fractions consist of a single [numerator](#fractions-wikipedia) and [denominator](#fractions-wikipedia) separated by the fracton symbol '/'.  Both the [numerator](#fractions-wikipedia) and [denominator](#fractions-wikipedia) MUST consist of [Ten10b Integers](#integers).  Integer Fractions MUST contain one and only one fracton symbol '/'.  The fracton symbol MUST NOT be the first or last character in a Integer Fraction character sequence.

### Integer Loops

Integer Loops consist of one or more characters from the [Natural Number Alphabet](#natural-number-alphabet).  All numbers in an Integer Loop MUST have a [Compart (aka. Overline)](#compart).  Integer Loops MAY have one or more zeros at the left. Integer Loops MAY contain commas between characters in the [Natural Number Alphabet](#natural-number-alphabet).

### Decimals

Decimals consist of one or more characters from the [Natural Number Alphabet](#natural-number-alphabet) separated by a decimal point.  Decimals MUST have one and only one decimal point.  The text to the left side of the decimal point is called the integer part and MUST conform to the [Integer Ten10b rules](#integers).  The text to the right side of the decimal point is called the decimal part and MAY have commas as well as trailing zeros.  The purpose of the trailing zeros is to communicate precision.

### Decimal Loops

Decimal Loops consist of a [Ten10b style Decimal](#decimals) followed by a [Ten10b style Integer Loop](#integer-loops).  Like all Ten10b number sequences, Decimal Loops MUST NOT contain any whitespace characters.

# Implementation Requirements

# Implementation Recommendations


# Commentary

[@see Ten64 Commentary](#ten64-commentary)

## Citation Commentary

Find or create Academic/Footnote Markdown style and RFC XML style citations to


# Citations

##### Analog Wikipedia

Wikipedia contributors. "Analog device." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Analog_device>.

##### Binary Number Systems Wikipedia

Wikipedia contributors. "Binary number." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Binary_number>.

##### Compart

Compart. "Unicode Character “̅” (U+0305)." *Compart*. Accessed April 5, 2026. <https://www.compart.com/en/unicode/U+0305>.

##### Decimals Wikipedia

Wikipedia contributors. "Decimal." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Decimal>.

##### Discrete System Wikipedia

Wikipedia contributors. "Discrete system." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Discrete_system>.

##### Endianness Wikipedia

Wikipedia contributors. "Endianness." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Endianness>.

##### Fractions Wikipedia

Wikipedia contributors. "Fraction." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Fraction>.

##### IEEE 754

Wikipedia contributors. "IEEE 754." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/IEEE_754>.

##### Integers Wikipedia

Wikipedia contributors. "Integer." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Integer>.

##### Integral Wikipedia

Wikipedia contributors. "Integral." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Integral>.

##### Line Wrapping Wikipedia

Wikipedia contributors. "Wrapping (text)." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Wrapping_(text)>.

##### Modern Western Numeral System

Morgan, S. "Modern Western Numeral System." In *Text Encoded Base 64 Numbers (Ten64)*. Internet-Draft draft-morgan-ten64-00, April 1, 2026. <https://www.ietf.org/archive/id/draft-morgan-ten64-00.html#modern-western-numeral-system>.

##### Positional Number Systems Wikipedia

Wikipedia contributors. "Positional notation." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Positional_notation>.

##### Ten64

Morgan, S. "Text Encoded Base 64 Numbers (Ten64)." Internet-Draft draft-morgan-ten64-00, April 1, 2026. <https://www.ietf.org/archive/id/draft-morgan-ten64-00.html>.

##### Ten64 Commentary

Morgan, S. "Commentary." In *Text Encoded Base 64 Numbers (Ten64)*. Internet-Draft draft-morgan-ten64-00, April 1, 2026. <https://www.ietf.org/archive/id/draft-morgan-ten64-00.html#commentary>.

##### UTF-8 RFC 3629

Yergeau, F. "UTF-8, a transformation format of ISO 10646." RFC 3629, STD 63, November 2003. <https://www.rfc-editor.org/info/rfc3629>.
