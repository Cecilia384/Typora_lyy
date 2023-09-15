

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=4e5+5;
int a[N],b[N],c[N],n,an[N];
int main()
{
	scanf("%d",&n);
	for(int i=1;i<=n;i++)
	scanf("%d",&a[i]),b[a[i]]++;
	int ct=0;
	for(int i=1;i<=n;i++)
	{
		if(b[i]==0)
		c[++ct]=i;
	}
	if(n==1)
	{
		printf("-1");
		return 0;
	}
	if(ct==0)
	{
		printf("%d\n",n+2);
		printf("%d %d ",a[2],a[1]);
		for(int i=3;i<=n;i++)
		b[i-2]=a[i];
		b[n]=a[2];
		b[n-1]=a[2];
		for(int i=1;i<=n;i++)
		a[i]=b[i],b[i]=0;
		for(int i=1;i<=n;i++)
		b[a[i]]++;
		for(int i=1;i<=n;i++)
		{
			if(b[i]==0)
			c[++ct]=i;
		}
	}
	else
	{
		printf("%d\n",n);
	}
	int k=0,j=0;
	printf("%d ",c[++k]);
	for(int i=1;i<n;i++)
	{
		if(b[a[i]]==2)
		{
			b[a[i]]++;
			j=i;
			break;
		}
		else
		{
			printf("%d ",a[i]);
		}
	}
	for(int i=j;i<n;i++)
	{
		if(b[a[i+1]]==2)
		{
			b[a[i+1]]++;
			printf("%d ",c[++k]);
		}
		else if(b[a[i+1]]==3)
		{
			printf("%d ",c[k--]);
		}
		else
		{
			printf("%d ",a[i]);
		}
	}
}
```

