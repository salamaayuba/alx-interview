0x04. UTF-8 Validation

UTF-8 is a variable-length character encoding standard used for electronic communication. Defined by the Unicode Standard, the name is derived from Unicode (or Universal Coded Character Set) Transformation Format – 8-bit.[1]

UTF-8 is capable of encoding all 1,112,064[a] valid character code points in Unicode using one to four one-byte (8-bit) code units. Code points with lower numerical values, which tend to occur more frequently, are encoded using fewer bytes. It was designed for backward compatibility with ASCII: the first 128 characters of Unicode, which correspond one-to-one with ASCII, are encoded using a single byte with the same binary value as ASCII, so that valid ASCII text is valid UTF-8-encoded Unicode as well.

UTF-8 was designed as a superior alternative to UTF-1, a proposed variable-length encoding with partial ASCII compatibility which lacked some features including self-synchronization and fully ASCII-compatible handling of characters such as slashes. Ken Thompson and Rob Pike produced the first implementation for the Plan 9 operating system in September 1992.[2][3] This led to its adoption by X/Open as its specification for FSS-UTF,[4] which would first be officially presented at USENIX in January 1993[5] and subsequently adopted by the Internet Engineering Task Force (IETF) in RFC 2277 (BCP 18)[6] for future internet standards work, replacing Single Byte Character Sets such as Latin-1 in older RFCs.

UTF-8 results in fewer internationalization issues[7][8] than any alternative text encoding, and it has been implemented in all modern operating systems, including Microsoft Windows, and standards such as JSON, where, as is increasingly the case, it is the only allowed form of Unicode.

UTF-8 is the dominant encoding for the World Wide Web (and internet technologies), accounting for 98.0% of all web pages, 99.0% of the top 10,000 pages, and up to 100% for many languages, as of 2023.[9] Virtually all countries and languages have 95% or more use of UTF-8 encodings on the web.

Naming
The official name for the encoding is UTF-8, the spelling used in all Unicode Consortium documents. Most standards officially list it in upper case as well, but all that do are also case-insensitive and utf-8 is often used in code.[citation needed]

Some other spellings may also be accepted by standards, e.g. web standards (which include CSS, HTML, XML, and HTTP headers) explicitly allow utf8 (and disallow "unicode") and many aliases for encodings.[10] Spellings with a space e.g. "UTF 8" should not be used. The official Internet Assigned Numbers Authority also lists csUTF8 as the only alias,[11] which is rarely used.

In Windows, UTF-8 is codepage 65001[12] (i.e. CP_UTF8 in source code).

In MySQL, UTF-8 is called utf8mb4[13] (with utf8mb3, and its alias utf8, being a subset encoding for characters in the Basic Multilingual Plane[14]). In HP PCL, the Symbol-ID for UTF-8 is 18N.[15]

In Oracle Database (since version 9.0), AL32UTF8[16] means UTF-8. See also CESU-8 for an almost synonym with UTF-8 that rarely should be used.

UTF-8-BOM and UTF-8-NOBOM are sometimes used for text files which contain or do not contain a byte order mark (BOM), respectively.[citation needed] In Japan especially, UTF-8 encoding without a BOM is sometimes called UTF-8N.[17][18]

Encoding
UTF-8 encodes code points in one to four bytes, depending on the value of the code point. In the following table, the x characters are replaced by the bits of the code point:

Code point ↔ UTF-8 conversion
First code point	Last code point	Byte 1	Byte 2	Byte 3	Byte 4
U+0000	U+007F	0xxxxxxx	
U+0080	U+07FF	110xxxxx	10xxxxxx	
U+0800	U+FFFF	1110xxxx	10xxxxxx	10xxxxxx	
U+10000	[b]U+10FFFF	11110xxx	10xxxxxx	10xxxxxx	10xxxxxx
The first 128 code points (ASCII) need one byte. The next 1,920 code points need two bytes to encode, which covers the remainder of almost all Latin-script alphabets, and also IPA extensions, Greek, Cyrillic, Coptic, Armenian, Hebrew, Arabic, Syriac, Thaana and N'Ko alphabets, as well as Combining Diacritical Marks. Three bytes are needed for the remaining 61,440 code points of the Basic Multilingual Plane (BMP), including most Chinese, Japanese and Korean characters. Four bytes are needed for the 1,048,576 code points in the other planes of Unicode, which include emoji (pictographic symbols), less common CJK characters, various historic scripts, and mathematical symbols.

