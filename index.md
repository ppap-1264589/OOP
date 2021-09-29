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

```c+
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
