#Maths

## Coprime

2 integers a & b are coprime if they don't have any common primes in their factorization.

say gcd(a,b) = c

then a = c*x  ,   b = c*y   where x,y some positive integer.

then the algo to find c is
```
while(a!=b) {
  if(a>b)
    a-=b;
  else
    b-=a;
}
return a;
```
