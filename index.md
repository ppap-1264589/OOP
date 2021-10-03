# [Trang chủ](https://ppap-1264589.github.io/interesting-solution)

## Các bài toán
- A. Codefun - P20002
- B. Serie A
* Link download đề bài:
- [Codefun - P20002](https://codefun.vn/problems/P20002)
- [Serie A](https://github.com/ppap-1264589/OOP/files/7253729/SERIEA.pdf)

## Chi tiết

### A. Codefun - P20002

- Nhận xét: một bài toán OOP rất bình thường ✔️
- Thực tế thì giới hạn của n và m khá bé, nên ĐPT thuật toán ở đây O(n^2) cũng được
- Trên Codefun cũng có lời giải công khai bài này, và nó cũng khá đơn giản
- Đây là cách của mình

```c++
#include <iostream>
using namespace std;
string itemName[1001];
int Price[1001];
string itemBuy[1001];
int number[1001];
int Total = 0;
int ItemIndex[1001];
int PriceIndex[1001];
int Index = 0;
class Item{
public:
    void getStock(int n){
        for (int i = 0; i < n; i++){
            cin >> itemName[i] >> Price[i];
        }
    }
    void displayStock(int n){
        for (int i = 0; i < n; i++){
            cout << i+1 << " " << itemName[i] << " " << Price[i] << endl;
        }
    }
};

class Invoice{
public:
    void getInvoice(int m, int n){
        for (int i = 0; i < m; i++){
            cin >> itemBuy[i] >> number[i];
            for (int j = 0; j < n; j++){
                if (itemBuy[i] == itemName[j]){
                    ItemIndex[Index] = j;
                    PriceIndex[Index] = Price[j];
                    Index++;
                    break;
                }
            }
        }
    }
    void displayInvoice(int m){
        for (int i = 0; i < m; i++){
            cout << ItemIndex[i]+1 << " " << itemBuy[i] << " ";
            cout << number[i] << " " << number[i]*PriceIndex[i] << "\n";
        }
    }
    void getTotal(int m){
        for (int i = 0; i < m; i++){
            Total += number[i]*PriceIndex[i];
        }
        cout << Total;
    }
};

int main (){
    int n,m;
    Item Stock;
    Invoice Bill;
    cin >> n;
    Stock.getStock(n);
    cin >> m;
    Bill.getInvoice(m,n);
	
    cout << "In stock:" << endl;
    Stock.displayStock(n);
    cout << "Invoice:" << endl;
    Bill.displayInvoice(m);
    cout << "Total: ";
    Bill.getTotal(m);
}
```

### B. Serie A

- Với mỗi một Team, ta khởi tạo một class:

 	+) Gồm các tham số như : điểm, số bàn thắng, bàn thua,...
	
	+) Phương thức update tỉ số và điểm của Team
	
	+) Quy ước tính chất của toán tử '<' trong phép sort bảng điểm số
	
- Dùng map để đánh dấu tên các đội -> số

- Nên sử dụng nạp chồng toán tử để dễ thao tác với tập hợp các Team

```c++
#include <bits/stdc++.h>
#define Task "A"
using namespace std;

const int maxn = 1001;
map<string, int> m;
int cnt = 0;
int n;
string t1, t2;

class team {
public:
    string name;
    int match, score, win, lost, draw, goal, goaled;
    team(){
        match = win = lost = score = draw = goal = goaled = 0;
        cin >> name;
        m[name] = cnt++;
    };
    ~team(){};

public:
    friend ostream& operator << (ostream& os, team& t) {
        os << t.name << " " << t.match << " " << t.score << " ";
        os << t.win << " " << t.lost << " " << t.draw << " ";
        os << t.goal << " " << t.goaled << " " << t.goal - t.goaled << "\n";
        return os;
    } //nạp chồng toán tử cout

    void update(int goal, int goaled) {
        this->goal += goal;
        this->goaled += goaled;
        if (goal > goaled) {
            win++;
            score += 3;
        }
        else if (goal < goaled) lost++;
        else {
            score++;
            draw++;
        }
        this -> match++;
    }
    
    int w_l() {return goal - goaled;}
    
    friend bool operator < (team& l, team& t) {
        if (l.score != t.score) return l.score > t.score;
        if (l.w_l() != t.w_l()) return l.w_l() > t.w_l();
        if (l.goal != t.goal) return l.goal > t.goal;
        return l.name < t.name;
    } // nạp chồng toán tử '<' trong phép sort
};

int main() {
    cin >> n;
    vector<team> a(n);
    int ts1, ts2; // tỉ số
    while(cin >> t1 >> t2 >> ts1 >> ts2){
        a[m[t1]].update(ts1, ts2);
        a[m[t2]].update(ts2, ts1);
    }
    sort(a.begin(), a.end());
    for (auto i : a) cout << i;
}
```
