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

<details>
  <summary>Spoiler warning</summary>
  
  Spoiler text. Note that it's important to have a space after the summary tag. You should be able to write any markdown you want inside the `<details>` tag... just make sure you close `<details>` afterward.
  
  ```javascript
  console.log("I'm a code block!");
  ```
  
</details>
