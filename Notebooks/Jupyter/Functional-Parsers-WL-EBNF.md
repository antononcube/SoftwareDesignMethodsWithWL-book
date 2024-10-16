# Functional Parsers (WL <-> EBNF)

## 1

```ebnf
<top> = <a> | <b> ;
<a> = 'a' , { 'A' } , [ '1' ];
<b> = 'b' , ( 'B' | '2' );
```

```mathematica
pTOP = ParseAlternativeComposition[pA, pB]; 
pA = ParseSequentialComposition[ParseSymbol["a"], ParseSequentialComposition[ParseMany[ParseSymbol["A"]], ParseOption[ParseSymbol["1"]]]]; 
pB = ParseSequentialComposition[ParseSymbol["b"], ParseAlternativeComposition[ParseSymbol["B"], ParseSymbol["2"]]];
```

## 2 

```ebnf
<args> = <newArg> | <oldArg> <@ MyFunc;
```

```mathematica
pARGS = ParseAlternativeComposition[pNEWARG, ParseApply[MyFunc, pOLDARG]];
```

## 3

```ebnf
<top> = <who> , <verb> , <lang> ;
<who> = 'I' | 'We' ;
<verb> = ( 'love' | 'hate' | 'like' | { '❤️' } | '🤮' ) <@ MyVerb ;
<lang> = ( 'Julia' | 'Perl' | 'Python' | 'R' | 'Raku' | 'WL' ) <@ MyLang; 
```

```mathematica
pTOP = ParseSequentialComposition[pWHO, ParseSequentialComposition[pVERB, pLANG]];
pWHO = ParseAlternativeComposition[ParseSymbol["I"], ParseSymbol["We"]];
pVERB = ParseApply[MyVerb, ParseAlternativeComposition[ParseSymbol["love"], ParseSymbol["hate"], ParseSymbol["like"], ParseMany[ParseSymbol["❤️"]], ParseSymbol["🤮"]]];
pLANG = ParseApply[MyLang, ParseAlternativeComposition[ParseSymbol["Julia"], ParseSymbol["Perl"], ParseSymbol["Python"], ParseSymbol["R"], ParseSymbol["Raku"], ParseSymbol["WL"]]];
```