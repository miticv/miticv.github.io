
# Erlang

http://www.erlang.org/downloads   
Install to `C:\Erlang\erl7.3` and add to PATH: `C:\Erlang\erl7.3\bin`   

When we defined Erlang, we did so at a language level, but in a broader sense, this is not all there is to it: Erlang is also a development environment as a whole. The code is compiled to bytecode and runs inside a virtual machine. So Erlang, much like Java and kids with ADD, can run anywhere. The standard distribution includes (among others) development tools (compiler, debugger, profiler, test framework), the Open Telecom Platform (OTP) Framework, a web server, a parser generator, and the mnesia database, a key-value storage system able to replicate itself on many servers, supporting nested transactions and letting you store any kind of Erlang data.   

##Invariable Variables   
Must start with Capital letter!  
variables can start with an underscore ('_') too, but by convention their use is restricted to values you do not care about   
```
>2+15.
17
>Var = 15

>f(Var) //clear variable 'Var'
>f() // clear all variables
```

## Atom
