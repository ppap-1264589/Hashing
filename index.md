# [Trang chủ](https://ppap-1264589.github.io/interesting-solution)

## Các bài toán
- A. Tìm xâu
- B. Ghép xâu
- C. Bắt đầu và kết thúc
- D. ADN
* Link download đề bài:
- [A. Tìm xâu](https://github.com/ppap-1264589/Hashing/files/6961866/A-Hash.pdf)
- [B. Ghép xâu](https://github.com/ppap-1264589/Hashing/files/7251329/B-Hash.pdf)
- [C. Bắt đầu và kết thúc](https://github.com/ppap-1264589/Hashing/files/7251526/C-Hash.pdf)
- [D. ADN](https://github.com/ppap-1264589/Hashing/files/7251529/D-Hash.pdf)


## Chi tiết

### A. Tìm xâu

<details>
<summary>Đề bài</summary>

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
</details>

<details>
<summary>Hướng dẫn</summary>

    Hoàn toàn có thể làm trâu bài toàn này với độ phức tạp O(n*m) cùng hàm find() trong thư viện cstring
    Tuy nhiên với thuật toán Hash String thì chỉ cần khởi tạo mã Hash trong O(m+n) và kiểm tra trong O(1)
</details>

<details>
<summary>Code</summary>
    
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
</details>

    
    
    