A "character" can take more than 4 bytes because it is made of more than one code point. For instance a national flag character takes 8 bytes since it is "constructed from a pair of Unicode scalar values" both from outside the BMP.[19][c]

Encoding process
In these examples, red, green, and blue digits indicate how bits from the code point are distributed among the UTF-8 bytes. Additional bits added by the UTF-8 encoding process are shown in black.

The Unicode code point for the euro sign € is U+20AC.
As this code point lies between U+0800 and U+FFFF, this will take three bytes to encode.
Hexadecimal 20AC is binary 0010 0000 1010 1100. The two leading zeros are added because a three-byte encoding needs exactly sixteen bits from the code point.
Because the encoding will be three bytes long, its leading byte starts with three 1s, then a 0 (1110...)
The four most significant bits of the code point are stored in the remaining low order four bits of this byte (11100010), leaving 12 bits of the code point yet to be encoded (...0000 1010 1100).
All continuation bytes contain exactly six bits from the code point. So the next six bits of the code point are stored in the low order six bits of the next byte, and 10 is stored in the high order two bits to mark it as a continuation byte (so 10000010).
Finally the last six bits of the code point are stored in the low order six bits of the final byte, and again 10 is stored in the high order two bits (10101100).
The three bytes 11100010 10000010 10101100 can be more concisely written in hexadecimal, as E2 82 AC.

The following table summarizes this conversion, as well as others with different lengths in UTF-8.

UTF-8 encoding process
Character	Binary code point	Binary UTF-8	Hex UTF-8
$	U+0024	010 0100	00100100	24
£	U+00A3	000 1010 0011	11000010 10100011	C2 A3
И	U+0418	100 0001 1000	11010000 10011000	D0 98
ह	U+0939	0000 1001 0011 1001	11100000 10100100 10111001	E0 A4 B9
€	U+20AC	0010 0000 1010 1100	11100010 10000010 10101100	E2 82 AC
한	U+D55C	1101 0101 0101 1100	11101101 10010101 10011100	ED 95 9C
𐍈	U+10348	0 0001 0000 0011 0100 1000	11110000 10010000 10001101 10001000	F0 90 8D 88
Example
In these examples, colored digits indicate multi-byte sequences used to encode characters beyond ASCII, while digits in black are ASCII.

As an example, the Vietnamese phrase Mình nói tiếng Việt (𨉟呐㗂越, "I speak Vietnamese") is encoded as follows:

Character	M	ì	n	h		n	ó	i		t	i	ế	n	g		V	i	ệ	t
Code point	4D	EC	6E	68	20	6E	F3	69	20	74	69	1EBF	6E	67	20	56	69	1EC7	74
Hex UTF-8	C3	AC	C3	B3	E1	BA	BF	E1	BB	87
Character	𨉟	呐	㗂	越
Code point	2825F	5450	35C2	8D8A
Hex UTF-8	F0	A8	89	9F	E5	91	90	E3	97	82	E8	B6	8A
Codepage layout
The following table summarizes usage of UTF-8 code units (individual bytes or octets) in a code page format. The upper half is for bytes used only in single-byte codes, so it looks like a normal code page; the lower half is for continuation bytes and leading bytes and is explained further in the legend below.

