# SAS-project princomp analysis
/*涵盖了成分评分矩阵，成分模式概略，陡坡图，已解释方差图形*/
/* 生成代码 (IMPORT) */
/* 源文件: iris.csv */
/* 源路径: /home/wlx5210/sasuser.v94 */
/* 代码生成日期: 18/10/21 下午2:15 */

%web_drop_table(iris);
FILENAME REFFILE '/home/wlx5210/sasuser.v94/iris.csv';
PROC IMPORT DATAFILE=REFFILE
	DBMS=CSV
	OUT=iris;
	GETNAMES=YES;
RUN;
PROC CONTENTS DATA=iris; RUN;
%web_open_table(iris);

/*proc princomp cov score */
ods graphics on;
title 'principal component analysis';
proc princomp data=iris cov plots=score(ellipse);  
run;
ods graphics off;

/*proc princomp patternprofile */
ods graphics on;
proc princomp data=iris n=3 out=PCiris standard 
                 plots=patternprofile;
run;
ods graphics off; 

/*plot the 3th components*/
ods graphics on;
proc princomp data=iris
                 plots(ncomp=3)=all n=5;
run;
ods graphics off;




