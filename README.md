# SQL Zoo Module Feedback 🧑‍🎓 
Data and Questions Source: [https://sqlzoo.net/wiki/Guest_House](https://sqlzoo.net/wiki/Module_Feedback)

Solutions written using MySQL

<img width="755" height="626" alt="image" src="https://github.com/user-attachments/assets/bebaf8f7-6248-418a-8c16-bb66a113fd85" />


 <br>
 <br>
  
### Easy Questions

 <br>
1. Find the student name from a matriculation number
 <br>
 
```sql
SELECT SPR_FNM1, SPR_SURN
FROM INS_SPR
WHERE SPR_CODE='50200100'
```
Result
|SPR_FNM1	|SPR_SURN|
|----|--------|
|Tom|Cotton|

 <br>
 
2. Show the module code and module name for modules studied by the student with number 50200100 in session 2016/7 TR1

```sql
SELECT INS_MOD.MOD_CODE, INS_MOD.MOD_NAME
FROM CAM_SMO
LEFT JOIN INS_MOD ON CAM_SMO.MOD_CODE = INS_MOD.MOD_CODE
WHERE SPR_CODE = 50200100 
AND AYR_CODE = '2016/7'
AND PSL_CODE = 'TR1'
```
Result
|MOD_CODE|MOD_NAME|
|-------|-------|
|CSN08101|Systems and Services|
|INF08104|Database Systems|
|SET08108|Software Development 2|


<br>
3. Show the module code and module name and details of the module leader for modules studied by the student with number 50200100 in session 2016/7 TR1

```sql
SELECT CAM_SMO.MOD_CODE, MOD_NAME, INS_MOD.PRS_CODE, PRS_FNM1, PRS_SURN
FROM CAM_SMO
LEFT JOIN INS_MOD ON INS_MOD.MOD_CODE = CAM_SMO.MOD_CODE
LEFT JOIN INS_PRS ON INS_PRS.PRS_CODE = INS_MOD.PRS_CODE
WHERE SPR_CODE =50200100 
AND AYR_CODE = '2016/7'
AND PSL_CODE = 'TR1'
```

Result
|MOD_CODE|MOD_NAME|PRS_CODE|PRS_FNM1|PRS_SURN|
|--------|--------|--------|--------|--------|
|CSN08101|Systems and Services|40000008|James|Jackson|
|INF08104|Database Systems|40000036|Andrew|Cumming|
|SET08108|Software Development 2|40000408|Neil|Urquhart|


<br>
5. Show the frequency chart for module SET08108 for question 4.1
   For each response 1-5 show the number of students who gave that response (Module SET08108, 2016/7, TR1)

```sql
SELECT MOD_CODE, RES_VALU, COUNT(DISTINCT SPR_CODE)
FROM INS_RES
WHERE MOD_CODE = 'SET08108'
   AND INS_RES.AYR_CODE='2016/7'
   AND INS_RES.PSL_CODE='TR1'
   AND INS_RES.QUE_CODE='4.1'
GROUP BY MOD_CODE, RES_VALU
```

Result

|MOD_CODE|MOD_NAME|RESPONSE_FREQ|
|--------|--------|--------|
|SET08108|1|5|
|SET08108|2|6|
|SET08108|3|5|
|SET08108|4|17|
|SET08108|5|28|











