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

    
    
    
---------------
    
### B. Ghép xâu
    
<details>
<summary>Đề bài</summary>

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
</details>

<details>
<summary>Hướng dẫn</summary>
    
    Thực hiện việc lấy mã Hash của các đoạn k ký tự liên tiếp trong xâu ban đầu vào tập A,
    và của tất cả các xâu trong tập hợp cho trước vào tập B
    
    Ta lưu lại hai tham số cho mỗi tập
    1. Mã Hash
    2. Thứ tự xâu
    
    Sort lại hai tập theo giá trị của mã Hash. 
    Đối với những mã Hash bằng nhau trong tập B, ta xếp mã Hash nào có 'thứ tự xâu' lớn hơn lên trước.
    Việc này đảm bảo cho các xâu giống nhau, thì xâu có 'thứ tự' lớn hơn luôn được đẩy lên trước
    
    Ghi kết quả : 
    result[thứ tự của xâu A[i]] = thứ tự xâu của B[i]
    for (i từ 1 -> m) cout << result[i] << " ";
</details>

<details>
<summary>Code</summary>
    
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
</details>

-----------------------------------------

### C. Bắt đầu và kết thúc
    
<details>
<summary>Đề bài</summary>

Cho một dãy số nguyên gồm n phần tử, đã bị xáo trộn vị trí theo một quy tắc như sau:
    
• Đảo ngược vị trí của dãy k số bắt đầu từ số thứ nhất tính từ trái,
    
• Đảo ngược vị trí của dãy k số bắt đầu từ số thứ hai tính từ trái,
    
• . . . . . .
    
• Đảo ngược vị trí của dãy k số kết thúc bởi số cuối cùng ở bên phải.
    
Ví dụ, với k = 3 và trình tự ban đầu các số là [1, 2, 3, 1, 2], sau khi sắp xếp lại theo kiểu trên
    
trình tự các số sẽ là [3, 1, 2, 2, 1].
    
Cho biết trình tự ban đầu và trình tự hiện tại của dãy số. Hãy xác định có bao nhiêu giá trị k khác nhau có thể đã
    
được áp dụng khi xáo dãy số trên và chỉ rõ các giá trị đó.
    
**Input**
    
• Dòng đầu tiên chứa số nguyên n(1 ≤ n ≤ 10^5),
    
• Dòng thứ 2 và dòng thứ 3: mỗi dòng chứa n số nguyên xác định trình tự ban đầu và trình tự hiện
    
tại của dãy số, mỗi số có giá trị trong phạm vi [1..10^5].
    
**Output**
    
• Dòng đầu tiên chứa số nguyên m – số giá trị k khác nhau có thể được sử dụng
    
• Dòng tiếp theo chứa m số nguyên dương – các giá trị có thể của k theo thứ tự tăng dần
    
**Example**
    
*input*
```c++
5
1 2 3 1 2
3 1 2 2 1
```
    
*output*
```c++
1
3
```
</details>
    
<details>
<summary>Hướng dẫn</summary>
    
    LƯU Ý: Nháp một chút ra giấy sẽ dễ hiểu hơn
    
    Ta để ý là việc xáo các xâu như vậy thì tổng số lần xoay sẽ luôn là n - k + 1
    Sẽ có hai trường hợp xảy ra
    - TH1: (n - k + 1) % 2 == 0
        Khi đó bản chất của xâu sẽ là (n-k+1) ký tự ở cuối hợp lại với (k-1) kí tự đầu tiên của xâu
    - TH2: (n - k + 1) % 2 == 1
        Khi đó bản chất của xâu sẽ là (n-k+1) ký tự ở cuối hợp lại với (k-1) kí tự đầu tiên (theo thứ tự ngược lại) của xâu
    
    Bài tập đòi hỏi kĩ thuật lấy mã Hash ngược của xâu
    
    Đáp án: Với mỗi k từ 1->n xét từng trường hợp tương ứng của (n - k + 1)
    Nếu mã Hash của xâu tìm được bằng mã Hash của xâu ban đầu, thì k là một đáp án khả thi
</details>
    
<details>
    <summary>Code</summary>
    
```c++
#include <bits/stdc++.h>
#pragma GCC optimize("Ofast")
#pragma GCC optimize ("unroll-loops")
#pragma GCC target("sse,sse2,sse3,ssse3,sse4,popcnt,abm,mmx,avx,tune=native")

#define ll                      long long
#define up(i,a,b)               for (int i = (a); i <= (b); i++)
#define down(i,a,b)             for (int i = (a); i >= (b); i--)
#define MOD                     1000000007
#define base                    311
using namespace std;

const int maxn = 1000001;
const long long MM = 1ll*MOD*MOD;
int n;
ll a[maxn];
ll b[maxn];
ll hashx[maxn];
ll hashn[maxn];
ll D[maxn]; // Decryptor
long long hashB;

void create(){
    up(i, 1, n){
        hashx[i] = (hashx[i-1]*base + a[i]) % MOD;
    }
    down(i, n, 1){
        hashn[i] = (hashn[i+1]*base + a[i]) % MOD;
    }
}

ll getx(int u, int v){
    return (hashx[v] - hashx[u-1]*D[v-u+1] + MM) % MOD;
}

ll getn(int u, int v){
    return (hashn[u] - hashn[v+1]*D[v-u+1] + MM) % MOD;
}

bool check(int k){
    long long sum = 0;
    if ((n - k + 1) % 2 == 0){
        sum = (hashx[k-1] + getx(k, n)*D[k-1]) % MOD;
    }
    else {
        sum = (getn(1, k-1) + getx(k, n)*D[k-1]) % MOD;
    }
    /// Decryptor is generated from 1 to n, so it
    /// only has effect on (1 -> n) hashed substring
    return (sum == hashB);
}

signed main (){
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    up(i, 1, n) cin >> a[i];
    up(i, 1, n) cin >> b[i];
    D[0] = 1;
    up(i, 1, n) D[i] = (D[i-1]*base) % MOD;
    up(i, 1, n){
        hashB = (hashB*base + b[i]) % MOD;
    }
    create();

    vector<int> res;
    for (int i = 1; i <= n; i++){
        if (check(i)) res.push_back(i);
    }

    cout << res.size() << "\n";
    for (auto x : res){
        cout << x << " ";
    }
    return 0;
}
```
</details>
