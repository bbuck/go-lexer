This package provides a Lexer that functions similarly to Rob Pike's discussion
about lexer design in this [talk](https://www.youtube.com/watch?v=HxaD_trXwRE).

You can define your token types by using the `lexer.TokenType` type (`int`) via

```go
const (
        StringToken lexer.TokenType = iota
        IntegerToken
        etc...
)
```

And then you define your own state functions (`lexer.StateFunc`) to handle
analyzing the string.

```go
func StringState(l *lexer.L) lexer.StateFunc {
        l.Next() // eat starting "
        l.Ignore() // drop current value
        while l.Peek() != '"' {
                l.Next()
        }
        l.Emit(StringToken)

        return SomeStateFunction
}
```

This Lexer is meant to emit tokens in such a fashion that it can be consumed
by go yacc.

# License

MIT