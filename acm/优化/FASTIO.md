## I/O

之后可以用fin，fout读入输出，1e5没有明显优势

```c++
struct BasicBuffer {
	std::vector<char> s;
	BasicBuffer() : s(1 << 18) {}
	char *p = s.data(), *beg = p, *end = p + s.size();
	inline char getc() {
		if (p == end)
			readAll();
		return *p++;
	}
	inline void putc(char c) {
		if (p == end)
			writeAll();
		*p++ = c;
	}
	inline void puts(const char *x) {
		while (*x != 0)
			putc(*x++);
	}
	void readAll() {
		std::fread(beg, 1, end - beg, stdin);
		p = s.data();
	}
	void writeAll() {
		std::fwrite(beg, 1, p - beg, stdout);
		p = s.data();
	}
};

struct FastI : BasicBuffer {
	FastI() {
		readAll();
	}
	ll read() {
		ll x = 0;
		char c = getc();
		bool sgn = true;
		while (!std::isdigit(c))
			sgn = sgn && c != '-', c = getc();
		while (std::isdigit(c))
			x = x * 10 + c - '0', c = getc();
		return sgn ? x : -x;
	}
	template <class T>
	FastI &operator>>(T &x) {
		return x = read(), *this;
	}
	FastI &operator>>(char &x) {
		return x = getc(), *this;
	}
};

struct FastO : BasicBuffer {
	std::array<char, 32> u{};
	~FastO() {
		writeAll();
	}
	void output(ll x) {
		char *i = u.data() + 20;
		if (x < 0)
			putc('-'), x = -x;
		do
			*--i = x % 10 + '0', x /= 10;
		while (x > 0);
		puts(i);
	}
	template <class T>
	FastO &operator<<(const T &x) {
		return output(x), *this;
	}
	FastO &operator<<(char x) {
		return putc(x), *this;
	}
	FastO &operator<<(const char *x) {
		return puts(x), *this;
	}
	FastO &operator<<(const std::string &x) {
		return puts(x.c_str()), *this;
	}
};

FastI fin;
FastO fout;
```

## 第二

```c++
namespace FastIOT{
	const int bsz=1<<18;
	char bf[bsz],*head,*tail;
	IL char gc(){if(head==tail)tail=(head=bf)+fread(bf,1,bsz,stdin);if(head==tail)return 0;return *head++;}
	template<typename T>IL void read(T &x){T f=1;x=0;char c=gc();for(;c>'9'||c<'0';c=gc())if(c=='-')f=-1;
	for(;c<='9'&&c>='0';c=gc())x=(x<<3)+(x<<1)+(c^48);x*=f;}
	template<typename T>IL void print(T x){if(x<0)putchar(45),x=-x;if(x>9)print(x/10);putchar(x%10+48);}
	template<typename T>IL void println(T x){print(x);putchar('\n');}
}
using namespace FastIOT;
```

