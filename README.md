import pandas as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

credited_card_df = pd.read_csv('/content/creditcard.csv')
credited_card_df.head()

Time	V1	V2	V3	V4	V5	V6	V7	V8	V9	...	V21	V22	V23	V24	V25	V26	V27	V28	Amount	Class
count	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	...	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61491.000000	61490.000000	61490.000000
mean	32315.344034	-0.237271	-0.009245	0.686906	0.170027	-0.262238	0.102613	-0.115160	0.057488	0.053122	...	-0.028080	-0.107424	-0.040104	0.005970	0.136116	0.020139	0.002365	0.004510	95.434437	0.002651
std	13799.588573	1.858811	1.650873	1.437527	1.382308	1.387481	1.305512	1.246739	1.191802	1.178365	...	0.721260	0.636939	0.592219	0.596774	0.438555	0.498542	0.382815	0.323475	268.645764	0.051418
min	0.000000	-56.407510	-72.715728	-32.965346	-5.172595	-42.147898	-26.160506	-26.548144	-41.484823	-9.283925	...	-20.262054	-10.933144	-26.751119	-2.836627	-7.495741	-2.534330	-8.567638	-9.617915	0.000000	0.000000
25%	26758.500000	-0.994568	-0.583205	0.201620	-0.725042	-0.881361	-0.636372	-0.604834	-0.144080	-0.654524	...	-0.228062	-0.527888	-0.179959	-0.325959	-0.128081	-0.329703	-0.063341	-0.006118	7.680000	0.000000
50%	36064.000000	-0.244368	0.075028	0.778314	0.184554	-0.295113	-0.150753	-0.074302	0.063124	-0.048761	...	-0.063048	-0.082467	-0.052011	0.061264	0.173929	-0.075671	0.009102	0.022644	26.000000	0.000000
75%	42644.000000	1.154727	0.731859	1.411352	1.052198	0.276515	0.492695	0.424238	0.339268	0.718936	...	0.113660	0.308504	0.078764	0.402787	0.422744	0.297594	0.082455	0.076347	87.680000	0.000000
max	49863.000000	1.960497	18.183626	4.101716	16.715537	34.801666	22.529298	36.677268	20.007208	10.392889	...	22.614889	5.805795	17.297845	4.014444	5.525093	3.517346	11.135740	33.847808	19656.530000	1.000000
8 rows × 31 columns

Class
0.0    61327
1.0      163
Name: count, dtype: int64
(61491, 31)
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 61491 entries, 0 to 61490
Data columns (total 31 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   Time    61491 non-null  int64  
 1   V1      61491 non-null  float64
 2   V2      61491 non-null  float64
 3   V3      61491 non-null  float64
 4   V4      61491 non-null  float64
 5   V5      61491 non-null  float64
 6   V6      61491 non-null  float64
 7   V7      61491 non-null  float64
 8   V8      61491 non-null  float64
 9   V9      61491 non-null  float64
 10  V10     61491 non-null  float64
 11  V11     61491 non-null  float64
 12  V12     61491 non-null  float64
 13  V13     61491 non-null  float64
 14  V14     61491 non-null  float64
 15  V15     61491 non-null  float64
 16  V16     61491 non-null  float64
 17  V17     61491 non-null  float64
 18  V18     61491 non-null  float64
 19  V19     61491 non-null  float64
...
 29  Amount  61490 non-null  float64
 30  Class   61490 non-null  float64
dtypes: float64(30), int64(1)
memory usage: 14.5 MB
Output is truncated. View as a scrollable element or open in a text editor. Adjust cell output settings...
Time	V1	V2	V3	V4	V5	V6	V7	V8	V9	...	V21	V22	V23	V24	V25	V26	V27	V28	Amount	Class
0	0	-1.359807	-0.072781	2.536347	1.378155	-0.338321	0.462388	0.239599	0.098698	0.363787	...	-0.018307	0.277838	-0.110474	0.066928	0.128539	-0.189115	0.133558	-0.021053	149.62	0.0
1	0	1.191857	0.266151	0.166480	0.448154	0.060018	-0.082361	-0.078803	0.085102	-0.255425	...	-0.225775	-0.638672	0.101288	-0.339846	0.167170	0.125895	-0.008983	0.014724	2.69	0.0
2	1	-1.358354	-1.340163	1.773209	0.379780	-0.503198	1.800499	0.791461	0.247676	-1.514654	...	0.247998	0.771679	0.909412	-0.689281	-0.327642	-0.139097	-0.055353	-0.059752	378.66	0.0
3	1	-0.966272	-0.185226	1.792993	-0.863291	-0.010309	1.247203	0.237609	0.377436	-1.387024	...	-0.108300	0.005274	-0.190321	-1.175575	0.647376	-0.221929	0.062723	0.061458	123.50	0.0
4	2	-1.158233	0.877737	1.548718	0.403034	-0.407193	0.095921	0.592941	-0.270533	0.817739	...	-0.009431	0.798278	-0.137458	0.141267	-0.206010	0.502292	0.219422	0.215153	69.99	0.0
5 rows × 31 columns

(163, 31)
(61327, 31)
