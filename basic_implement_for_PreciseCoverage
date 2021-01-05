// exercise_01.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//
#include<string.h>
#include<cstdio>
#include<iostream>
#include<cstring>
#define clr(x) memset(x, 0, sizeof(x))
#define clrlow(x) memset(x, -1, sizeof(x))
#define maxnode 1001010
#define maxn    1010
using namespace std;
struct DLX {
	int n, m;
	int U[maxnode], D[maxnode], L[maxnode], R[maxnode], col[maxnode], row[maxnode];
	int H[maxn];
	int ansed, ans[maxn], size;
	void init(int _n, int _m)
	{
		n = _n;
		m = _m;
		for (int i = 0; i <= m; i++)
		{
			U[i] = i;
			D[i] = i;
			L[i] = i - 1;
			R[i] = i + 1;
			col[i] = i;
			row[i] = 0;
		}
		L[0] = m;
		R[m] = 0;
		size = m;
		clrlow(H);
		clr(ans);
		ansed = 0;
		return;
	}
	void push(int r, int c)
	{
		size++;
		D[size] = D[c];
		U[size] = c;
		U[D[c]] = size;
		D[c] = size;
		row[size] = r;
		col[size] = c;
		if (H[r] < 0)
		{
			H[r] = size;
			R[size] = L[size] = size;
		}
		else
		{
			L[size] = H[r];
			R[size] = R[H[r]];
			L[R[H[r]]] = size;
			R[H[r]] = size;
		}
	}
	void del(int c)
	{
		R[L[c]] = R[c];
		L[R[c]] = L[c];
		for (int i = D[c]; i != c; i = D[i])
			for (int j = R[i]; j != i; j = R[j])
			{
				D[U[j]] = D[j];
				U[D[j]] = U[j];
			}
		return;
	}
	void reback(int c)
	{
		for (int i = U[c]; i != c; i = U[i])
			for (int j = L[i]; j != i; j = L[j])
			{
				D[U[j]] = j;
				U[D[j]] = j;
			}
		R[L[c]] = c;
		L[R[c]] = c;
		return;
	}
	bool dancing(int dep)
	{
		if (R[0] == 0)
		{
			ansed = dep;
			return true;
		}
		int c = R[0];
		del(c);
		for (int i = D[c]; i != c; i = D[i])
		{
			ans[dep] = row[i];
			for (int j = R[i]; j != i; j = R[j])
				del(col[j]);
			if (dancing(dep + 1))
				return true;
			for (int j = L[i]; j != i; j = L[j])
				reback(col[j]);
		}
		return false;
	}

}dlx;
int main()
{
	int n, m, p, k;
	while (scanf_s("%d%d", &n, &m) == 2)
	{
		dlx.init(n, m);
		for (int i = 1; i <= n; i++)
		{
			scanf_s("%d", &p);
			for (int j = 1; j <= p; j++)
			{
				scanf_s("%d", &k);
				dlx.push(i, k);
			}
		}
		printf("NO(default)\n");
		if (!dlx.dancing(0)) {
			printf("NO\n");
		}
		else
		{
			printf("%d", dlx.ansed);
			for (int i = 0; i < dlx.ansed; i++)
				printf(" %d", dlx.ans[i]);
			printf("\n");
		}
	}
	return 0;
}


