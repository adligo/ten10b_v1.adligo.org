# Text Encoded Base 10 Numbers (Ten10b)

# Abstract

Text Encoded Base 10 Numbers (Ten10b), are a [positional number system](#positional-number-systems-wikipedia) designed to be encoded in [UTF-8](#utf-8-rfc-3629) text, based on the system you likely learned in elementary school and used throughout your mathematics courses.  It is a [discrete system](#discrete-system-wikipedia) designed to provide the maximum clarity for the serialization of numbers (which fit on a single line of text) across the internet.  Although the numbers encoded by the Ten10b system MAY represent a point on a continuous curve (aka an [integral](#integral-wikipedia) or simply [analog](#analog-wikipedia)), the text itself is a [discreet system](#discrete-system-wikipedia).  In addition, it SHOULD be noted that since all [binary number systems](#binary-number-systems-wikipedia) are discrete, by proxy all number systems built on top of them are by proxy [discrete number systems](#discrete-system-wikipedia).  This includes [floating point numbers](#ieee-754) which MAY introduce rounding issues when printed or converted to other [positional number systems](#positional-number-systems-wikipedia).

Ten10b codifies five types of numbers which MAY be represented with [UTF-8 text](#utf-8-rfc-3629) as follows [Integers](#integers), [Integer Fractions](#integer-fractions), [Integer Loops](#integer-loops), [Decimals](#decimals), and [Decimal Loops (aka. Repeating Decimals)](#decimal-loops).  Ten10b allows for numbers to be of any size, any number of characters.  However, since Ten10b numbers MUST be parsable from a single line of text, [line wrapping](#line-wrapping-wikipedia) SHOULD NOT be used with Ten10b.  To improve human-readability, we suggest using [Ten64](#ten64) for numbers that do NOT fit on a single line.  Finally, Ten10b users SHOULD use a 92 character per line and character limiter.

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

| [UTF-8 Character](#utf-8-rfc-3629)                   |
|------------------------------------------------------|
| 0                                                    |
| 1                                                    |
| 2                                                    |
| 3                                                    |
| 4                                                    |
| 5                                                    |
| 6                                                    |
| 7                                                    |
| 8                                                    |
| 9                                                    |
| -                                                    |
| +                                                    |
| .                                                    |
| ,                                                    |
| /                                                    |
| [u0305 / Compart (aka. Overline [i.e. &#x0305;1&#x0305;2&#x0305;3]) ](#compart) |


# The Five Number Types

Any of the five number types MAY have a sign prefix which is optional.  The sign prefix MAY be either positive '+' or negative '-'.  When the sign prefix is present, it MUST be the first character of the Ten10b character sequence.

### Integers

Integers are built with the [Modern Western Numeral System](#modern-western-numeral-system) and are well-known and have many identical definitions, [i.e. Wikipedia](#integers-wikipedia).  Integers are arranged in descending order ([aka. little ending](#endianness-wikipedia)).  Integers MUST
consist of only the [Natural Numbers](#natural-number-alphabet).  Integers MUST NOT have one or more zeros on their left side.  Integers MAY contain commas between characters in the [Natural Number Alphabet](#natural-number-alphabet).

###### Example A

```
1,234
```

### Integer Fractions

Integer Fractions consist of a single [numerator](#fractions-wikipedia) and [denominator](#fractions-wikipedia) separated by the fracton symbol '/'.  Both the [numerator](#fractions-wikipedia) and [denominator](#fractions-wikipedia) MUST consist of [Ten10b Integers](#integers).  Integer Fractions MUST contain one and only one fracton symbol '/'.  The fracton symbol MUST NOT be the first or last character in a Integer Fraction character sequence.

###### Example B

```
1,234/2,345
```

### Integer Loops

Integer Loops consist of one or more characters from the [Natural Number Alphabet](#natural-number-alphabet).  All characters in an Integer Loop MUST have a [Compart (aka. Overline)](#compart) (Note this includes commas, in addition to the characters from the [Natural Numbers Alphabet](#natural-number-alphabet)).  Integer Loops MAY have one or more zeros at the left. Integer Loops MAY contain commas between characters in the [Natural Number Alphabet](#natural-number-alphabet).

###### Example C

&#x0305;0&#x0305;1&#x0305;2&#x0305;,&#x0305;3

### Decimals

Decimals consist of one or more characters from the [Natural Number Alphabet](#natural-number-alphabet) separated by a [decimal point](#decimals).  Decimals MUST have one and only one [decimal point](#decimals-wikipedia).  Decimals MUST NOT contain a fraction symbol '/'.  The text to the left side of the decimal point is called the integer part and MUST conform to the [Integer Ten10b rules](#integers).  The text to the right side of the decimal point is called the decimal part and MAY have commas as well as trailing zeros (aka. zeros at the right side of the Ten10b character sequence).  The purpose of the trailing zeros is to communicate precision.

###### Example D

```
123.456,678,000
```

### Decimal Loops

Decimal Loops consist of a [Ten10b style Decimal](#decimals) followed by a [Ten10b style Integer Loop](#integer-loops).  Like all Ten10b number sequences, Decimal Loops MUST NOT contain any whitespace characters.  Note, although not a hard limit for [single precision and double precision floating-point numbers](#ieee-754), generally there is a respective [9 and 17 rule provided by C++](#decimal-conversion-c).  However, since floating-point precision MAY increase or vary over time, modern standards SHOULD be sought for conversion algorithms.

##### Example F

123,456.123,34&#x0305;2&#x0305;,&#x0305;3
## Commas and Comma Scheme Conventions

Ten10b SHOULD use commas at the time of encoding to improve human-readability.  However, the use of commas is optional.  Also note, parsers/readers MAY simply ignore commas.  Commas MUST NOT be the first or last character in a Ten10b character sequence.

##### The Three-Digit Comma Sequence Convention

This convention is simply to place a comma after every three additional numeric digits away from the decimal point.  This convention is commonly used in large integers for currency, for example.  However, this convention should be extended to decimal places when using Ten10b.

i.e.

```
123,456,789.123,456,789,012
```
##### The Ten 5-1 Comma Sequence Convention

This convention is for larger numbers where it would help to identify every 25 decimal places.  Similar to the three-digit convention, we start at the decimal place and then move away. Adding commas in the following sequence;

```
after ten digits
after five digits
after four digits
after three digits
after two digits
after one digit
```

i.e.

```
7654,09876,1235467890.1234567890,09876,5432,321,21,1,1234567890,09
```

# Implementation Requirements

Ten10b implementations MUST guarantee exact equality of number being encoded and transmitted over the internet!

# Implementation Recommendations

Because of the [implementation requirements](#implementation-requirements) we recommend creating a one-to-one type system in the languages of your choice to convey this information.  Essentially, these recommended classes would act as an intermediary between the language's type system and the readers and writers of Ten10b.  In addition, noting the capital T at the start of the class names is short for Ten10b, we recommend the following class names.

## Class Diagram


### TNumber

This is the abstract class with static factory methods named <i><b>from*</b></i> (pronounced from star).  The <i><b>from*</b></i> methods MAY be overloaded or MAY have extension methods depending on if your language allows method overloading.

i.e. [Java](#java) Psudocode

```
String s = TNumber.from((float) 10.19).toString();
TNumber t = TNumber.from("10.19");
println(t.getType()); // Prints TDecimal
float f = ((TDecimal) t).toFloat();
BigDecimal b = ((TDecimal) t).toBigDecimal();
```

i.e. [Typescript / ECMA Script](#typescript) Psudocode

```
let s : string = TNumber.fromNumber(10.19).toString();
let t : TDecimal = TNumber.fromBigDecimal(new BigDecimal("10.19");
number n = t.toNumber(); // IEEE 754 per the ECMA Script standard
```

### TInt

This is the representation of [Ten10b Integers](#integers).  It SHOULD extend T number, when extension is available.  It SHOULD provide various methods <i><b>to*</b></i> (pronounced to star) which convert the TInt into the local language's class or type system.

It MUST return false from the <i><b>isDecimalOrFraction</b></i> method.  It MUST return false to the <i><b>isDecimal</b></i> method.  It MUST return false from the <i><b>isFraction</b></i> method.

It MUST return false from the <i><b>isLoop</b></i> method.  It MAY provide a true or false answer to the <i><b>isBig</b></i> method.  When the <i><b>isBig</b></i> method returns false, it MUST throw an exception or error when the <i><b>toBigInt</b></i> is called.


### TFraction

TFraction is the representation of a [Ten10b Integer Fraction](#integer-fractions).  It MUST return a TInt result for the <i><b>getNumerator</b></i> and <i><b>getDenominator</b></i> methods.  It MUST return true if either the numerator or denominator returns true for the <i><b>isBig<b></i> method.

It MUST return true from the isDecimalOrFraction method.  It MUST return false from the <i><b>isDecimal</b></i> method.  It MUST return true from the <i><b>isFraction</b></i> method.  It MUST return false from the <i><b>isLoop</b></i> method.



### TIntLoop

TFraction is the representation of a [Ten10b Integer Loop](#integer-fractions).
It MUST return the next digit when the <i><b>next</b></i> method is called.

It MUST return false from the isDecimalOrFraction method.  It MUST return false from the <i><b>isDecimal</b></i> method.  It MUST return true from the <i><b>isFraction</b></i> method.  It MUST return true from the <i><b>isLoop</b></i> method.


### TDecimal

TFraction is the representation of a [Ten10b Decimal](#decimals).  It MAY return either true or false from the <i><b>isBig</b></i> method, and SHOULD base this decision around the semantics of the libraries in the language it is implemented in.

TDecimals MUST be implemented using a BigInteger type (i.e. [BigInt](#ecma-script), [BigInteger](#java-language-specification)) for the numeric part (integer and decimal parts), which conforms to [ISO/IEC 10967 integer datatype section 5.1 / International Math Standard.](#math-international-standard).  TDecimals MUST also be implemented using a 2nd BigInteger type (i.e. [BigInt](#ecma-script), [BigInteger](#java-language-specification)) to track the number of [(base/radix 10) decimal places](#base-10), which conforms to [ISO/IEC 10967 integer datatype section 5.1 / International Math Standard.](#math-international-standard).

It MUST return true from the <i><b>isDecimalOrFraction</b></i> method.  It MUST return true from the <i><b>isDecimal</b></i> method.  It MUST return false from the <i><b>isFraction</b></i> method.  It MUST return false from the <i><b>isLoop</b></i> method.

### TDecimalLoop

TFraction is the representation of a [Ten10b Decimal Loops](#decimal-loops).
The <i><b>to* (pronounced to star)</b></i> methods will have implementation algorithms based on the language implementation details.

It MUST return true from the <i><b>isDecimalOrFraction</b></i> method.  It MUST return true from the <i><b>isDecimal</b></i> method.  It MUST return false from the <i><b>isFraction</b></i> method.  It MUST return true from the <i><b>isLoop</b></i> method.

# Compatibility

### JSON

[JSON](#json-rfc-8259) is based on UTF-8 and by proxy, Ten10b is compatible with [JSON](#json-rfc-8259) strings.

### [XCN](#xcn-github)

Extensible (eXtensible) Classification System is a downstream client and will be compatible by default.

### XML

[XML](#xml-wc3) MAY be based on UTF-8, when it is Ten10b compatible with XML strings.  [XML](#xml-wc3) with non UTF-8 character encodings is NOT compatible with Ten10b.

# Commentary

[@see Ten64 Commentary](#ten64-commentary)

## The Ten10b Acronym

S Morgan:

In an attempt to improve human audibility, I added a small b at the end of the acronym.  It seemed to have a nice ring to it, like two 21B.

## Citation Commentary

Find or create Academic/Footnote Markdown style and RFC XML style citations to


# Citations

##### Analog Wikipedia

Wikipedia contributors. "Analog device." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Analog_device>.

##### Base 10

Computers must frequently translate between binary data and human-readable base-10 (decimal) positional number systems.

Knuth, Donald E. *The Art of Computer Programming, Volume 2: Seminumerical Algorithms*. 3rd ed., Addison-Wesley, 1997, pp. 195. (Section 4.1: Positional Number Systems).


##### Binary Number Systems Wikipedia

Wikipedia contributors. "Binary number." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Binary_number>.

##### Compart

Compart. "Unicode Character “̅” (U+0305)." *Compart*. Accessed April 5, 2026. <https://www.compart.com/en/unicode/U+0305>.

##### Decimal Conversion C++

The C++ standard library provides a specific constant for this exact round-trip serialization guarantee called `max_digits10`.[^1]

[^1]: "std::numeric_limits\<T\>::max_digits10." *cppreference.com*, https://en.cppreference.com/w/cpp/types/numeric_limits/max_digits10. Accessed 5 Apr. 2026.

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

##### Java Language Specification

Gosling, J., Joy, B., Steele, G., Bracha, G., Buckley, A., Smith, D., and Bierman, G. *The Java® Language Specification, Java SE 21 Edition*. Oracle America, Inc., September 2023. Accessed April 5, 2026. <https://docs.oracle.com/javase/specs/jls/se21/html/index.html>.

##### JSON RFC 8259

Many modern APIs use the JSON data interchange format.

Bray, Tim, editor. "The JavaScript Object Notation (JSON) Data Interchange Format." *Internet Engineering Task Force (IETF)*, RFC 8259, Dec. 2017. https://doi.org/10.17487/RFC8259. Accessed 5 Apr. 2026.

##### Line Wrapping Wikipedia

Wikipedia contributors. "Wrapping (text)." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Wrapping_(text)>.

##### Math International Standard

*Information technology — Language independent arithmetic — Part 1: Integer and floating point arithmetic*, ISO/IEC 10967-1:2012, Jul. 2012.

##### Modern Western Numeral System

Morgan, S. "Modern Western Numeral System." In *Text Encoded Base 64 Numbers (Ten64)*. Internet-Draft draft-morgan-ten64-00, April 1, 2026. <https://www.ietf.org/archive/id/draft-morgan-ten64-00.html#modern-western-numeral-system>.

##### Positional Number Systems Wikipedia

Wikipedia contributors. "Positional notation." *Wikipedia, The Free Encyclopedia*. Accessed April 5, 2026. <https://en.wikipedia.org/wiki/Positional_notation>.

##### Ten64

Morgan, S. "Text Encoded Base 64 Numbers (Ten64)." Internet-Draft draft-morgan-ten64-00, April 1, 2026. <https://www.ietf.org/archive/id/draft-morgan-ten64-00.html>.

##### Ten64 Commentary

Morgan, S. "Commentary." In *Text Encoded Base 64 Numbers (Ten64)*. Internet-Draft draft-morgan-ten64-00, April 1, 2026. <https://www.ietf.org/archive/id/draft-morgan-ten64-00.html#commentary>.

##### TypeScript

Microsoft. "TypeScript: Typed JavaScript at Any Scale." Accessed April 5, 2026. <https://www.typescriptlang.org/>.

##### UTF-8 RFC 3629

Yergeau, F. "UTF-8, a transformation format of ISO 10646." RFC 3629, STD 63, November 2003. <https://www.rfc-editor.org/info/rfc3629>.

The document must be structured according to the W3C XML specification.[^1]

##### XML WC3

Bray, Tim, et al., editors. "Extensible Markup Language (XML) 1.0 (Fifth Edition)." *World Wide Web Consortium (W3C)*, 26 Nov. 2008. https://www.w3.org/TR/xml/. Accessed 5 Apr. 2026.
