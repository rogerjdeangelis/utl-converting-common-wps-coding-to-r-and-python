# utl-converting-common-wps-coding-to-r-and-python
Converting common wps coding to r and python code 
    %let pgm=utl-converting-common-wps-coding-to-r-and-python;

    Converting common wps coding to r and python code

    All of the solutions below return either wps datasets or dataframes, except python native pivoting.

    github
    http://tinyurl.com/526bbdwf
    https://github.com/rogerjdeangelis/utl-converting-common-wps-coding-to-r-and-python

    You may need to do minor ajustments to fix slight syntactical differences for SQLLITE in R and Python.
    For instance, exponentiation uses '**' in Python and '^' in R
    Panda and R sqllite3 does not support regular expressions.
    Sqllite does support a form of wps 'index', like, contains and substr operations.

    TASKS ( SOLUTIONS FOR WPS, R AND PYTHON)

      0. regex loops and sql
      1. add columns
      2. loops
      3. functions
      4. subset rows
      5. drop keep columns
      6. sort ascending
      7. sort descending
      8. summarize weight by sex
      9. logical processing
     10. regular expressions ( no sqllite support for regex)
     11. pivot wide to long sql (may be slight variations amoung languages)
     12. pivot_long_to_wide sql
     13. pivot_long_to_wide no sql (no python solution)
           Python issue: could not coerce the pivoted output into a usable panda dataframe,my issue?)
     14. pivot_wide_to_long no sql (no python solution)
           Python issue: could not coerce the pivoted output into a usable panda dataframe,my issue?)
    %let pgm=utl-intergrating-traditional-languages-with-rusing-regex-loops-sql;

    Intergrating-traditional-languages-with-r-using-regex-loops-sql

    github
    http://tinyurl.com/526bbdwf
    https://github.com/rogerjdeangelis/utl-converting-common-wps-coding-to-r-and-python

    github
    https://tinyurl.com/59bx7me8
    https://github.com/rogerjdeangelis/utl-leveraging-your-knowledge-of-regular-expressions-to-wps-r-python-multi-language

    /*___                               _                                   _
     / _ \   _ __ ___  __ _  _____  __ | | ___   ___  _ __  ___   ___  __ _| |
    | | | | | `__/ _ \/ _` |/ _ \ \/ / | |/ _ \ / _ \| `_ \/ __| / __|/ _` | |
    | |_| | | | |  __/ (_| |  __/>  <  | | (_) | (_) | |_) \__ \ \__ \ (_| | |
     \___/  |_|  \___|\__, |\___/_/\_\ |_|\___/ \___/| .__/|___/ |___/\__, |_|
                      |___/                          |_|                 |_|
    */

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    %utl_rbeginx;
    parmcards4;
    hgtwgt<-read.table(header = TRUE, text = "
    NAME HGT WGT
    Roger 69  99
    James 60  84
    Janet 65  98
    ")
    hgtwgt
    saveRDS(hgtwgt,file="d:/rds/hgtwgt.rds")
    ;;;;
    %utl_rendx;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* d:/rds/hgtwgt.rds                                                                                                      */
    /*                                                                                                                        */
    /*    NAME HGT WGT                                                                                                        */
    /* 1 Roger  69  99                                                                                                        */
    /* 2 James  60  84                                                                                                        */
    /* 3 Janet  65  98                                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*   _ __ ___  __ _  _____  __                                                                                            */
    /*  | `__/ _ \/ _` |/ _ \ \/ /                                                                                            */
    /*  | | |  __/ (_| |  __/>  <                                                                                             */
    /*  |_|  \___|\__, |\___/_/\_\                                                                                            */
    /*            |___/                                                                                                       */
    /*                                                                                                                        */
    /*  COMMON GENERIC SYNTAX                R SYNTAX                                                                         */
    /*                                                                                                                        */
    /*  $string ="James";                    %utl_submit_r64x("                                                               */
    /*  if ($str =~ /^J/)                    hgtwgt<-readRDS(file='d:/rds/hgtwgt.rds');                                       */
    /*     {                                 hgtwgt;                                                                          */
    /*      print "$string";                 library(dplyr);                                                                  */
    /*     }                                 want <- hgtwgt |>                                                                */
    /*                                         filter(grepl('^J', NAME));                                                     */
    /*                                       want;                                                                            */
    /*                                       saveRDS(hgtwgt,file='d:/rds/regex.rds')                                          */
    /*                                       ");                                                                              */
    /*                                                                                                                        *r
    /*                                          NAME HGT WGT                                                                  *r
    /*                                       1 James  60  84                                                                  *r
    /*                                       2 Janet  65  98                                                                  *r
    /*                                                                                                                        *r
    /*       _       _         __                            _                                                                */
    /*    __| | __ _| |_ __ _ / _|_ __ __ _ _ __ ___   ___  | | ___   ___  _ __  ___                                          */
    /*   / _` |/ _` | __/ _` | |_| `__/ _` | `_ ` _ \ / _ \ | |/ _ \ / _ \| `_ \/ __|                                         */
    /*  | (_| | (_| | || (_| |  _| | | (_| | | | | | |  __/ | | (_) | (_) | |_) \__ \                                         */
    /*   \__,_|\__,_|\__\__,_|_| |_|  \__,_|_| |_| |_|\___| |_|\___/ \___/| .__/|___/                                         */
    /*                                                                    |_|                                                 */
    /*                                                                                                                        */
    /*  COMMON GENERIC SYNTAX   ADDING TO EXISTING DATAFRAME                    FILLING EMPTY DATAFRAME                       */
    /*                                                                                                                        */
    /*  DECLARE y(5);           %utl_submit_r64x('                             %utl_submit_r64x('                             */
    /*  DO x = 1 TO 5 BY 1      hgtwgt<-readRDS(file="d:/rds/hgtwgt.rds");     xy <- data.frame(X = double(), Y= double());   */
    /*    y[i]=**2;             for (i in seq(1,nrow(hgtwgt),1)) {             for (i in seq(1,2,1)) {                        */
    /*  End;                        hgtwgt[i,"BMI"]=703 *                        xy[i,"X"] = i;                               */
    /*                                   hgtwgt[i,"WGT"] /  hgtwgt[i,"HGT"]^2;   xy[i,"Y"] = i^2;                             */
    /*                          };                                               };                                           */
    /*                          hgtwgt;                                            xy;                                        */
    /*                          ');                                                ');                                        */
    /*                                                                                                                        */
    /*                                                                             X Y                                        */
    /*                                                                           1 1 1                                        */
    /*                                                                           2 2 4                                        */
    /*                                                                                                                        */
    /*                            HGT WGT      BMI                                                                            */
    /*                                                                          %utl_submit_r64x('                            */
    /*                          1  69  99 14.61815                              xy <- data.frame(X = double(), Y= double());  */
    /*                          2  56  84 18.83036                              for (i in seq(1,2,1)) {                       */
    /*                          3  65  98 16.30627                                xy[i,1] = i;                                */
    /*                                                                            xy[i,2] = i^2;                              */
    /*                                                                            };                                          */
    /*                          NON LOOP SOLUTIONS                                  xy;                                       */
    /*                                                                                                                        */
    /*                          %utl_submit_r64x('                                X Y                                         */
    /*                          library(dplyr);                                 1 1 1                                         */
    /*                          hgtwgt<-readRDS(file="d:/rds/hgtwgt.rds");      2 2 4                                         */
    /*                          hgtwgt;                                                                                       */
    /*                          hgtwgt<-mutate(hgtwgt,                          %utl_submit_r64x('                            */
    /*                            BMI = 703 * WGT / HGT^2);                     xy <- data.frame(X = double(), Y= double());  */
    /*                          hgtwgt;                                         for (i in seq(1,2,1)) {                       */
    /*                          ');                                               ros=cbind(X=i,Y=i^2);                       */
    /*                                                                            xy=rbind(xy,ros);                           */
    /*                            HGT WGT      BMI                                };                                          */
    /*                          1  69  99 14.61815                              xy;                                           */
    /*                          2  56  84 18.83036                              ');                                           */
    /*                          3  65  98 16.30627                                                                            */
    /*                                                                                                                        */
    /*                   _        _        _                                                                                  */
    /*   _ __ ___   __ _| |_ _ __(_)_  __ | | ___   ___  _ __  ___                                                            */
    /*  | `_ ` _ \ / _` | __| `__| \ \/ / | |/ _ \ / _ \| `_ \/ __|                                                           */
    /*  | | | | | | (_| | |_| |  | |>  <  | | (_) | (_) | |_) \__ \                                                           */
    /*  |_| |_| |_|\__,_|\__|_|  |_/_/\_\ |_|\___/ \___/| .__/|___/                                                           */
    /*                                                  |_|                                                                   */
    /*                   _        _        _                                                                                  */
    /*  COMMON GENERIC SYNTAX   ADDING TO EXISTING DATAFRAME                                                                  */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  mtx=j(2,2,0);             %utl_submit_r64x('                                                                          */
    /*  do ix=1 TO 2;             mtx<-matrix(nrow=2,ncol=2);                                                                 */
    /*   do iy=1 to 2;            for (i in seq(1,2,1))  {                                                                    */
    /*    mtx[ix,iy]=ix + iy;      for (j in seq(1,2,1))  {                                                                   */
    /*   end;                           mtx[i,j]=i+j ;                                                                        */
    /*  end;                            }                                                                                     */
    /*                              };                                                                                        */
    /*                            colnames(mtx)<-c("x","y");                                                                  */
    /*                            mtx;                                                                                        */
    /*                            ');                                                                                         */
    /*                                 x y                                                                                    */
    /*                                                                                                                        */
    /*                            [1,] 2 3                                                                                    */
    /*                            [2,] 3 4                                                                                    */
    /*                                                                                                                        */
    /*                            Matrix with character elements                                                              */
    /*                            (cannot have both integer and numeric)                                                      */
    /*                                                                                                                        */
    /*                            %utl_submit_r64x('                                                                          */
    /*                            mtx<-matrix(nrow=2,ncol=2);                                                                 */
    /*                            for (i in seq(1,2,1))  {                                                                    */
    /*                             for (j in seq(1,2,1))  {                                                                   */
    /*                                  mtx[i,j]=paste0(i+j) ;                                                                */
    /*                                  }                                                                                     */
    /*                              };                                                                                        */
    /*                            colnames(mtx)<-c("x","y");                                                                  */
    /*                            mtx;                                                                                        */
    /*                            ');                                                                                         */
    /*                                 x   y                                                                                  */
    /*                            [1,]  "2" "3"                                                                               */
    /*                            [2,]  "3" "4"                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.classz;
      set sashelp.class;
    run;quit;

    /*             _     _             _
    / |   __ _  __| | __| |   ___ ___ | |_   _ _ __ ___  _ __  ___
    | |  / _` |/ _` |/ _` |  / __/ _ \| | | | | `_ ` _ \| `_ \/ __|
    | | | (_| | (_| | (_| | | (_| (_) | | |_| | | | | | | | | \__ \
    |_|  \__,_|\__,_|\__,_|  \___\___/|_|\__,_|_| |_| |_|_| |_|___/

    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Add new columns to a datasets                                                                                          */
    /*                                                                                                                        */
    /* WPS DATASTEP                WPS PROC R                        WPS PYTHON                           WPS SQL PYTHON & R  */
    /* =======================     =============================     ================================     ==================  */
    /* data want;                  library(dplyr);                   classz["HGTDQR"]=                    select              */
    /*   set classz;               classz %>%                         classz["HEIGHT"]**2;                 HEIGHT^2 as HGTSQR */
    /*   HGTSQR=HEIGHT**2);           mutate(HGTSQR=HEIGHT^2) %>%    classz["BMI"]=                         ,703*WEIGHT       */
    /*   BMI=703*WEIGHT/HGTSQR;       mutate(BMI=703*WEIGHT/HGTSQR)   classz["WEIGHT"]/classz["HGTDQR"];    /HEIGHT^2 as BMI  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___    _
    |___ \  | | ___   ___  _ __  ___
      __) | | |/ _ \ / _ \| `_ \/ __|
     / __/  | | (_) | (_) | |_) \__ \
    |_____| |_|\___/ \___/| .__/|___/
                          |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Looping is discouraged in Python and R (seems complex in python)                                                      */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  WPS LOOP                                 R LOOP                                              WPS SQL PYTHON & R       */
    /*  ========                                 ======                                              ==================       */
    /*  data want;                                                                                   select                   */
    /*    array hgtwgt height weight;                                                                  HEIGHT^2 as HGTSQR     */
    /*    do row=1 to nobs;                      for(i in 1:nrow(classz))                             ,703*WEIGHT             */
    /*      set sd1.classz nobs=nobs point=row;     {                                                    /HEIGHT^2 as BMI     */
    /*      hgtsqr = hgtwgt[1]*hgtwgt[1];            classz[i,"BMI"] <- 703*classz[i,"WEIGHT"]                                */
    /*      bmi    = 703*hgtwgt[2]/hgtsqr;            / classz[i,"HEIGHT"]^2;                                                 */
    /*      output;                                 };                                                                        */
    /*    end;                                                                                                                */
    /*    stop;                                                                                                               */
    /*                                                                                                                        */
    /*  PYTHON LOOP                                                                                                           */
    /*  ===========                                                                                                           */
    /*                                                                                                                        */
    /*  for index, row in classz.iterrows():                                                                                  */
    /*     classz.at[index, 'HGTSQR'] = classz.loc[index, 'HEIGHT']*classz.loc[index, 'HEIGHT'];                              */
    /*                                                                                                                        */
    /*  for index, row in classz.iterrows():                                                                                  */
    /*     classz.at[index, 'BMI'] = 703*classz.loc[index, 'WEIGHT']/classz.loc[index, 'HGTSQR'];                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____    __                  _   _
    |___ /   / _|_   _ _ __   ___| |_(_) ___  _ __  ___
      |_ \  | |_| | | | `_ \ / __| __| |/ _ \| `_ \/ __|
     ___) | |  _| |_| | | | | (__| |_| | (_) | | | \__ \
    |____/  |_|  \__,_|_| |_|\___|\__|_|\___/|_| |_|___/

    */


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* FUNCTIONS IN R and Python can only return one value                                                                    */
    /*                                                                                                                        */
    /* WPS FUNCTION                                  WPS R FUNCTION                                    WPS SQL PYTHON & R     */
    /* ==========================================    ======================                          ====================     */
    /*                                                                                                select                  */
    /* proc fcmp outlib=work.functions.bmi;          bmi <- function(x,y) {                             HEIGHT^2 as HGTSQR    */
    /*   subroutine bmi(height,weight,hgtsqr,bmi);     z <- 703.0*x/y^2;                               ,703*WEIGHT            */
    /*     outargs hgtsqr, bmi;                        return(z)                                          /HEIGHT^2 as BMI    */
    /*     hgtsqr=height*height;                     };                                                                       */
    /*     bmi=703*weight/hgtsqr;                    sqr <- function(x) {                                                     */
    /*   endsub;                                       z <- x*x;                                                              */
    /* run;quit;                                       return(z)                                                              */
    /*                                               };                                                                       */
    /* data sd1.want;                                classz$BMI    <-bmi(classz$WEIGHT,classz$HEIGHT)                         */
    /*   retain hgtsqr bmi .;                        classz$HGTSQR <-sqr(classz$HEIGHT);                                      */
    /*   set sd1.classz;                                                                                                      */
    /*   call bmi(height,weight,hgtsqr,bmi);                                                                                  */
    /* run;quit;                                                                                                              */
    /*                                                                                                                        */
    /*  WPS PYTHON FUNCTION                                                                                                   */
    /*  ===================                                                                                                   */
    /*                                                                                                                        */
    /* def calc_bmi(x, y):;                                                                                                   */
    /* .  return  y/(x**2);                                                                                                   */
    /* data["BMI"] = data.apply(lambda x: calc_bmi(x["WEIGHT"], x["HEIGHT"]), axis=1);                                        */
    /*                                                                                                                        */
    /* def calc_sqr(x):;                                                                                                      */
    /* .  return  x**2;                                                                                                       */
    /* data["HGTSQR"] = data.apply(lambda x: calc_sqr(x["HEIGHT"]), axis=1);                                                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _               _              _
    | || |    ___ _   _| |__  ___  ___| |_   _ __ _____      _____
    | || |_  / __| | | | `_ \/ __|/ _ \ __| | `__/ _ \ \ /\ / / __|
    |__   _| \__ \ |_| | |_) \__ \  __/ |_  | | | (_) \ V  V /\__ \
       |_|   |___/\__,_|_.__/|___/\___|\__| |_|  \___/ \_/\_/ |___/

    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Filter dataset                                                                                                         */
    /*                                                                                                                        */
    /* WPS Datastep             WPS PROC R                    wps python                         WPS SQL PYTHON & R           */
    /* ======================   ===========================  ===============================     ==================           */
    /*                                                                                                                        */
    /* data classz;             classz %>% filter(SEX=="M")  classz.loc[classz["SEX"] == "M"];     select                     */
    /*   set sd1.classz                                                                               *                       */
    /*     (where=(SEX="M"));                                                                      from                       */
    /*                                                                                                classz                  */
    /*                                                                                             where                      */
    /*                                                                                                sex = "M"               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___        _                   _
    | ___|    __| |_ __ ___  _ __   | | _____  ___ _ __
    |___ \   / _` | `__/ _ \| `_ \  | |/ / _ \/ _ \ `_ \
     ___) | | (_| | | | (_) | |_) | |   <  __/  __/ |_) |
    |____/   \__,_|_|  \___/| .__/  |_|\_\___|\___| .__/
                            |_|                   |_|
    */

    /**************************************************************************************************************************/
    /*      _                                                                                                                 */
    /*   __| |_ __ ___  _ __                                                                                                  */
    /*  / _` | `__/ _ \| `_ \                                                                                                 */
    /* | (_| | | | (_) | |_) |                                                                                                */
    /*  \__,_|_|  \___/| .__/                                                                                                 */
    /*                 |_|                                                                                                    */
    /*                                                                                                                        */
    /* Filter dataset                                                                                                         */
    /*                                                                                                                        */
    /* WPS DATASTEP           WPS PROC R                        WPS PYTHON                              WPS SQL PYTHON & R     */
    /* ====================== ===========================      =====================================    ==================     */
    /*                                                                                                                        */
    /*   set classz(          classz %>% select (-SEX,-HEIGHT)  classz.drop(["SEX","HEIGHT"]                select            */
    /*     drop=SEX WEIGHT)                                        , axis=1);                                 name            */
    /*                                                                                                       ,age             */
    /*                                                                                                       ,weight          */
    /*  _                                                                                                   from              */
    /* | | _____  ___ _ __                                                                                    classz          */
    /* | |/ / _ \/ _ \ `_ \                                                                                                   */
    /* |   <  __/  __/ |_) |                                                                                                  */
    /* |_|\_\___|\___| .__/                                                                                                   */
    /*               |_|                                                                                                      */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* WPS DATASTEP           WPS PROC R                       WPS PYTHON (NO KEEP FUNCTION)           WPS SQL PYTHON & R     */
    /* ====================== ===========================     =====================================    ==================     */
    /*                                                                                                                        */
    /*   set classz(          classz %>% select (SEX,HEIGHT)   classz[["SEX", "HEIGHT"]]                   select             */
    /*     keep=SEX WEIGHT)                                                                                  sexe             */
    /*                                                                                                      ,height           */
    /*                                                                                                     from               */
    /*                                                                                                       classz           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*__                    _                                  _ _
     / /_    ___  ___  _ __| |_    __ _ ___  ___ ___ _ __   __| (_)_ __   __ _
    | `_ \  / __|/ _ \| `__| __|  / _` / __|/ __/ _ \ `_ \ / _` | | `_ \ / _` |
    | (_) | \__ \ (_) | |  | |_  | (_| \__ \ (_|  __/ | | | (_| | | | | | (_| |
     \___/  |___/\___/|_|   \__|  \__,_|___/\___\___|_| |_|\__,_|_|_| |_|\__, |
                                                                         |___/
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* WPS DATASTEP            WPS PROC R                    WPS PYTHON (NO KEEP FUNCTION)                 WPS SQL PYTHON & R */
    /* ======================  ===========================   =====================================         ================== */
    /*                                                                                                                        */
    /* proc sort data=classz;  classz %>% arrange(SEX,AGE)    classz.sort_values(['SEX', 'AGE'],            select            */
    /*  by sex age;                                                                                            *              */
    /*                                                                                                       from             */
    /*                                                                                                         classz         */
    /*                                                                                                       order            */
    /*                                                                                                         by sex, age    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                  _        _                              _ _
    |___  |  ___  ___  _ __| |_   __| | ___  ___  ___ ___ _ __   __| (_)_ __   __ _
       / /  / __|/ _ \| `__| __| / _` |/ _ \/ __|/ __/ _ \ `_ \ / _` | | `_ \ / _` |
      / /   \__ \ (_) | |  | |_ | (_| |  __/\__ \ (_|  __/ | | | (_| | | | | | (_| |
     /_/    |___/\___/|_|   \__| \__,_|\___||___/\___\___|_| |_|\__,_|_|_| |_|\__, |
                                                                              |___/
    */


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* WPS DATASTEP            WPS PROC R                    WPS PYTHON (NO KEEP FUNCTION)                 WPS SQL PYTHON & R */
    /* ======================  ===========================   =====================================         ================== */
    /*                                                                                                                        */
    /* proc sort data=classz;  classz %>% arrange(SEX,-AGE)   classz.sort_values(['SEX', 'AGE']              select           */
    /*  by sex descending age;                                   , ascending=[True, False])                    *              */
    /*                                                                                                       from             */
    /*                                                                                                         classz         */
    /*                                                                                                       order            */
    /*                                                                                                         by sex         */
    /*                                                                                                            age desc    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

     /*___                                             _                       _       _     _     _
      ( _ )   ___ _   _ _ __ ___  _ __ ___   __ _ _ __(_)_______ __      _____(_) __ _| |__ | |_  | |__  _   _   ___  _____  __
      / _ \  / __| | | | `_ ` _ \| `_ ` _ \ / _` | `__| |_  / _ \\ \ /\ / / _ \ |/ _` | `_ \| __| | `_ \| | | | / __|/ _ \ \/ /
     | (_) | \__ \ |_| | | | | | | | | | | | (_| | |  | |/ /  __/ \ V  V /  __/ | (_| | | | | |_  | |_) | |_| | \__ \  __/>  <
      \___/  |___/\__,_|_| |_| |_|_| |_| |_|\__,_|_|  |_/___\___|  \_/\_/ \___|_|\__, |_| |_|\__| |_.__/ \__, | |___/\___/_/\_\
                                                                                 |___/                   |___/
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* WPS PROC MEANS               WPS PROC R                  WPS PYTHON (NO KEEP FUNCTION)             WPS SQL PYTHON & R  */
    /* ======================       =========================== =====================================     ==================  */
    /*                                                                                                     select             */
    /* ods output summary=cls;       sumry<- classz %>%          classz.groupby(["SEX"]).agg({"WEIGHT":       sex             */
    /* proc means data=sd1.classz    group_by (SEX) %>%         ["mean","median","count"                    ,min(weight)      */
    /*  mean stddev median min max;   summarize(n=n(),            ,"std","min","max"]});                     ,max(weight)     */
    /* class sex;                       mean   = mean(WEIGHT)                                                ,median(weight)  */
    /* var weight;                     ,sd     = sd(WEIGHT)                                                  ,avg(weight)     */
    /*                                 ,median = median(WEIGHT)                                              ,stdev  (weight) */
    /*                                 ,min    = min(WEIGHT)                                               from               */
    /*                                 ,max    = max(WEIGHT)                                                  have            */
    /*                                );                                                                   group              */
    /*                                                                                                        by sex          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___    _             _           _                                       _
     / _ \  | | ___   __ _(_) ___ __ _| |  ___ ___  _ __ ___  _ __   __ _ _ __(_)___  ___  _ __  ___
    | (_) | | |/ _ \ / _` | |/ __/ _` | | / __/ _ \| `_ ` _ \| `_ \ / _` | `__| / __|/ _ \| `_ \/ __|
     \__, | | | (_) | (_| | | (_| (_| | || (_| (_) | | | | | | |_) | (_| | |  | \__ \ (_) | | | \__ \
       /_/  |_|\___/ \__, |_|\___\__,_|_| \___\___/|_| |_| |_| .__/ \__,_|_|  |_|___/\___/|_| |_|___/
                     |___/                                   |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* WPS SELECT WHEN DATASTEP       WPS PROC R               WPS PYTHON (NO KEEP FUNCTION)    WPS SQL PYTHON & R            */
    /* ========================       ======================   =============================    ==================            */
    /*                                                                                                                        */
    /*  select                        mutate(TEEN =            def my_condition(AGE):           select                        */
    /*   case                          case_when(                  if AGE >=11 and AGE <=12      case                         */
    /*     when age between 11 and 12    AGE >=11 & AGE <=12          return "PRE_TEEN "           when age between 11 and 12 */
    /*        then "PRE_TEEN  "           ~ "PRE_TEEN ",           if AGE >=13 and AGE <=16          then "PRE_TEEN  "        */
    /*     when age between 13 and 16    AGE >=13 & AGE <=16          return "POST_TEEN"           when age between 13 and 16 */
    /*        then "POST_TEEN "           ~ "POST_TEEN"            else :   return "ERR"             then "POST_TEEN "        */
    /*     else "ERR"                    TRUE  ~ "ERR"         classz["TEEN"] = classz["AGE"]      else "ERR"                 */
    /*   end as TEEN                    ))                         .apply(my_condition)          end as TEEN                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  ___                         _                                               _
    / |/ _ \   _ __ ___  __ _ _   _| | __ _ _ __   _____  ___ __  _ __ ___  ___ ___(_) ___  _ __  ___
    | | | | | | `__/ _ \/ _` | | | | |/ _` | `__| / _ \ \/ / `_ \| `__/ _ \/ __/ __| |/ _ \| `_ \/ __|
    | | |_| | | | |  __/ (_| | |_| | | (_| | |   |  __/>  <| |_) | | |  __/\__ \__ \ | (_) | | | \__ \
    |_|\___/  |_|  \___|\__, |\__,_|_|\__,_|_|    \___/_/\_\ .__/|_|  \___||___/___/_|\___/|_| |_|___/
                        |___/                              |_|
    */
    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* WPS DATASTEP PRXMATCH           WPS PROC R                      WPS PROC PYTHON              ONLY WPS SQL              */
    /* ======================          ======================          ===========================  ==================        */
    /*                                                                                                                        */
    /*  samplestr ="is Python fun";     samplestr<-c("is Python fun"); string = "Python is fun";    case                      */
    /*                                  output <- grep("Python"        match =                       when (prxmatch('\Python\'*/
    /*  loc=prxmatch("/Python/"          ,samplestr, value=TRUE);       re.search("Python",string);   ,'is Python fun')>0)    */
    /*    ,samplestr);                 if (output == samplestr) {;     if match:;                        then "pattern found" */
    /*  if loc > 0 then                    print("pattern found");      print("pattern found");      else "pattern NOT found" */
    /*    putlog "pattern found    ");  } else  {;                     else:;                        end as match             */
    /*  else                            .  print("pattern NOT found");   print("pattern NOT");                                */
    /*    putlog "pattern NOT found");  };                                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ _         _            _              _     _        _          _                               _
    / / |  _ __ (_)_   _____ | |_  __      _(_) __| | ___  | |_ ___   | | ___  _ __   __ _   ___  __ _| |
    | | | | `_ \| \ \ / / _ \| __| \ \ /\ / / |/ _` |/ _ \ | __/ _ \  | |/ _ \| `_ \ / _` | / __|/ _` | |
    | | | | |_) | |\ V / (_) | |_   \ V  V /| | (_| |  __/ | || (_) | | | (_) | | | | (_| | \__ \ (_| | |
    |_|_| | .__/|_| \_/ \___/ \__|   \_/\_/ |_|\__,_|\___|  \__\___/  |_|\___/|_| |_|\__, | |___/\__, |_|
          |_|                                                                        |___/          |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*    INPUT                     WPS R and Python (very slight sytax chages may be needed)                                 */
    /*                                                                                                                        */
    /*  data sd1.havfat;            select day,'A' as var,A as val from havFat union all                                      */
    /*    input day a b c d;        select day,'B' as var,B as val from havFat union all                                      */
    /*  cards4;                     select day,'C' as var,C as val from havFat union all                                      */
    /*  3 0 3 6 9                   select day,'D' as var,D as val from havFat                                                */
    /*  4 1 4 7 10                                                                                                            */
    /*  5 2 5 8 11                                                                                                            */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /* ____          _            _     _                     _                  _     _                  _
    / |___ \   _ __ (_)_   _____ | |_  | | ___  _ __   __ _  | |_ ___  __      _(_) __| | ___   ___  __ _| |
    | | __) | | `_ \| \ \ / / _ \| __| | |/ _ \| `_ \ / _` | | __/ _ \ \ \ /\ / / |/ _` |/ _ \ / __|/ _` | |
    | |/ __/  | |_) | |\ V / (_) | |_  | | (_) | | | | (_| | | || (_) | \ V  V /| | (_| |  __/ \__ \ (_| | |
    |_|_____| | .__/|_| \_/ \___/ \__| |_|\___/|_| |_|\__, |  \__\___/   \_/\_/ |_|\__,_|\___| |___/\__, |_|
              |_|                                     |___/                                            |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  data sd1.long;             select                                                                                     */
    /*    informat variable $1.;       day                                                                                    */
    /*    input  value day var;       ,max(case when partition=1 then value else . end) as a                                  */
    /*  cards4;                       ,max(case when partition=2 then value else . end) as b                                  */
    /*  0 3 A                         ,max(case when partition=3 then value else . end) as c                                  */
    /*  1 4 A                         ,max(case when partition=4 then value else . end) as d                                  */
    /*  2 5 A                       from                                                                                      */
    /*  3 3 B                         %sqlpartition(sd1.long,by=day)                                                          */
    /*  4 4 B                                                                                                                 */
    /*  5 5 B                        subsitute this for macro for R and python sqllite                                        */
    /*  6 3 C                                                                                                                 */
    /*  7 4 C                       (select day, value , row_number() OVER (PARTITION BY dad) as partition from long )        */
    /*  8 5 C                                                                                                                 */
    /*  9 3 D                       use sql arrays to generated repeated code                                                 */
    /*  10 4 D                                                                                                                */
    /*  11 5 D                                                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /* _____         _            _              _     _        _          _                                             _
    / |___ /   _ __ (_)_   _____ | |_  __      _(_) __| | ___  | |_ ___   | | ___  _ __   __ _   _ __   ___    ___  __ _| |
    | | |_ \  | `_ \| \ \ / / _ \| __| \ \ /\ / / |/ _` |/ _ \ | __/ _ \  | |/ _ \| `_ \ / _` | | `_ \ / _ \  / __|/ _` | |
    | |___) | | |_) | |\ V / (_) | |_   \ V  V /| | (_| |  __/ | || (_) | | | (_) | | | | (_| | | | | | (_) | \__ \ (_| | |
    |_|____/  | .__/|_| \_/ \___/ \__|   \_/\_/ |_|\__,_|\___|  \__\___/  |_|\___/|_| |_|\__, | |_| |_|\___/  |___/\__, |_|
              |_|                                                                         |___/                       |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*    INPUT                   WPS PROCESS                   WPS PROC R                                                    */
    /*                                                                                                                        */
    /* data sd1.havfat;        proc transpose data=sd1.havFat   library(tidyverse);                                           */
    /*   input day a b c d;      out=fat_to_long;               pivot_wide_to_long<-gather(have, "VAR", "VAL", -DAY);         */
    /* cards4;                 by day;                                                                                        */
    /* 3 0 3 6 9               run;quit;                                                                                      */
    /* 4 1 4 7 10                                                                                                             */
    /* 5 2 5 8 11                                                                                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /* _  _           _            _     _                     _                  _     _                                _
    / | || |    _ __ (_)_   _____ | |_  | | ___  _ __   __ _  | |_ ___  __      _(_) __| | ___   _ __   ___    ___  __ _| |
    | | || |_  | `_ \| \ \ / / _ \| __| | |/ _ \| `_ \ / _` | | __/ _ \ \ \ /\ / / |/ _` |/ _ \ | `_ \ / _ \  / __|/ _` | |
    | |__   _| | |_) | |\ V / (_) | |_  | | (_) | | | | (_| | | || (_) | \ V  V /| | (_| |  __/ | | | | (_) | \__ \ (_| | |
    |_|  |_|   | .__/|_| \_/ \___/ \__| |_|\___/|_| |_|\__, |  \__\___/   \_/\_/ |_|\__,_|\___| |_| |_|\___/  |___/\__, |_|
               |_|                                     |___/                                                          |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*    INPUT                 WPS PROCESS                     WPS PROC R                                                    */
    /*                                                                                                                        */
    /* data sd1.long;           proc sort data=sd1.long;        pivot_long_to_wide<-pivot_wide_to_long %>%                    */
    /*   informat variable $1.; by day;                          pivot_wider(names_from = VAR, values_from = VAL);            */
    /*   input  value day var;                                                                                                */
    /* cards4;                  proc transpose data=sd1.long                                                                  */
    /* 0 3 A                     out=long_to_fat;                                                                             */
    /* 1 4 A                      by day;                                                                                     */
    /* 2 5 A                      id variable;                                                                                */
    /* 3 3 B                      var value;                                                                                  */
    /* 4 4 B                                                                                                                  */
    /* 5 5 B                                                                                                                  */
    /* 6 3 C                                                                                                                  */
    /* 7 4 C                                                                                                                  */
    /* 8 5 C                                                                                                                  */
    /* 9 3 D                                                                                                                  */
    /* 10 4 D                                                                                                                 */
    /* 11 5 D                                                                                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
