# SAS-project
/*主成分分析能够帮助我们探索变量之间的潜在关系的维度，研究观测对象（如品牌或者个人）在这些不同维度上分布差异*/
/*在市场细分，品牌定位，CRM大型宽表的处理*/
/*技术关键点 因子旋转，biplot,screeplot,var_plot探索性因子分析EFA，验证性因子分析CFA,结构化因子分析*/
/*PCA Analysis */
/* 生成代码 (IMPORT) */
/* 源文件: iris.csv */
/* 源路径: /home/wlx5210/sasuser.v94 */
/* 代码生成日期: 18/10/21 下午1:17 */

%web_drop_table(iris);


FILENAME REFFILE '/home/wlx5210/sasuser.v94/iris.csv';

PROC IMPORT DATAFILE=REFFILE
	DBMS=CSV
	OUT=iris;
	GETNAMES=YES;
RUN;

PROC CONTENTS DATA=iris; RUN;
%web_open_table(iris);

/* Principal Component Analysis*/
title3 'Principal Component Analysis';
proc factor data=iris simple corr;
run;


/*Principal Factor Analysis*/
ods graphics on;  
title3 'Principal Factor Analysis with Promax Rotation';
proc factor data=iris 
      priors=smc msa residual 
      rotate=promax reorder
      outstat=fact_all 
      plots=(scree initloadings preloadings(vector) loadings);
run;
ods graphics off;

/*Harris-Kaiser Rotation*/
ods graphics on;
   title3 'Harris-Kaiser Rotation with Cureton-Mulaik Weights';
   proc factor data=iris rotate=hk norm=weight reorder
        plots=loadings;
run;
ods graphics off;

/*Maximum Likelihood Factor Analysis*/
title3 'Maximum Likelihood Factor Analysis with Three Factors';
proc factor data=iris method=ml heywood n=2;
run;

/*Using Confidence Intervals to Locate Salient Factor Loadings*/
title2 'A nine-variable-three-factor example';
proc factor data=iris method=ml reorder rotate=quartimin
      nobs=200 n=3 se cover=.45 alpha=.1;
run;












