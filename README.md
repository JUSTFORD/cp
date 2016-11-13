#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<assert.h>
/*
char const *find_char(char const *src, char const *str)           //cp 06-01 �����׸��ַ�
{
	if (src == NULL || str == NULL)
	{
		return NULL;
	}

	char const *tmp = src;
	char const *s = str;
	
	while (*tmp != 0)
	{
		s = str;
		while (*s != 0)
		{
			if (*s == *tmp)
			{
				return tmp;
			}
			s++;
		}
		tmp++;
	}
	return NULL;
}


int del_substr(char *str, char const *substr)  //cp 06-02   �ַ���ɾ���Ӵ�
{
	if (str == NULL)
	{
		return 0;
	}
	if (substr == NULL)
	{
		return 1;
	}

	char *s = str;
	char *s1 = s;
	char const *p = substr;
	

	while (*s != 0)
	{
		p = substr;
		if (*s == *p)
		{
			s1 = s;
			while (*p == *s1)
			{
				p++;
				s1++;
			}
			if (*p != 0)
			{
				s++;
				continue;
			}
			else
			{
				
				while (*s++ = *s1++);
				
				return 1;
			}
		}
		s++;
	}

	return 0;
}


void reverse_string(char *string)          //cp 06-03  �����ַ���
{
	if (string == NULL && *string==0)
	{	
		return;
	}
	char *tmp = string;
	while (*tmp != 0)tmp++;

	tmp--;

	char p;

	while (tmp > string)
	{
		p = *tmp;
		*tmp = *string;
		*string = p;
		tmp--;
		string++;
	}
}

int main()
{
	char s1[20] = "ABCDEF";
	char *s2 = "CD";

	//reverse_string(s1);
	//printf("%s\n",find_char(s1, s2));
	//printf("%d\n", del_substr(s1, s2));
	printf("%s\n", s1);
}
*/




char * big_num_add(char *s1, char *s2)
{
	int len1 = strlen(s1) + 1;
	int len2 = strlen(s2) + 1;

	char *str1 = (char *)malloc(sizeof(char)*len1);
	char *str2 = (char *)malloc(sizeof(char)*len2);
	char *rs = (char *)malloc(sizeof(char)*((len1 > len2 ? len1 : len2)+2));
	assert(rs != NULL);
	assert(str1 != NULL);
	assert(str2 != NULL);
	strcpy(str1, s1);
	strcpy(str2, s2);

	_strrev(str1);
	_strrev(str2);

	int bit = 0;
	char *start = rs;
	char*p1 = str1;
	char*p2 = str2;

	while (*p1&&*p2)
	{
 		*rs = *p1 + *p2 + bit - '0';

		if (*rs > '9')
		{
			bit = 1;
			*rs -= 10;
		}
		else
		{
			bit = 0;
		}
		
		p1++;
		p2++;
		rs++;
	}

	while (*p1)
	{
		*rs = *p1 + bit;
		if (*rs > '9')
		{
			bit = 1;
			*rs -= 10;
		}
		else
		{
			bit = 0;
		}
		rs++;
		p1++;
	}
	while (*p2)
	{
		*rs = *p2 + bit;
		if (*rs > '9')
		{
			bit = 1;
			*rs -= 10;
		}
		else
		{
			bit = 0;
		}
		rs++;
		p2++;
	}
	if (bit != 0)
	{
		*rs = '1';
		rs++;
	}

	*rs = 0;
	_strrev(start);
	free(str1);
	free(str2);
	return start;
}


char *big_num_sub(char *s1, char *s2)
{
	int len1 = strlen(s1) + 1;
	int len2 = strlen(s2) + 1;

	char *str1 = (char *)malloc(sizeof(char)*len1);
	char *str2 = (char *)malloc(sizeof(char)*len2);
	char *rs = (char *)malloc(sizeof(char)*((len1 > len2 ? len1 : len2) + 2));
	assert(rs != NULL);
	assert(str1 != NULL);
	assert(str2 != NULL);

	
	strcpy(str1, s1);
	strcpy(str2, s2);


	_strrev(str1);
	_strrev(str2);

	int bit = 0;
	char *start = rs;
	char*p1 = str1;
	char*p2 = str2;

	while (*p1 && *p2)
	{
		*rs = *p1 - *p2 + '0' - bit;
		if (*rs < '0')
		{
			*rs += 10;
			bit = 1;
		}
		else
		{
			bit = 0;
		}
		*rs++;
		*p1++;
		*p2++;
	}

	while (*p1)
	{
		*rs = *p1 - bit;
		if (*rs < '0')
		{
			*rs += 10;
			bit = 1;
		}
		else
		{
			bit = 0;
		}
		*rs++;
		*p1++;
	}

	*rs = 0;

	_strrev(start);
	free(str1);
	free(str2);

	return start;



}



int main(int argc,char *argv[])
{
	

	/*char *sum=NULL;                    //�������ӷ�  ֧�ֶ����������� 
	char s3[20] = "";
	for (int i = 1; i < argc; i++)
	{
		sum = big_num_add(s3, argv[i]);
		strcpy(s3, sum);
		free(sum);
	}

	printf("%s\n", s3);*/
	

	/*
	char s1[] = "9000000";
	char s2[] = "111";
	
	char *s3 = big_num_sub(s1, s2);     //����������  
	printf("%s\n", s3);
	free(s3);*/

	/*char *s3;                          //�������Ӽ� ֧�ַ��� 
	switch (*argv[1])
	{
	case '+':s3 = big_num_add(argv[2], argv[3]); break;
	case '-':s3 = big_num_sub(argv[2], argv[3]); break;
	default:printf("��������%s\n", argv[1]); exit(-1);
		
	}
	printf("result = %s\n", s3);
	free(s3);*/
	return 0;
}


/*
void check(char *s)    //cp 01-3   �ַ�У����
{
char check = -1;
while (*s)
{
check += *s;
s++;
}
check += '\n';
printf("%d\n", check);

}

int main()
{
char s[] = "0000000013215";
check(s);
return 0;
}*/
