#

```
brake_csv_by_N_lines () {
  local SOURCENAME=$1
  local TRIMROWS=$2
  local TOTALROW=`wc -l $SOURCENAME| grep  -o '[0-9]*'`
  local N=0
  
  head -n1 $SOURCENAME > $SOURCENAME.head
  LEFTROWS=$(( TOTALROW - 1 ))
  
  for (( ; ; ))
    do
      if (( $LEFTROWS <= 0 )) ; then     break;   fi;
      echo $LEFTROWS $SOURCENAME $N
      cat $SOURCENAME.head > out/$SOURCENAME.$N.csv
      tail -n$LEFTROWS $SOURCENAME | head -n$TRIMROWS >> out/$SOURCENAME.$N.csv
      N=$(( N + 1 ))
      LEFTROWS=$(( LEFTROWS - TRIMROWS ));
    done
}

mkdir out
brake_csv_by_N_lines happiness_score.csv 1000000
brake_csv_by_N_lines track_recommender.csv 300000
brake_csv_by_N_lines activity_text.csv 300000
```

```
$ ls -lah out/
total 1.7G
drwxrwxr-x. 2 user user 4.0K Jul  4 16:25 .
drwxr-xr-x. 3 user user 4.0K Jul  4 16:25 ..
-rw-rw-r--. 1 user user  74M Jul  4 16:25 activity_text.csv.0.csv
-rw-rw-r--. 1 user user  35M Jul  4 16:25 activity_text.csv.10.csv
-rw-rw-r--. 1 user user  68M Jul  4 16:25 activity_text.csv.1.csv
-rw-rw-r--. 1 user user  65M Jul  4 16:25 activity_text.csv.2.csv
-rw-rw-r--. 1 user user  60M Jul  4 16:25 activity_text.csv.3.csv
-rw-rw-r--. 1 user user  52M Jul  4 16:25 activity_text.csv.4.csv
-rw-rw-r--. 1 user user  52M Jul  4 16:25 activity_text.csv.5.csv
-rw-rw-r--. 1 user user  49M Jul  4 16:25 activity_text.csv.6.csv
-rw-rw-r--. 1 user user  52M Jul  4 16:25 activity_text.csv.7.csv
-rw-rw-r--. 1 user user  51M Jul  4 16:25 activity_text.csv.8.csv
-rw-rw-r--. 1 user user  59M Jul  4 16:25 activity_text.csv.9.csv
-rw-rw-r--. 1 user user  66M Jul  4 16:23 happiness_score.csv.0.csv
-rw-rw-r--. 1 user user  66M Jul  4 16:23 happiness_score.csv.1.csv
-rw-rw-r--. 1 user user  12M Jul  4 16:23 happiness_score.csv.2.csv
-rw-rw-r--. 1 user user  67M Jul  4 16:25 track_recommender.csv.0.csv
-rw-rw-r--. 1 user user  86M Jul  4 16:25 track_recommender.csv.10.csv
-rw-rw-r--. 1 user user  69M Jul  4 16:25 track_recommender.csv.11.csv
-rw-rw-r--. 1 user user  60M Jul  4 16:25 track_recommender.csv.1.csv
-rw-rw-r--. 1 user user  69M Jul  4 16:25 track_recommender.csv.2.csv
-rw-rw-r--. 1 user user  84M Jul  4 16:25 track_recommender.csv.3.csv
-rw-rw-r--. 1 user user  86M Jul  4 16:25 track_recommender.csv.4.csv
-rw-rw-r--. 1 user user  87M Jul  4 16:25 track_recommender.csv.5.csv
-rw-rw-r--. 1 user user  86M Jul  4 16:25 track_recommender.csv.6.csv
-rw-rw-r--. 1 user user  86M Jul  4 16:25 track_recommender.csv.7.csv
-rw-rw-r--. 1 user user  83M Jul  4 16:25 track_recommender.csv.8.csv
-rw-rw-r--. 1 user user  85M Jul  4 16:25 track_recommender.csv.9.csv
```

