```c++
const ll base1=1331,base2=311,mod1=1e9+7,mod2=1000000000000002493;
inline ll ksc(ull x,ull y ,ll p){return (x*y-(ull)((ld)x/p*y)*p+p)%p;}
map<pair<ull,ull>,int>h;
ull hash[N];
void Hash()
{
	hash[0]=(ull)1;
	for(int i=1;i<N-10;++i)hash[i]=ksc(hash[i-1],base1,mod1);
}
```

