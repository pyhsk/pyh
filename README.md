# pyh: Extended Python3 syntax inspired by Haskell and more

Compile into Python, or, preprocessor.


```python
# Function call
interact
interact()

interact countLines
interact(countLines())

foo 5
foo(5)

add 1 2
add(1, 2)

## Special:
fst ("haskell", 1)
fst(("haskell", 1))

fst("haskell", 1) # old-school
<refuse, to prevent errors>


# Function definition
add a b
	return a + b

def add(a, b):
	return a + b

# One-line function definition
add a b = a + b

def add(a, b):
		return a + b

# No colons any more
while True
	pass

for i in range(100)
	print i

# Inline statements
haskell = if 1 == 1 then "awesome" else "awful"
haskell =  pyh_if(1 == 1, "awesome", "awful")

# Better lambda
\i: show i
lambda i: show(i)

\x y: 2*x + y
lambda x, y: return 2 * x + y


# Switch
case args
  "help" -> printHelp
  "start" -> startProgram
  _ -> putStrLn "bad args"
 
if args == "help":
	printHelp()
elif args == "start":
	startProgram()
else:
	putStrLn("bad args")

# Old-school logical operators
&& -> and
|| -> or

# Where
qsort l = qsort lesser + [p] + qsort greater
    where p = l[0]
		  xs = l[1:]
		  lesser  = filter (< p) xs
          greater = filter (>= p) xs
# you can see: + operator is inferior to function calls
```



Example code:
```python
def decistmt(s):
    result = []
    g = tokenize(BytesIO(s.encode('utf-8')).readline)  # tokenize the string
    for toknum, tokval, _, _, _ in g:
        if toknum == NUMBER and '.' in tokval:  # replace NUMBER tokens
            result.extend([
                (NAME, 'Decimal'),
                (OP, '('),
                (STRING, repr(tokval)),
                (OP, ')')
            ])
        else:
            result.append((toknum, tokval))
    return untokenize(result).decode('utf-8')

decistmt s
    result = []
    g = tokenize $ (BytesIO $ s.encode 'utf-8').readline  # tokenize the string
    for toknum, tokval, _, _, _ in g
        if toknum == NUMBER && '.' in tokval  # replace NUMBER tokens
            result.extend [
                (NAME, 'Decimal'),
                (OP, '('),
                (STRING, repr(tokval)),
                (OP, ')')
            ]
        else
            result.append (toknum, tokval)
    return (untokenize result).decode 'utf-8'
```


Design philosophy:
* Do not mix with official syntax.

Links:
* https://wiki.python.org/moin/PythonImplementations
* https://jon.how/likepython/
* https://learnxinyminutes.com/docs/haskell/

Implementation: stdlib/tokenize

