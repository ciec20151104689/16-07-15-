```c
#include "stdafx.h"
#include "stdlib.h"
#include "string.h"

int _tmain()
{
	FILE *fp, *fp1;
	char *docu;
	char lat[20];
	char lon[20];
	char date[20];
	char time[20];
	int  len, i = 0;
	if   ((fp = fopen("d:\\export.gpx", "r")) == 0)
	{
		printf("文件不能正常打开");
		return(-1);
	}
	fp1      = fopen ("d:\\export.csv", "w") ;
    fseek    (fp , 0 ,SEEK_END);       
    len      = ftell ( fp ) ;                   //
    docu     = ( char * ) malloc (len );
	printf   ("len=%d\n", len);
	fseek    (fp, 0 , SEEK_SET);
	fread    (docu, 1 , len , fp );             //
	docu     [ len ] = '\0' ;
	fprintf  (fp1, "纬度 ,经度 ,日期 ,时间\n");

	while (!(docu[i] == '<' && docu[i + 1] == '/' && docu[i + 2] == 'g' && docu[i + 3] == 'p' && docu[i + 4] == 'x' && docu[i + 5] == '>'))
	{
		if (docu[i] == ' '&&docu[i + 1] == 'l'&&docu[i + 2] == 'a'&&docu[i + 3] == 't')
		{
			strncpy(lat, &docu[i + 6], 9);
			strncpy(lon, &docu[i + 22], 10);
			strncpy(date, &docu[i + 44], 10);
			strncpy(time, &docu[i + 55], 10);
			lat[9] = '\0';
			lon[10] = '\0';
			date[10] = '\0';
			time[8] = '\0';
			fprintf(fp1, "%s,%s,%s,%s\n", lat, lon, date, time);
			printf("%s,%s,%s,%s\n", lat, lon, date, time);
		}
		i++;
	}
	fclose(fp);
	fclose(fp1);
	free(docu);
	return 0;
}
```