UTF-8
0	1	2	3	4	5	6	7	8	9	A	B	C	D	E	F
0x	NUL	SOH	STX	ETX	EOT	ENQ	ACK	BEL	BS	HT	LF	VT	FF	CR	SO	SI
1x	DLE	DC1	DC2	DC3	DC4	NAK	SYN	ETB	CAN	EM	SUB	ESC	FS	GS	RS	US
2x	 SP 	!	"	#	$	%	&	'	(	)	*	+	,	-	.	/
3x	0	1	2	3	4	5	6	7	8	9	:	;	<	=	>	?
4x	@	A	B	C	D	E	F	G	H	I	J	K	L	M	N	O
5x	P	Q	R	S	T	U	V	W	X	Y	Z	[	\	]	^	_
6x	`	a	b	c	d	e	f	g	h	i	j	k	l	m	n	o
7x	p	q	r	s	t	u	v	w	x	y	z	{	|	}	~	DEL
8x	+0	+1	+2	+3	+4	+5	+6	+7	+8	+9	+A	+B	+C	+D	+E	+F
9x	+10	+11	+12	+13	+14	+15	+16	+17	+18	+19	+1A	+1B	+1C	+1D	+1E	+1F
Ax	+20	+21	+22	+23	+24	+25	+26	+27	+28	+29	+2A	+2B	+2C	+2D	+2E	+2F
Bx	+30	+31	+32	+33	+34	+35	+36	+37	+38	+39	+3A	+3B	+3C	+3D	+3E	+3F
Cx	2	2	2	2	2	2	2	2	2	2	2	2	2	2	2	2
Dx	2	2	2	2	2	2	2	2	2	2	2	2	2	2	2	2
Ex	3	3	3	3	3	3	3	3	3	3	3	3	3	3	3	3
Fx	4	4	4	4	4	4	4	4	5	5	5	5	6	6		
  7-bit (single-byte) code points. They must not be followed by a continuation byte.[20]
  Continuation bytes.[21] The cell shows in hexadecimal the value of the 6 bits they add.[d]
  Leading bytes for a sequence of multiple bytes, must be followed by exactly N−1 continuation bytes.[22] The tooltip shows the code point range and the Unicode blocks encoded by sequences starting with this byte.
  Leading bytes where not all arrangements of continuation bytes are valid. E0 and F0 could start overlong encodings. F4 can start code points greater than U+10FFFF. ED can start code points in the range U+D800–U+DFFF, which are invalid UTF-16 surrogate halves.[23]
  Do not appear in a valid UTF-8 sequence. C0 and C1 could be used only for an "overlong" encoding of a 1-byte character.[24] F5 to FD are leading bytes of 4-byte or longer sequences that can only encode code points larger than U+10FFFF.[23] FE and FF were never assigned any meaning.[25]
Overlong encodings
In principle, it would be possible to inflate the number of bytes in an encoding by padding the code point with leading 0s. To encode the euro sign € from the above example in four bytes instead of three, it could be padded with leading 0s until it was 21 bits long – 000 000010 000010 101100, and encoded as 11110000 10000010 10000010 10101100 (or F0 82 82 AC in hexadecimal). This is called an overlong encoding.

The standard specifies that the correct encoding of a code point uses only the minimum number of bytes required to hold the significant bits of the code point. Longer encodings are called overlong and are not valid UTF-8 representations of the code point. This rule maintains a one-to-one correspondence between code points and their valid encodings, so that there is a unique valid encoding for each code point. This ensures that string comparisons and searches are well-defined.

Invalid sequences and error handling
Not all sequences of bytes are valid UTF-8. A UTF-8 decoder should be prepared for:

invalid bytes
an unexpected continuation byte
a non-continuation byte before the end of the character
the string ending before the end of the character (which can happen in simple string truncation)
an overlong encoding
a sequence that decodes to an invalid code point
Many of the first UTF-8 decoders would decode these, ignoring incorrect bits and accepting overlong results. Carefully crafted invalid UTF-8 could make them either skip or create ASCII characters such as NUL, slash, or quotes. Invalid UTF-8 has been used to bypass security validations in high-profile products including Microsoft's IIS web server[26] and Apache's Tomcat servlet container.[27] RFC 3629 states "Implementations of the decoding algorithm MUST protect against decoding invalid sequences."[23] The Unicode Standard requires decoders to "...treat any ill-formed code unit sequence as an error condition. This guarantees that it will neither interpret nor emit an ill-formed code unit sequence."

Since RFC 3629 (November 2003), the high and low surrogate halves used by UTF-16 (U+D800 through U+DFFF) and code points not encodable by UTF-16 (those after U+10FFFF) are not legal Unicode values, and their UTF-8 encoding must be treated as an invalid byte sequence. Not decoding unpaired surrogate halves makes it impossible to store invalid UTF-16 (such as Windows filenames or UTF-16 that has been split between the surrogates) as UTF-8,[28] while it is possible with WTF-8.

Some implementations of decoders throw exceptions on errors.[29] This has the disadvantage that it can turn what would otherwise be harmless errors (such as a "no such file" error) into a denial of service. For instance early versions of Python 3.0 would exit immediately if the command line or environment variables contained invalid UTF-8.[30]

Since Unicode 6[31] (October 2010), the standard (chapter 3) has recommended a "best practice" where the error is either one byte long, or ends before the first byte that is disallowed. In these decoders E1,A0,C0 is two errors (2 bytes in the first one). This means an error is no more than three bytes long and never contains the start of a valid character, and there are 21,952 different possible errors.[32] The standard also recommends replacing each error with the replacement character "�" (U+FFFD).

These recommendations are not often followed. It is common to consider each byte to be an error, in which case E1,A0,C0 is three errors (each 1 byte long). This means there are only 128 different errors, and it is also common to replace them with 128 different characters, to make the decoding "lossless".[33]

Byte order mark
If the Unicode byte order mark (BOM, U+FEFF) character is at the start of a UTF-8 file, the first three bytes will be 0xEF, 0xBB, 0xBF.

The Unicode Standard neither requires nor recommends the use of the BOM for UTF-8, but warns that it may be encountered at the start of a file trans-coded from another encoding.[34] While ASCII text encoded using UTF-8 is backward compatible with ASCII, this is not true when Unicode Standard recommendations are ignored and a BOM is added. A BOM can confuse software that isn't prepared for it but can otherwise accept UTF-8, e.g. programming languages that permit non-ASCII bytes in string literals but not at the start of the file. Nevertheless, there was and still is software that always inserts a BOM when writing UTF-8, and refuses to correctly interpret UTF-8 unless the first character is a BOM (or the file only contains ASCII).[35]

Adoption
See also: Popularity of text encodings

Declared character set for the 10 million most popular websites since 2010

Use of the main encodings on the web from 2001–2012 as recorded by Google,[36] with UTF-8 overtaking all others in 2008 and over 60% of the web in 2012 (since then approaching 100%). UTF-8 is the only encoding of Unicode (explicitly) listed there, and the rest only provide subsets of Unicode. The ASCII-only figure includes all web pages that only contain ASCII characters, regardless of the declared header.
UTF-8 has been the most common encoding for the World Wide Web since 2008.[37] As of October 2023, UTF-8 is used by 98.0% of surveyed web sites.[9][e] Although many pages only use ASCII characters to display content, few websites now declare their encoding to only be ASCII instead of UTF-8.[38] Over 50% of the languages tracked have 100% UTF-8 use.

Many standards only support UTF-8, e.g. JSON exchange requires it (without a byte order mark (BOM)).[39] UTF-8 is also the recommendation from the WHATWG for HTML and DOM specifications, and stating "UTF-8 encoding is the most appropriate encoding for interchange of Unicode"[8] and the Internet Mail Consortium recommends that all e‑mail programs be able to display and create mail using UTF-8.[40][41] The World Wide Web Consortium recommends UTF-8 as the default encoding in XML and HTML (and not just using UTF-8, also declaring it in metadata), "even when all characters are in the ASCII range ... Using non-UTF-8 encodings can have unexpected results".[42]

Lots of software has the ability to read/write UTF-8. It may though require the user to change options from the normal settings, or may require a BOM (byte order mark) as the first character to read the file. Examples of software supporting UTF-8 include Microsoft Word,[43][44][45] Microsoft Excel (2016 and later),[46][47] Google Drive, LibreOffice and most databases.

However for local text files UTF-8 usage is less prevalent, where legacy single-byte (and a few CJK multi-byte) encodings remain in use. The primary cause for this are outdated text editors that refuse to read UTF-8 unless the first bytes of the file encode a byte order mark character (BOM).[48]

Some recent software can only read and write UTF-8 or at least do not require a BOM.[49] Windows Notepad, in all currently supported versions of Windows, defaults to writing UTF-8 without a BOM (a change from the outdated/unsupported Windows 7), bringing it into line with most other text editors.[50] Some system files on Windows 11 require UTF-8[51] with no requirement for a BOM, and almost all files on macOS and Linux are required to be UTF-8 without a BOM.[citation needed] Java 18 defaults to reading and writing files as UTF-8,[52] and in older versions (e.g. LTS versions) only the NIO API was changed to do so. Many other programming languages default to UTF-8 for I/O, including Ruby 3.0[53][54] and R 4.2.2.[55] All currently supported versions of Python support UTF-8 for I/O, even on Windows (where it is opt-in for the open() function[56]), and plans exist to make UTF-8 I/O the default in Python 3.15 on all platforms.[57][58] C++23 adopts UTF-8 as the only portable source code file format (surprisingly there was none before).[59]

Usage of UTF-8 in memory is much lower than in other areas, UTF-16 is often used instead. This occurs particularly in Windows, but also in JavaScript, Python,[f] Qt, and many other cross-platform software libraries. Compatibility with the Windows API is the primary reason for this, that choice was initially done due to the belief that direct indexing of the BMP would improve speed. Translating from/to external text which is in UTF-8 slows software down, and more importantly introduces bugs when different pieces of code do not do the exact same translation.

Back-compatibility is a serious impediment to changing code to use UTF-8 instead of a 16-bit encoding, but this is happening. The default string primitive in Go,[61] Julia, Rust, Swift 5,[62] and PyPy[63] uses UTF-8 internally in all cases, while Python, since Python 3.3, uses UTF-8 internally in some cases (for Python C API extensions);[60][64] a future version of Python is planned to store strings as UTF-8 by default;[65][66] and modern versions of Microsoft Visual Studio use UTF-8 internally.[67] Microsoft's SQL Server 2019 added support for UTF-8, and using it results in a 35% speed increase, and "nearly 50% reduction in storage requirements."[68]

All currently supported Windows versions support UTF-8 in some way (including Xbox);[7] partial support has existed since at least Windows XP. As of May 2019, Microsoft has reversed its previous position of only recommending UTF-16; the capability to set UTF-8 as the "code page" for the Windows API was introduced; and Microsoft recommends programmers use UTF-8,[69] and even states "UTF-16 [..] is a unique burden that Windows places on code that targets multiple platforms."[7]

History
See also: Universal Coded Character Set § History
The International Organization for Standardization (ISO) set out to compose a universal multi-byte character set in 1989. The draft ISO 10646 standard contained a non-required annex called UTF-1 that provided a byte stream encoding of its 32-bit code points. This encoding was not satisfactory on performance grounds, among other problems, and the biggest problem was probably that it did not have a clear separation between ASCII and non-ASCII: new UTF-1 tools would be backward compatible with ASCII-encoded text, but UTF-1-encoded text could confuse existing code expecting ASCII (or extended ASCII), because it could contain continuation bytes in the range 0x21–0x7E that meant something else in ASCII, e.g., 0x2F for '/', the Unix path directory separator, and this example is reflected in the name and introductory text of its replacement. The table below was derived from a textual description in the annex.

UTF-1
Number
of bytes	First
code point	Last
code point	Byte 1	Byte 2	Byte 3	Byte 4	Byte 5
1	U+0000	U+009F	00–9F				
2	U+00A0	U+00FF	A0	A0–FF			
2	U+0100	U+4015	A1–F5	21–7E, A0–FF			
3	U+4016	U+38E2D	F6–FB	21–7E, A0–FF	21–7E, A0–FF		
5	U+38E2E	U+7FFFFFFF	FC–FF	21–7E, A0–FF	21–7E, A0–FF	21–7E, A0–FF	21–7E, A0–FF
In July 1992, the X/Open committee XoJIG was looking for a better encoding. Dave Prosser of Unix System Laboratories submitted a proposal for one that had faster implementation characteristics and introduced the improvement that 7-bit ASCII characters would only represent themselves; all multi-byte sequences would include only bytes where the high bit was set. The name File System Safe UCS Transformation Format (FSS-UTF) and most of the text of this proposal were later preserved in the final specification.[70][71][72][73]

FSS-UTF
FSS-UTF proposal (1992)
Number
of bytes	First
code point	Last
code point	Byte 1	Byte 2	Byte 3	Byte 4	Byte 5
1	U+0000	U+007F	0xxxxxxx				
2	U+0080	U+207F	10xxxxxx	1xxxxxxx			
3	U+2080	U+8207F	110xxxxx	1xxxxxxx	1xxxxxxx		
4	U+82080	U+208207F	1110xxxx	1xxxxxxx	1xxxxxxx	1xxxxxxx	
5	U+2082080	U+7FFFFFFF	11110xxx	1xxxxxxx	1xxxxxxx	1xxxxxxx	1xxxxxxx
In August 1992, this proposal was circulated by an IBM X/Open representative to interested parties. A modification by Ken Thompson of the Plan 9 operating system group at Bell Labs made it self-synchronizing, letting a reader start anywhere and immediately detect character boundaries, at the cost of being somewhat less bit-efficient than the previous proposal. It also abandoned the use of biases and instead added the rule that only the shortest possible encoding is allowed; the additional loss in compactness is relatively insignificant, but readers now have to look out for invalid encodings to avoid reliability and especially security issues. Thompson's design was outlined on September 2, 1992, on a placemat in a New Jersey diner with Rob Pike. In the following days, Pike and Thompson implemented it and updated Plan 9 to use it throughout, and then communicated their success back to X/Open, which accepted it as the specification for FSS-UTF.[72]

FSS-UTF (1992) / UTF-8 (1993)[2]
Number
of bytes	First
code point	Last
code point	Byte 1	Byte 2	Byte 3	Byte 4	Byte 5	Byte 6
1	U+0000	U+007F	0xxxxxxx					
2	U+0080	U+07FF	110xxxxx	10xxxxxx				
3	U+0800	U+FFFF	1110xxxx	10xxxxxx	10xxxxxx			
4	U+10000	U+1FFFFF	11110xxx	10xxxxxx	10xxxxxx	10xxxxxx		
5	U+200000	U+3FFFFFF	111110xx	10xxxxxx	10xxxxxx	10xxxxxx	10xxxxxx	
6	U+4000000	U+7FFFFFFF	1111110x	10xxxxxx	10xxxxxx	10xxxxxx	10xxxxxx	10xxxxxx
UTF-8 was first officially presented at the USENIX conference in San Diego, from January 25 to 29, 1993. The Internet Engineering Task Force adopted UTF-8 in its Policy on Character Sets and Languages in RFC 2277 (BCP 18) for future internet standards work, replacing Single Byte Character Sets such as Latin-1 in older RFCs.[6]

In November 2003, UTF-8 was restricted by RFC 3629 to match the constraints of the UTF-16 character encoding: explicitly prohibiting code points corresponding to the high and low surrogate characters removed more than 3% of the three-byte sequences, and ending at U+10FFFF removed more than 48% of the four-byte sequences and all five- and six-byte sequences.

Standards
There are several current definitions of UTF-8 in various standards documents:

RFC 3629 / STD 63 (2003), which establishes UTF-8 as a standard internet protocol element
RFC 5198 defines UTF-8 NFC for Network Interchange (2008)
ISO/IEC 10646:2014 §9.1 (2014)[74]
The Unicode Standard, Version 15.0.0 (2022)[75]
They supersede the definitions given in the following obsolete works:

The Unicode Standard, Version 2.0, Appendix A (1996)
ISO/IEC 10646-1:1993 Amendment 2 / Annex R (1996)
RFC 2044 (1996)
RFC 2279 (1998)
The Unicode Standard, Version 3.0, §2.3 (2000) plus Corrigendum #1 : UTF-8 Shortest Form (2000)
Unicode Standard Annex #27: Unicode 3.1 (2001)[76]
The Unicode Standard, Version 5.0 (2006)[77]
The Unicode Standard, Version 6.0 (2010)[78]
They are all the same in their general mechanics, with the main differences being on issues such as allowed range of code point values and safe handling of invalid input.
