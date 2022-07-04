# Go Brackets


There is little agreement among developers about how the brackets should be used. There are basically three ways to write a block of code with languages that require curly brackets.  
  

**STYLE 1**
```
if response == True{
    return "OK";
}
```
  
**STYLE 2**
```
if response == True
{
    return "OK";
}
```
  
**STYLE 3**
```
if response == True
    return "OK";
```

Countless words have been spent to prove one or the other faction right. Do you want to know mine? I have always used style 1 for coding in C / C ++ and Java. Python is another story.  
  
With Go the situation is different: there is only one correct way to use parentheses, this one

```
package main
import "fmt"
func main() {
    fmt.Println("hello world")
}
```

If you write something different, you got an error

```
// File test.go
package main
import "fmt"
func main() 
{
    fmt.Println("hello world")
}

$ go run test.go 
# command-line-arguments
./1.0_BracketError.go:11:6: missing function body
./1.0_BracketError.go:12:1: syntax error: unexpected semicolon or newline before {
```

What is the reason for this choice? The official documentation gives a very clear explanation.

>Why are there braces but no semicolons? And why can't I put the opening brace on the next line?
>Go uses brace brackets for statement grouping, a syntax familiar to programmers who have worked with any language in the C family. Semicolons, however, are for parsers, not for people, and we wanted to eliminate them as much as possible. To achieve this goal, Go borrows a trick from BCPL: the semicolons that separate statements are in the formal grammar but are injected automatically, without lookahead, by the lexer at the end of any line that could be the end of a statement. This works very well in practice but has the effect that it forces a brace style. For instance, the opening brace of a function cannot appear on a line by itself.

