
# Things (nums and sys and stuff)


```awk 

@include "lib"

```


## Sample

A thing for catching many values, but keepig
only  small sample of them.


```awk 

```


## Column

`Column`s hold either `Number`s or `Symbol`s,
      at some specific column `pos`.
`Column`s have `txt` (the txt
top of the column)..


```awk 
function Column(i,     txt,pos) {
  has(i,"my")
  i.adder= ""
  i.name = txt
  i.pos  = pos
}
function Column1(i,v,pos,t,  tmp) {
  if (v=="?") return
  if ( ! length(i.my) ) {
    if (isnum(v)) {
      i.adder="NumberFarcade1"
      NumberFarcade(i.my)
      t.cols.num[pos]
    } else {
      i.adder="Symbol1"
      Symbol(i.my)
      t.cols.sym[pos]
  }}
  tmp=i.adder
  @tmp(i.my,v)
}
function NumberFarcade(i) {
  has(i,"remedian","Remedian")
  has(i,"sample",  "Sample")
  has(i,"num",     "Number")
}
function NumberFarcade1(i,v) {
  if (Sample1(i.sample, v)) {
    Remedian1(i.remedian,v)
    Number1(i.num, v)
}}
function Sample(i,     most) {
  i.most= most ? most : 64
  has(i,"all")
  i.n=0
}
function Sample1(i,v,    
                 added,len) {
  i.n++
  len=length(i.all)
  if (len < i.most) {
    push(i.all,v)
    added=1
  } else if (rand() < len/i.n) {  
    i.all[ int(len*rand()) + 1 ] = v
    added=1
  }
  return added
}
function Symbol(i) {
  has(i,"count")
  i.mode = ""
  i.most = 0
}
function Symbol1(i,v,     n) {
  n = ++i.counts[v]
  if (n > i.most) {
    i.mode = v
    i.most = n
}}
function Number(i) {
  i.hi = -1e32
  i.lo =  1e32
  i.n  = i.mu = i.m2 = i.sd = 0
}
function Number1(i,v,          delta) {
  v    += 0
  i.n  += 1
  i.lo  = v < i.lo ? v : i.lo 
  i.hi  = v > i.hi ? v : i.hi 
  delta = v - i.mu
  i.mu += delta/i.n
  i.m2 += delta*(v-i.mu)
  if (i.n > 1)
	  i.sd = (i.m2/(i.n-1))^0.5
}
function Remedian(i,   k) {
  has(i,"all")
  has(i,"more")
  i.k = k ? k : 128
  i._median = ""
}
function Remedian1(i, v)  {
  push(i.all,v)
  if (length(i.all) == i.k) {
    if (!length(i.more)) 
      Remedian(i.more,i.k)
    i._median = median(i.all)
    Remedian1(i.more, i._median)
    empty(i.all)
}}
function Remedians(i) {
  if (length(i.more))  
     return Remedians(i.more)
  if (i._median == "") 
    i._median = median(i.all)
  return i._median
}
```
