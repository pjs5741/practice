```
#include <iostream>

using namespace std;

void Input_Data(int *money, int *type, int *num);		//금액, 음료 종류, 수량을 입력하는 함수
int Compute_Total(int type, int num);		//총액을 계산하는 함수
char Check_Money(int total, int *money);		//금액 체크 함수
void Print_Result(char selection, int total, int money, int type, int num);		//결과 출력 함수

int main()
{
	char selection;
	int money, type, num, wanted_total, Last_total;
	do
	{
		cout << "==================================음료 자판기==============+++==============================" << endl;
		cout << "1. 생수 : 500원\t\t 2.사이다 : 800원\t\t3.옥수수차: 1200원" << endl;
		cout << "============================================================================================" << endl;
		Input_Data(&money, &type, &num);
		wanted_total = Compute_Total(type, num);
		wanted_total;
		Last_total = Check_Money(wanted_total, &money);
		Last_total;
		Print_Result(Last_total, wanted_total, money, type, num);

		cout << "\n음료수를 더 뽑겠습니까?(Y/N):";
		cin >> selection;

		while (selection != 'Y' && selection != 'y' && selection != 'N' && selection != 'n')
		{
			cout << "오직 Y,y,N,n만 입력하세요:";
			cin >> selection;
		}
		if (selection == 'N' || selection == 'n')
		{
			cout << "이용해 주셔서 감사합니다.\n";
		}
	} while (selection == 'Y' || selection == 'y');

	return 0;
}

void Input_Data(int *money, int *type, int *num)
{
	cout << "돈을 넣어 주세요 :";
	cin >> *money;
	cout << "음료 선택 및 수량:";
	cin >> *type >> *num;
}

int Compute_Total(int type, int num)
{
	int wanted_total = 0;
	switch (type)
	{
	case 1:
		wanted_total = 500 * num;
		break;
	case 2:
		wanted_total = 800 * num;
		break;
	case 3:
		wanted_total = 1200 * num;
		break;
	default:
		break;
	}
	return  wanted_total;
}

char Check_Money(int total, int *money)
{
	char selection = 0;
	int j;
	while (total > *money)
	{

		cout << "금액이" << total - *money << "원 부족합니다. 돈을 더 투입하시겠습니까? (Y/N)";
		cin >> selection;

		if (selection != 'Y' && selection != 'y' && selection != 'N' && selection != 'n')
		{
			cout << "오직 Y,y,N,n만 입력하시오. :";
			cin >> selection;
		}
		if (selection == 'Y' || selection == 'y')
		{
			cout << "추가 투입금:";
			cin >> j;
			*money += j;

		}
		else if (selection == 'N' || selection == 'n')
		{
			break;
		}


	}
	return selection;
}

void Print_Result(char selection, int total, int money, int type, int num)
{
	const char *arry[] = { { "생수" },{ "사이다" },{ "옥수수차" } };

	if (selection == 'y' || selection == 'Y')
	{
		if (total <= money)
		{
			cout << "현재 금액 :" << money << endl;
			cout << arry[type - 1] << num << "개와 잔돈" << money - total << "원을 받으십시오.\n\n";
		}
	}
	else if (selection == 'N' || selection == 'n')
	{
		cout << "투입하신 금액이 부족하여 판매가 취소되었습니다.\n" << "투입하신돈" << money << "원을 받으십시오\n\n";
	}
	else if (total <= money)
	{
		cout << "현재 금액 :" << money << endl;
		cout << arry[type - 1] << num << "개와 잔돈" << money - total << "원을 받으십시오.\n\n";
	}
}

```

![1](https://user-images.githubusercontent.com/48274630/159153503-b10b7fed-4f25-473b-8446-95d2a01d8641.png)
