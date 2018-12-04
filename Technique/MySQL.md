## Required Storage and Range for Integer Types Supported by MySQL

Type | Storage (Bytes) | Minimum Value Signed |	Minimum Value Unsigned | Maximum Value Signed	| Maximum Value Unsigned
--- | --- | --- | --- | --- | ---
TINYINT | 1 | -128 | 0 | 127 | 255
SMALLINT |	2 |	-32768 | 0 | 32767 | 65535
MEDIUMINT |	3 |	-8388608 | 0 | 8388607 | 16777215
INT | 4 | -2147483648 | 0 | 2147483647 | 4294967295
BIGINT | 8 | -2^63 | 0 | 2^63-1 | 2^64-1

## [utf8_unicode_ci vs utf8_general_ci by MySQL](https://forums.mysql.com/read.php?103,187048,188748#msg-188748)

### utf8_general_ci is a very simple collation. 

What it does - it just 
* removes all accents 
* then converts to upper case 
* uses the code of this sort of "base letter" result letter to compare. 

For example, these Latin letters: ÀÁÅåāă (and all other Latin letters "a" 
with any accents and in any cases) are all compared as equal to "A". 

### utf8_unicode_ci

* utf8_unicode_ci supports so called expansions and ligatures.
* utf8_unicode_ci is *generally* more accurate for all scripts. 

**The disadvantage of utf8_unicode_ci is that it is a little bit 
slower than utf8_general_ci.**

So when you need better sorting order - use utf8_unicode_ci, 
and when you utterly interested in performance - use utf8_general_ci

## force index
select id from table force index(PRI/index)