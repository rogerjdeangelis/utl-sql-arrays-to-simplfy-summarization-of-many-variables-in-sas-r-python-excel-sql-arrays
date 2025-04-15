# utl-sql-arrays-to-simplfy-summarization-of-many-variables-in-sas-r-python-excel-sql-arrays
sql arrays to simplfy summarization of many variables in sas r python excel sql
    %let pgm=utl-sql-arrays-to-simplfy-summarization-of-many-variables-in-sas-r-python-excel-sql-arrays;

    sql arrays to simplfy summarization of many variables in sas r python excel sql

       CONTENTS

          1 sas sql
          2 r sql
          3 excel sql
          4 python sql not done
          5 related repos


    github
    https://tinyurl.com/3uv9sbhw
    https://github.com/rogerjdeangelis/utl-sql-arrays-to-simplfy-summarization-of-many-variables-in-sas-r-python-excel-sql-arrays

    communities.sas
    https://tinyurl.com/4rxt64ts
    https://communities.sas.com/t5/SAS-Programming/How-to-pass-macro-variable-in-Proc-SQL-functions/m-p/831584#M328627

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */
                                                                                                                              */
    /**************************************************************************************************************************/
    /*            INPUT                    |          PROCESS                             |          OUTPUT                   */
    /*            =====                    |          =======                             |           ======                  */
    /*                                     |                                              |                                   */
    /* SEX    AGE    HEIGHT    WEIGHT      | 1 SAS SQL                                    | ROWS SEX MAGE MHEIGHT MWEIGHT     */
    /*                                     | =========                                    |                                   */
    /*  M      14     69.0      112.5      |                                              |  1    F  13.4  61.38    96.3      */
    /*  F      13     56.5       84.0      | %array(_vrs,values=                          |  2    M  13.0  62.26    96.3      */
    /*  F      13     65.3       98.0      |  %utl_varlist(sd1.have,keep=_numeric_));     |                                   */
    /*  F      14     62.8      102.5      |                                              |                                   */
    /*  M      14     63.5      102.5      | proc sql;                                    |                                   */
    /*  M      12     57.3       83.0      |   create                                     |                                   */
    /*  F      12     59.8       84.5      |      table want as                           |                                   */
    /*  F      15     62.5      112.5      |   select                                     |                                   */
    /*  M      13     62.5       84.0      |      sex                                     |                                   */
    /*  M      12     59.0       99.5      |      ,%do_over(_vrs,phrase=avg(?) as m?      |                                   */
    /*                                     |       ,between=comma)                        |                                   */
    /* options validvarname=upcase;        |   from                                       |                                   */
    /* libname sd1 "d:/sd1";               |      sd1.have                                |                                   */
    /* data sd1.have;                      |   group                                      |                                   */
    /*   set sashelp.class(obs=10);        |      by sex                                  |                                   */
    /*   keep sex age weight height;       | ;quit;                                       |                                   */
    /* run;quit;                           |                                              |                                   */
    /*                                     |----------------------------------------------------------------------------------*/
    /*                                     |                                              |                                   */
    /*                                     | 2-3 r excel sql (see below for excel)        |  R                                */
    /*                                     | ======================================       |    SEX mAGE mHEIGHT mWEIGHT       */
    /*                                     |                                              |                                   */
    /*                                     | %utl_rbeginx;                                |  1   F 13.4   61.38    96.3       */
    /*                                     | parmcards4;                                  |  2   M 13.0   62.26    96.3       */
    /*                                     | library(haven)                               |                                   */
    /*                                     | library(sqldf)                               | SAS                               */
    /*                                     | library(dplyr)                               |                                   */
    /*                                     | source("c:/oto/fn_tosas9x.R")                | ROWS SEX MAGE MHEIGHT MWEIGHT     */
    /*                                     | have<-read_sas("d:/sd1/have.sas7bdat")       |                                   */
    /*                                     | have                                         |  1    F  13.4  61.38    96.3      */
    /*                                     | numname <- have %>%                          |  2    M  13.0  62.26    96.3      */
    /*                                     |   select_if(is.numeric) %>%                  |                                   */
    /*                                     |   names()                                    |                                   */
    /*                                     | numname                                      |                                   */
    /*                                     | phrases <- paste(sprintf(                    |                                   */
    /*                                     |     ",avg(%1$s) as m%1$s"                    |                                   */
    /*                                     |      ,numname                                |                                   */
    /*                                     |     ),collapse=' ')                          |                                   */
    /*                                     | str(phrases)                                 |                                   */
    /*                                     | want<-sqldf(paste(                           |                                   */
    /*                                     |   'select sex'                               |                                   */
    /*                                     |   ,phrases                                   |                                   */
    /*                                     |   ,'from have group by sex'))                |                                   */
    /*                                     | want                                         |                                   */
    /*                                     | fn_tosas9x(                                  |                                   */
    /*                                     |       inp    = want                          |                                   */
    /*                                     |      ,outlib ="d:/sd1/"                      |                                   */
    /*                                     |      ,outdsn ="want"                         |                                   */
    /*                                     |      )                                       |                                   */
    /*                                     | ;;;;                                         |                                   */
    /*                                     | %utl_rendx;                                  |                                   */
    /*                                     |                                              |                                   */
    /*************************************************************************************************************************

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      set sashelp.class(obs=10);
      keep sex age weight height;
    run;quit;


    /**************************************************************************************************************************/
    /* SEX    AGE    HEIGHT    WEIGHT                                                                                         */
    /*                                                                                                                        */
    /*  M      14     69.0      112.5                                                                                         */
    /*  F      13     56.5       84.0                                                                                         */
    /*  F      13     65.3       98.0                                                                                         */
    /*  F      14     62.8      102.5                                                                                         */
    /*  M      14     63.5      102.5                                                                                         */
    /*  M      12     57.3       83.0                                                                                         */
    /*  F      12     59.8       84.5                                                                                         */
    /*  F      15     62.5      112.5                                                                                         */
    /*  M      13     62.5       84.0                                                                                         */
    /*  M      12     59.0       99.5                                                                                         */
    /**************************************************************************************************************************/

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */

    %array(_vrs,values=
     %utl_varlist(sd1.have,keep=_numeric_));

    proc sql;
      create
         table want as
      select
         sex
         ,%do_over(_vrs,phrase=avg(?) as m?
          ,between=comma)
      from
         sd1.have
      group
         by sex
    ;quit;


    /**************************************************************************************************************************/
    /* Obs    SEX    MAGE    MHEIGHT    MWEIGHT                                                                               */
    /*                                                                                                                        */
    /*  1      F     13.4     61.38       96.3                                                                                */
    /*  2      M     13.0     62.26       96.3                                                                                */
    /**************************************************************************************************************************/

    /*___                     _
    |___ \   _ __   ___  __ _| |
      __) | | `__| / __|/ _` | |
     / __/  | |    \__ \ (_| | |
    |_____| |_|    |___/\__, |_|
                           |_|
    */
    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(sqldf)
    library(dplyr)
    source("c:/oto/fn_tosas9x.R")
    have<-read_sas("d:/sd1/have.sas7bdat")
    have
    numname <- have %>%
      select_if(is.numeric) %>%
      names()
    numname
    phrases <- paste(sprintf(
        ",avg(%1$s) as m%1$s"
         ,numname
        ),collapse=' ')
    str(phrases)
    want<-sqldf(paste(
      'select sex'
      ,phrases
      ,'from have group by sex'))
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /* R                           |  SAS                                                                                     */
    /*   SEX mAGE mHEIGHT mWEIGHT  |  ROWNAMES    SEX    MAGE    MHEIGHT    MWEIGHT                                           */
    /*                             |                                                                                          */
    /* 1   F 13.4   61.38    96.3  |      1        F     13.4     61.38       96.3                                            */
    /* 2   M 13.0   62.26    96.3  |      2        M     13.0     62.26       96.3                                            */
    /**************************************************************************************************************************/

    /*____                     _             _
    |___ /    _____  _____ ___| |  ___  __ _| |
      |_ \   / _ \ \/ / __/ _ \ | / __|/ _` | |
     ___) | |  __/>  < (_|  __/ | \__ \ (_| | |
    |____/   \___/_/\_\___\___|_| |___/\__, |_|
                                          |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utlfkil(d:/xls/wantxl.xlsx);

    %utl_rbeginx;
    parmcards4;
    library(openxlsx)
    library(sqldf)
    library(haven)
    have<-read_sas("d:/sd1/have.sas7bdat")
    wb <- createWorkbook()
    addWorksheet(wb, "have")
    writeData(wb, sheet = "have", x = have)
    saveWorkbook(
        wb
       ,"d:/xls/wantxl.xlsx"
       ,overwrite=TRUE)
    ;;;;
    %utl_rendx;

    %utl_rbeginx;
    parmcards4;
    library(openxlsx)
    library(sqldf)
    library(dplyr)
    source("c:/oto/fn_tosas9x.R")
     wb<-loadWorkbook("d:/xls/wantxl.xlsx")
     have<-read.xlsx(wb,"have")
     addWorksheet(wb, "want")
    numname <- have %>% select_if(is.numeric) %>% names()
    numname
     phrases <- paste(sprintf(
        ",avg(%1$s) as m%1$s"
         ,numname
        ),collapse=' ')
     want<-sqldf(paste(
      'select sex'
      ,phrases
      ,'from have group by sex'))
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /* -----------------------+                                                                                               */
    /* | A1| fx    |  SEX     |                                                                                               */
    /* ---------------------------------------------+                                                                         */
    /* [_] |    A     |    B    |    C    |    D    |                                                                         */
    /* ---------------------------------------------|                                                                         */
    /*  1  |   SEX    |   AGE   | HEIGHT  | WEIGHT  |                                                                         */
    /*  -- |----------+---------+---------+---------|                                                                         */
    /*  2  |F         | 13.4    | 61.38   | 96.3    |                                                                         */
    /*  -- |----------+---------+---------+---------|                                                                         */
    /*  3  |M         | 13      | 62.26   | 96.3    |                                                                         */
    /*  -- |----------+---------+---------+---------|                                                                         */
    /* [WANT]                                                                                                                 */
    /**************************************************************************************************************************/

    /*  _              _       _      _
    | || |    _ __ ___| | __ _| |_ __| |  _ __ ___ _ __   ___  ___
    | || |_  | `__/ _ \ |/ _` | __/ _` | | `__/ _ \ `_ \ / _ \/ __|
    |__   _| | | |  __/ | (_| | || (_| | | | |  __/ |_) | (_) \__ \
       |_|   |_|  \___|_|\__,_|\__\__,_| |_|  \___| .__/ \___/|___/
                                                  |_|
    */;

    REPO
    ------------------------------------------------------------------------------------------------------------------------------
    https://github.com/rogerjdeangelis/utl-complex-join-of-seven-tables-left-self-join-using-sql-arrays
    https://github.com/rogerjdeangelis/utl-computing-counts-using-sql-arrays
    https://github.com/rogerjdeangelis/utl-computing-maxs-and-mins-of-all-numeric-and-character-variables-using-sql-arrays
    https://github.com/rogerjdeangelis/utl-pivot-long-pivot-wide-transpose-partitioning-sql-arrays-wps-r-python
    https://github.com/rogerjdeangelis/utl-simple-example-of-sql-array
    https://github.com/rogerjdeangelis/utl-simplifying-repetitive-code-using-sql-arrays-and-Barts-array-macro
    https://github.com/rogerjdeangelis/utl-sql-arrays-for-very-fast-in-database-processing
    https://github.com/rogerjdeangelis/utl-stack-columns-and-count-values-using-with-and-without-sql-arrays-in-sas-r-and-python
    https://github.com/rogerjdeangelis/utl-transpose-pivot-wide-to-long-using-sql-arrays-in-sas-r-and-python
    https://github.com/rogerjdeangelis/utl-transposing-and-summarizing-by-group-using-sql-arrays
    https://github.com/rogerjdeangelis/utl-transposing-multiple-variables-using-transpose-macro-sql-arrays-proc-report
    https://github.com/rogerjdeangelis/utl-transposing-pivoting-minimums-using-sql-arrays
    https://github.com/rogerjdeangelis/utl-using-sql-arrays-and-do_over-to-cast_0_1-to-Y-N
    https://github.com/rogerjdeangelis/utl-using-sql-arrays-substract-the-values-in-row2-row4-from-row1-by-column
    https://github.com/rogerjdeangelis/utl-using-sql-arrays-to-implement-datastep-variable-ranges
    https://github.com/rogerjdeangelis/utl-very-fast-processing-using-sql-arrays-on-large-core-systems

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
