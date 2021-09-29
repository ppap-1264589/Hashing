## [Trang chủ](https://ppap-1264589.github.io/interesting-solution)

# Các bài toán
- [A. Tìm xâu](#id-sectionA)
- [B. Ghép xâu](#id-sectionB)
- [C. 
* Link download đề bài:
- [A. Tìm xâu](https://github.com/ppap-1264589/Hashing/files/6961866/A-Hash.pdf)
- [B. Ghép xâu](https://github.com/ppap-1264589/Hashing/files/7251329/B-Hash.pdf)
- [A](https://github.com/ppap-1264589/Hashing/files/6961866/A-Hash.pdf)
- [A](https://github.com/ppap-1264589/Hashing/files/6961866/A-Hash.pdf)
- [A](https://github.com/ppap-1264589/Hashing/files/6961866/A-Hash.pdf)

# Chi tiết

<div id='id-sectionA'/>

### A. Tìm xâu

Cho 2 xâu A, B độ dài không vượt quá 10^6. Đưa ra những vị trí xuất hiện xâu A trong xâu B.

**Input**

Dòng đầu chứa xâu A

Dòng hai chứa xâu B

**Output**

Dòng đầu chứa số k là số vị trí xuất hiện xâu A trong xâu B.

Dòng 2 chứa k số nguyên tăng dần xác định k vị trí xuất hiện A trong B

**Example**

*Input*
```C++
viet
vietnamnamvietviet
```

*Output*
```c++
3
1 11 15
```

# Code
```c++
#include <bits/stdc++.h>
#define Task ""
#define up(i,a,b)               for (int i = (a); i <= (b); i++)
#define base                    4
using namespace std;

const int maxn = 10000001;
const long long MM = 1ll*MOD*MOD;

long long H[maxn];
long long B[maxn];
string a,b;
int n,m;

long long gethash(int u, int v){
    return (B[v] - B[u-1]*H[n] + MM) % MOD;
}

signed main (){
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    cin >> b >> a;
    n = a.size();
    m = b.size();
    a = '@' + a;
    b = '@' + b;

    long long hashA = 0;
    for (int i = 1; i <= n; i++){
        hashA = (hashA*base + a[i]) % MOD;
    } // Hash code of string a

    H[0] = 1;
    for (int i = 1; i <= m; i++){
        B[i] = (B[i-1]*base + b[i]) % MOD;
        // Hash code of substrings from 1 to i in b
        H[i] = (H[i-1]*base) % MOD;
        // Decryptor
    }

    for (int v = n; v <= m; v++){
        int u = v - n + 1;
        if (gethash(u, v) == hashA){
            cout << u << " ";
        }
    }
    return 0;
}
```
-----------------------

### B. Ghép xâu

Cho một xâu gồm n ký tự

Cho một tập hợp gồm m xâu 

Hãy chỉ ra trình tự lắp ghép các mẩu giấy để được xâu ban đầu.

Biết rằng luôn tồn tại cách ghép m xâu từ tập hợp đã cho thành xâu n ký tự ban đầu

**Input**

Dòng đầu tiên chứa 2 số nguyên n và m(1 ≤ m ≤ n ≤ 10^6) 

Dòng thứ 2 chứa xâu ban đầu gồm các ký tự thường, độ dài không quá 10^6. 

Mỗi dòng trong m dòng tiếp theo chứa xâu độ dài k = n / m.

**Output**

Đưa ra một dòng m số nguyên xác định trình tự lắp ghép các mẩu giấy. Nếu tồn tại nhiều cách lắp
ghép thì đưa ra cách có thứ tự từ điển lớn nhất.

**Example**

*Input*
```c++
9 3
toivoitoi
voi
toi
toi
```

*Output*
```c++
3 1 2
```

# Editorial
```c++

```

# Code
```c++
#include <bits/stdc++.h>
#pragma GCC optimize("Ofast")
#pragma GCC optimize ("unroll-loops")
#pragma GCC target("sse,sse2,sse3,ssse3,sse4,popcnt,abm,mmx,avx,tune=native")

#define up(i,a,b)               for (int i = (a); i <= (b); i++)
#define down(i,a,b)             for (int i = (a); i >= (b); i--)
#define MOD                     1000000007
#define base                    3956221
#define pii                     pair<int, int>
#define f                       first
#define s                       second
using namespace std;

const int maxn = 1000001;
const long long MM = 1ll*MOD*MOD;
int n,m;
string s;
pii S[maxn];
pii R[maxn];
int res[100008];

long long gethash(string t){
    long long vhash = 0;
    int nn = t.size();
    t = '@' + t;
    for (int i = 1; i <= nn; i++){
        vhash = (vhash*base + t[i]) % MOD;
    }
    return vhash;
}

//bool cmp1(pii x, pii y){
//    if (x.f == y.f) return (x.s < y.s);
//    return (x.f < y.f);
//}

bool cmp2(pii x, pii y){
    if (x.f == y.f) return (x.s > y.s);
    return (x.f < y.f);
}

signed main (){
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m;
    cin >> s;
    s = '@' + s;
    int u = n/m;
    string a;
    int dem = 1;
    for (int i = 1; i <= n; i += u){
        a = s.substr(i, u);
        S[dem] = make_pair(gethash(a), dem);
        dem++;
    }

    dem = 0;
    for (int i = 1; i <= m; i++){
        string x;
        cin >> x;
        R[i] = make_pair(gethash(x), i);
    }

    sort(S+1, S+m+1);
    sort(R+1, R+m+1, cmp2);

    up(i, 1, m) res[S[i].s] = R[i].s;
    up(i, 1, m) cout << res[i] << " ";
}
```
