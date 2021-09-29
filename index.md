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

Cho 2 xâu A, B độ dài không vượt quá 10^6. Đưa ra những vị trí xuất hiện xâu A trong xâu B.

**Input**

Dòng đầu chứa xâu A

Dòng hai chứa xâu B

**Output**

Dòng đầu chứa số k là số vị trí xuất hiện xâu A trong xâu B.

Dòng 2 chứa k số nguyên tăng dần xác định k vị trí xuất hiện A trong B

**Example**

*Input*
```c++
viet
vietnamnamvietviet
```

*Output*
```c++
3
1 11 15
```


#### Hướng dẫn

Hoàn toàn có thể làm trâu bài toán này với độ phức tạp O(n*m) cùng hàm find() trong thư viện <cstring>

Tuy nhiên với thuật toán Hash String thì chỉ cần khởi tạo mã Hash trong O(m+n) và kiểm tra trong O(1)
    
#### [Code](https://ideone.com/u6oNbQ)

---------------
    
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

#### Hướng dẫn

Thực hiện việc lấy mã Hash của các đoạn k ký tự liên tiếp trong xâu ban đầu vào tập A, và của tất cả các xâu trong tập hợp cho trước vào tập B
    
Ta lưu lại hai tham số cho mỗi tập:
1. Mã Hash
2. Thứ tự xâu
    
Sort lại hai tập theo giá trị của mã Hash. 
Đối với những mã Hash bằng nhau trong tập B, ta xếp mã Hash nào có 'thứ tự xâu' lớn hơn lên trước.
    
Việc này đảm bảo cho các xâu giống nhau, thì xâu có 'thứ tự' lớn hơn luôn được đẩy lên trước
    
Ghi kết quả : 
```c++    
result[thu tu cua xau A[i]] = thu tu cua xau B[i]    
for (i : 1 -> m) cout << result[i] << " ";
```

#### [Code](https://ideone.com/od38MB)

-----------------------------------------

### C. Bắt đầu và kết thúc
    
Cho một dãy số nguyên gồm n phần tử, đã bị xáo trộn vị trí theo một quy tắc như sau:
    
• Đảo ngược vị trí của dãy k số bắt đầu từ số thứ nhất tính từ trái,
    
• Đảo ngược vị trí của dãy k số bắt đầu từ số thứ hai tính từ trái,
    
• . . . . . .
    
• Đảo ngược vị trí của dãy k số kết thúc bởi số cuối cùng ở bên phải.
    
Ví dụ, với k = 3 và trình tự ban đầu các số là [1, 2, 3, 1, 2], sau khi sắp xếp lại theo kiểu trên trình tự các số sẽ là [3, 1, 2, 2, 1].
    
Cho biết trình tự ban đầu và trình tự hiện tại của dãy số. Hãy xác định có bao nhiêu giá trị k khác nhau có thể đã được áp dụng khi xáo dãy số trên và chỉ rõ các giá trị đó.
    
**Input**
    
• Dòng đầu tiên chứa số nguyên n(1 ≤ n ≤ 10^5),
    
• Dòng thứ 2 và dòng thứ 3: mỗi dòng chứa n số nguyên xác định trình tự ban đầu và trình tự hiện
    
tại của dãy số, mỗi số có giá trị trong phạm vi [1..10^5].
    
**Output**
    
• Dòng đầu tiên chứa số nguyên m – số giá trị k khác nhau có thể được sử dụng
    
• Dòng tiếp theo chứa m số nguyên dương – các giá trị có thể của k theo thứ tự tăng dần
    
**Example**
    
*Input*
```c++
5
1 2 3 1 2
3 1 2 2 1
```
    
*Output*
```c++
1
3
```
    
#### Hướng dẫn
    
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
        
#### [Code](https://ideone.com/XvOmUc)


-----------

### D. ADN
Một trong những nhiệm vụ của phân tích gen di truyền là so sánh độ giống nhau của 2 chuỗi ADN.

Chuỗi ADN đó là xâu chỉ chứa các ký tự từ tập {A, G, C, T}. Khi so sánh người ta có thể đẩy vòng tròn các ký tự trong chuỗi ADN. 

Mục tiêu của so sánh là tìm đoạn ADN dài nhất giống nhau ở 2 xâu bao gồm các ký tự liên tiếp.
Độ dài đoạn giống nhau này được gọi là độ giống nhau của 2 chuỗi.

Yêu cầu: Cho 2 chuỗi ADN có độ dài giống nhau và không vượt quá 50 000. Hãy xác định độ giống
nhau của 2 chuỗi.

**Input**

Gồm 2 dòng, mỗi dòng chứa một chuỗi ADN.

**Output**

Một số nguyên – độ giống nhau của 2 chuỗi

**Example**

*Input*
```c++
ACAGTG
AGTGTC
```

*Output*
```c++
5
```

*Note*

Giải thích: 2 xâu sau đẩy vòng là ACAGTG và TCAGTG

#### Hướng dẫn

Nhận thấy xâu cho trước có thể đẩy vòng tròn, nên ta quy xâu cho trước về dạng gấp đôi: a = a + a và b = b + b

Sử dụng kĩ thuật tìm kiếm nhị phân:

- Quy về bài toán tìm result sao cho result là xâu con liên tiếp chung dài nhất của cả hai xâu
- xét k và xét 1 xâu độ dài (result + 1 << k) có thỏa mãn hay không ?
- Nếu (result + 1 << k) là một xâu thỏa mãn kết quả : result += (1 << k)
- Lần lượt tìm đến k-1, k-2... 0

Nhận xét: do tính chất 'chung' của hai xâu **giảm dần** khi 'độ dài tìm được' **tăng lên**
-> Bài toán có tính đơn điệu hàm số -> Tìm kiếm nhị phân

Sử dụng map để đánh dấu mã Hash nào đã xuất hiện ở xâu A

-> Xét xâu B, nếu mã Hash đã xuất hiện ở A, chứng tỏ kết quả res + (1 << k) thỏa mãn


# Warning

Nếu ta chỉ dùng 1 MOD, thì chúng ta sẽ không Accepted được bài toán (đúng khoảng 30% số test)

Tại sao ?

Trước tiên chúng ta cần phải quay về bài toán ngày sinh nhật: 
>! Trong một phòng có 75 người, xác suất để hai người có cùng ngày sinh xấp xỉ 100% (?!)

Phân tích: giả sử tất cả mọi người trong phòng đều có ngày sinh khác nhau đôi một

Nếu người thứ nhất sinh vào một ngày nào đó trong năm, thì người thứ 2 không thể sinh vào ngày đó

-> Xác suất để 2 người khác ngày sinh: (1 * (1 - 1/365)) * 100% 

-> Xác suất để 3 người khác ngày sinh: (1 * (1 - 1/365) * (1 - 2/365)) * 100%
...

Tương tự: xác suất để 75 người đều khác ngày sinh : ~ 0.1%

Trở về với bài toán, ta thấy rằng xác suất để có được hai mã Hash khác nhau trong 10^5 số từ 0->10^9, sẽ là một tỉ lệ rất nhỏ (tính toán cho thấy giá trị này đạt khoảng 18%) -> hiệu quả của thuật toán Hash không cao !

-> Nên dùng nhiều base hoặc nhiều MOD để giảm xác xuất Collision

#### [Code](https://ideone.com/ZE3GT0)
