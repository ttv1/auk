# hello

asdas


```awk 

function subray(a,b)   { a[b][1];    delete a[b][1]; }

function push(x,y,z,   n) {
  n = length(x[y])
  x[y][n+1] = z
}

```

here

```awk 

function test(   x,k,j,l) {
  split("",x,"")
  subray(x,1)
  test1(x[1])
  for(k in x)
    for(j in x[k])
      for(l in x[k][j])
        print k,j,l
  print(length(x[1][2][3]))
  show(x[1][2][3],"x")
}
function test1(x) {
  subray(x, 2)
  test2(x[2])
}
function test2(x) {
  subray(x,3)
  num0(x[3])
}
function num0(x)   { 
   x.n = x.mu=x.m2=0; x.hi=-1e31; x.lo=1e32 
 }
function show(a,pre,    i) {
  for(i in a)
    print pre"["i"]="a[i]
}
BEGIN { test() }

```
