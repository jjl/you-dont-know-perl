# Perl Delta Redux.

## 5.18

- `warnings` category for experimental `feature`s
- Hashes now randomized
- New Hash functions
- `PERL_HASH_SEED` = hex string
- `PERL_PERTURB_KEYS`
- `Hash::Util::hash_seed()` returns a string
- `PERL_HASH_SEED_DEBUG` more detailed
- Unicode 6.2
- Support for non-latin-1 character name custom aliases
- `${^LAST_FH}`
- Character class set operations in regexps, ie:

```perl
$char =~ /(?[ \p{Cyrillic} & \p{Lower} ])/
```
- lexical subs 

```perl
my sub foo {  };
foo();
```

- computed labels

```perl
my $GOTO_TABLE = {
    0 => 'A',
    1 => 'B',
    2 => 'B',
    3 => 'A',
    4 => 'A',
    5 => 'A',
    6 => 'B',
};

C: {
    A: for my $a ( 0 .. 8 ) {
      B:  for my $b ( 0 .. 3 ) {
        print "$a . $b\n";
        next $GOTO_TABLE->{$a} || 'C';
      }
    }
}
```
→
```
0 . 0
1 . 0
1 . 1
1 . 2
1 . 3
2 . 0
2 . 1
2 . 2
2 . 3
3 . 0
4 . 0
5 . 0
6 . 0
6 . 1
6 . 2
6 . 3
7 . 0
```
- Bunch of stuff added to `CORE::` : `defined, delete, exists, glob, pos, protoytpe, scalar, split, study, undef`
- `kill -INT $ID` sends `SIGINT` to process group `$ID` instead of sending `0` ( Previously you needed to say `-15` )
- Unknown names in `\N{...}` a syntax error
- Invalid character name aliases in `\N{...}` a syntax error.
- `\N{BELL}` is 🔔( U+1F514) instead of  (U + 0007 ). Use `\N{ALERT}` if you want the control charachter.
- [`New Restrictions in Multi-Character Case-Insensitive Matching in Regular Expression Bracketed Character Classes`](https://metacpan.org/module/RJBS/perl-5.18.1/pod/perl5180delta.pod#New-Restrictions-in-Multi-Character-Case-Insensitive-Matching-in-Regular-Expression-Bracketed-Character-Classes) -- somebody explain this in a way a human can understand, I read it and its nonsense to me.
- single character variables ( ie: `$v` ) now imply the same restrictions as normal variables
- `${foo:bar}` and `$foo:bar` are now equally invalid
- vertical tabs (`\cK` ) are now whitespace (`\s`) everywhere.
- `s///e` stricter. My god. This was valid code:

```perl
%_=(_,"Just another ");
$_="Perl hacker,\n";
s//_}->{_/e;print
```
- `given` aliases `$_` like `foreach () {}`
- smartmatch ( `~~` ) deemed experimental
- lexical `$_` now experiemental, documentation here is hard to grok
- `$/  = \8; my $scalar = <>` reads 8 characters, not 8 bytes.
- `<<"Foo";` parsing always occurs on line after the heredoc ( perl #114040 )
- `m/foo/and 1` no longer valid, → `m/foo/ and 1`
- `for qw( 1 2 3 ) {}` no longer valid → `for (qw( 1 2 3 ) ){  }`
- `use warnings` no longer accidentally turns off warnings that are already turned on
- `state sub { }` and `our sub { } ` now only valid under `lexical_subs`
- Assigning to `%ENV` now stringifies and downgrades to bytes within the perl interpreter, not only in children inheriting `%ENV`
- `require` now considers a present, but unreadable file an error and `dies` instead of ignoring the file and continuing searching `@INC`
- `split ' ', $bar` now behaves the same as `$foo = ' '; split $foo, $bar`
- shit with `m{fooo\{1,3\}}` meaning the slashes escape the outerbrackets, not the metacharacter behaviour
- `/( ?foo )/` and `/( *foo )/` deprecated, use `/(?foo)/` and `/(?*foo)/` plzkthx

## 5.16

## 5.14

## 5.12

## 5.10

## 5.8
