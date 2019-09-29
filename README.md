# gretl_panel_data
The open-source econometric software [gretl] (http://gretl.sourceforge.net/) nicely supports working with panel data.

Once a panel data set is defined, the user can access different information.

## Illustration
Load the Grunfeld investment data set:
```gretl
open grunfeld.gdt
```
A helpful command is the ```$obsdate``` accessor for returning a series holding ISO dates. However, for getting this working, once need to set the observation dimension as follows:
```gretl
setobs 1 1935 --panel-time
series obsdate = $obsdate
print obsdate -o --range=1:40
```
This returns (only some values are shown) a series of integers holding ISO dates for each cross-sectional unit
```
           obsdate

 1:01     19350101
 1:02     19360101
 1:03     19370101
 1:04     19380101
 1:05     19390101
 1:06     19400101
 .
 .
 .
 2:16     19500101
 2:17     19510101
 2:18     19520101
 2:19     19530101
 2:20     19540101
```

The following accessors are useful when working with panel data:
```gretl
eval $pd				      # Number of time periods T
eval $tmax				    # T * N for full sample
eval $nobs				    # T * N for currently selected sample
catch eval $obsmicro	# Not defined for panel
catch eval $obsminor	# Discrete values of time-dimension, 1 to T
eval $obsmajor			  # Discrete values of cross-sectional dimension, 1 to N
```
Returning
```
20
200
200
```
Additional information are:
```gretl
catch eval $obsmicro	  # Not defined for panel data
series time_dim_id = $obsminor	    # Discrete values of time-dimension, 1 to T
series cross_dim_id =  $obsmajor		# Discrete values of cross-sectional dimension, 1 to N
print time_dim_id cross_dim_id -o --range=1:40
```
Returning:
```
       time_dim_id cross_dim_id

 1:01            1            1
 1:02            2            1
 1:03            3            1
 1:04            4            1
 1:05            5            1
 1:06            6            1
 1:07            7            1
 1:08            8            1
 1:09            9            1
 1:10           10            1
 1:11           11            1
 1:12           12            1
 1:13           13            1
 1:14           14            1
 1:15           15            1
 1:16           16            1
 1:17           17            1
 1:18           18            1
 1:19           19            1
 1:20           20            1
 2:01            1            2
 2:02            2            2
 2:03            3            2
 2:04            4            2
 2:05            5            2
 2:06            6            2
 2:07            7            2
 2:08            8            2
 2:09            9            2
 2:10           10            2
 2:11           11            2
 2:12           12            2
 2:13           13            2
 2:14           14            2
 2:15           15            2
 2:16           16            2
 2:17           17            2
 2:18           18            2
 2:19           19            2
 2:20           20            2
 ```



