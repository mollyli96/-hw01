hw01-molly-li
================
Molly Li
2/21/2018

1) Data Dictionary (10 pts)
===========================

2) Data Import (20 pts)
=======================

``` r
library(readr)
```

    ## Warning: package 'readr' was built under R version 3.3.2

``` r
library(dplyr)
```

    ## Warning: package 'dplyr' was built under R version 3.3.2

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library("corrplot")
```

    ## Warning: package 'corrplot' was built under R version 3.3.2

    ## corrplot 0.84 loaded

``` r
column_names <- c(
         'symboling',
         'normalized_losses',
         'make',
         'fuel_type',
         'aspiration',
         'num_of_doors',
         'body_style',
         'drive_wheels',
         'engine_location',
         'wheel_base',
         'length',
         'width',
         'height',
         'curb_weight',
         'engine_type',
         'num_of_cylinders',
         'engine_size',
         'fuel_system',
         'bore',
         'stroke',
         'compression_ratio',
         'horsepower',
         'peak_rpm',
         'city_mpg',
         'highway_mpg',
         'price')

 colClasses <- c(
         'real',
         'real',
         'character',
         'character',
         'character',
         'character',
         'character',
         'character',
         'character',
         'real',
         'real',
         'real',
         'real',
         'integer',
         'character',
         'character',
         'integer',
         'character',
         'real',
         'real',
         'real',
         'integer',
         'integer',
         'integer',
         'integer',
         'integer'
         )
dat1 <- read.csv('imports-85.data', header= T)
str("imports-85.data, vec.len = 1")
```

    ##  chr "imports-85.data, vec.len = 1"

``` r
dat1
```

    ##     X3  X.   alfa.romero    gas   std  two convertible rwd front X88.60
    ## 1    3   ?   alfa-romero    gas   std  two convertible rwd front   88.6
    ## 2    1   ?   alfa-romero    gas   std  two   hatchback rwd front   94.5
    ## 3    2 164          audi    gas   std four       sedan fwd front   99.8
    ## 4    2 164          audi    gas   std four       sedan 4wd front   99.4
    ## 5    2   ?          audi    gas   std  two       sedan fwd front   99.8
    ## 6    1 158          audi    gas   std four       sedan fwd front  105.8
    ## 7    1   ?          audi    gas   std four       wagon fwd front  105.8
    ## 8    1 158          audi    gas turbo four       sedan fwd front  105.8
    ## 9    0   ?          audi    gas turbo  two   hatchback 4wd front   99.5
    ## 10   2 192           bmw    gas   std  two       sedan rwd front  101.2
    ## 11   0 192           bmw    gas   std four       sedan rwd front  101.2
    ## 12   0 188           bmw    gas   std  two       sedan rwd front  101.2
    ## 13   0 188           bmw    gas   std four       sedan rwd front  101.2
    ## 14   1   ?           bmw    gas   std four       sedan rwd front  103.5
    ## 15   0   ?           bmw    gas   std four       sedan rwd front  103.5
    ## 16   0   ?           bmw    gas   std  two       sedan rwd front  103.5
    ## 17   0   ?           bmw    gas   std four       sedan rwd front  110.0
    ## 18   2 121     chevrolet    gas   std  two   hatchback fwd front   88.4
    ## 19   1  98     chevrolet    gas   std  two   hatchback fwd front   94.5
    ## 20   0  81     chevrolet    gas   std four       sedan fwd front   94.5
    ## 21   1 118         dodge    gas   std  two   hatchback fwd front   93.7
    ## 22   1 118         dodge    gas   std  two   hatchback fwd front   93.7
    ## 23   1 118         dodge    gas turbo  two   hatchback fwd front   93.7
    ## 24   1 148         dodge    gas   std four   hatchback fwd front   93.7
    ## 25   1 148         dodge    gas   std four       sedan fwd front   93.7
    ## 26   1 148         dodge    gas   std four       sedan fwd front   93.7
    ## 27   1 148         dodge    gas turbo    ?       sedan fwd front   93.7
    ## 28  -1 110         dodge    gas   std four       wagon fwd front  103.3
    ## 29   3 145         dodge    gas turbo  two   hatchback fwd front   95.9
    ## 30   2 137         honda    gas   std  two   hatchback fwd front   86.6
    ## 31   2 137         honda    gas   std  two   hatchback fwd front   86.6
    ## 32   1 101         honda    gas   std  two   hatchback fwd front   93.7
    ## 33   1 101         honda    gas   std  two   hatchback fwd front   93.7
    ## 34   1 101         honda    gas   std  two   hatchback fwd front   93.7
    ## 35   0 110         honda    gas   std four       sedan fwd front   96.5
    ## 36   0  78         honda    gas   std four       wagon fwd front   96.5
    ## 37   0 106         honda    gas   std  two   hatchback fwd front   96.5
    ## 38   0 106         honda    gas   std  two   hatchback fwd front   96.5
    ## 39   0  85         honda    gas   std four       sedan fwd front   96.5
    ## 40   0  85         honda    gas   std four       sedan fwd front   96.5
    ## 41   0  85         honda    gas   std four       sedan fwd front   96.5
    ## 42   1 107         honda    gas   std  two       sedan fwd front   96.5
    ## 43   0   ?         isuzu    gas   std four       sedan rwd front   94.3
    ## 44   1   ?         isuzu    gas   std  two       sedan fwd front   94.5
    ## 45   0   ?         isuzu    gas   std four       sedan fwd front   94.5
    ## 46   2   ?         isuzu    gas   std  two   hatchback rwd front   96.0
    ## 47   0 145        jaguar    gas   std four       sedan rwd front  113.0
    ## 48   0   ?        jaguar    gas   std four       sedan rwd front  113.0
    ## 49   0   ?        jaguar    gas   std  two       sedan rwd front  102.0
    ## 50   1 104         mazda    gas   std  two   hatchback fwd front   93.1
    ## 51   1 104         mazda    gas   std  two   hatchback fwd front   93.1
    ## 52   1 104         mazda    gas   std  two   hatchback fwd front   93.1
    ## 53   1 113         mazda    gas   std four       sedan fwd front   93.1
    ## 54   1 113         mazda    gas   std four       sedan fwd front   93.1
    ## 55   3 150         mazda    gas   std  two   hatchback rwd front   95.3
    ## 56   3 150         mazda    gas   std  two   hatchback rwd front   95.3
    ## 57   3 150         mazda    gas   std  two   hatchback rwd front   95.3
    ## 58   3 150         mazda    gas   std  two   hatchback rwd front   95.3
    ## 59   1 129         mazda    gas   std  two   hatchback fwd front   98.8
    ## 60   0 115         mazda    gas   std four       sedan fwd front   98.8
    ## 61   1 129         mazda    gas   std  two   hatchback fwd front   98.8
    ## 62   0 115         mazda    gas   std four       sedan fwd front   98.8
    ## 63   0   ?         mazda diesel   std    ?       sedan fwd front   98.8
    ## 64   0 115         mazda    gas   std four   hatchback fwd front   98.8
    ## 65   0 118         mazda    gas   std four       sedan rwd front  104.9
    ## 66   0   ?         mazda diesel   std four       sedan rwd front  104.9
    ## 67  -1  93 mercedes-benz diesel turbo four       sedan rwd front  110.0
    ## 68  -1  93 mercedes-benz diesel turbo four       wagon rwd front  110.0
    ## 69   0  93 mercedes-benz diesel turbo  two     hardtop rwd front  106.7
    ## 70  -1  93 mercedes-benz diesel turbo four       sedan rwd front  115.6
    ## 71  -1   ? mercedes-benz    gas   std four       sedan rwd front  115.6
    ## 72   3 142 mercedes-benz    gas   std  two convertible rwd front   96.6
    ## 73   0   ? mercedes-benz    gas   std four       sedan rwd front  120.9
    ## 74   1   ? mercedes-benz    gas   std  two     hardtop rwd front  112.0
    ## 75   1   ?       mercury    gas turbo  two   hatchback rwd front  102.7
    ## 76   2 161    mitsubishi    gas   std  two   hatchback fwd front   93.7
    ## 77   2 161    mitsubishi    gas   std  two   hatchback fwd front   93.7
    ## 78   2 161    mitsubishi    gas   std  two   hatchback fwd front   93.7
    ## 79   1 161    mitsubishi    gas turbo  two   hatchback fwd front   93.0
    ## 80   3 153    mitsubishi    gas turbo  two   hatchback fwd front   96.3
    ## 81   3 153    mitsubishi    gas   std  two   hatchback fwd front   96.3
    ## 82   3   ?    mitsubishi    gas turbo  two   hatchback fwd front   95.9
    ## 83   3   ?    mitsubishi    gas turbo  two   hatchback fwd front   95.9
    ## 84   3   ?    mitsubishi    gas turbo  two   hatchback fwd front   95.9
    ## 85   1 125    mitsubishi    gas   std four       sedan fwd front   96.3
    ## 86   1 125    mitsubishi    gas   std four       sedan fwd front   96.3
    ## 87   1 125    mitsubishi    gas turbo four       sedan fwd front   96.3
    ## 88  -1 137    mitsubishi    gas   std four       sedan fwd front   96.3
    ## 89   1 128        nissan    gas   std  two       sedan fwd front   94.5
    ## 90   1 128        nissan diesel   std  two       sedan fwd front   94.5
    ## 91   1 128        nissan    gas   std  two       sedan fwd front   94.5
    ## 92   1 122        nissan    gas   std four       sedan fwd front   94.5
    ## 93   1 103        nissan    gas   std four       wagon fwd front   94.5
    ## 94   1 128        nissan    gas   std  two       sedan fwd front   94.5
    ## 95   1 128        nissan    gas   std  two   hatchback fwd front   94.5
    ## 96   1 122        nissan    gas   std four       sedan fwd front   94.5
    ## 97   1 103        nissan    gas   std four       wagon fwd front   94.5
    ## 98   2 168        nissan    gas   std  two     hardtop fwd front   95.1
    ## 99   0 106        nissan    gas   std four   hatchback fwd front   97.2
    ## 100  0 106        nissan    gas   std four       sedan fwd front   97.2
    ## 101  0 128        nissan    gas   std four       sedan fwd front  100.4
    ## 102  0 108        nissan    gas   std four       wagon fwd front  100.4
    ## 103  0 108        nissan    gas   std four       sedan fwd front  100.4
    ## 104  3 194        nissan    gas   std  two   hatchback rwd front   91.3
    ## 105  3 194        nissan    gas turbo  two   hatchback rwd front   91.3
    ## 106  1 231        nissan    gas   std  two   hatchback rwd front   99.2
    ## 107  0 161        peugot    gas   std four       sedan rwd front  107.9
    ## 108  0 161        peugot diesel turbo four       sedan rwd front  107.9
    ## 109  0   ?        peugot    gas   std four       wagon rwd front  114.2
    ## 110  0   ?        peugot diesel turbo four       wagon rwd front  114.2
    ## 111  0 161        peugot    gas   std four       sedan rwd front  107.9
    ## 112  0 161        peugot diesel turbo four       sedan rwd front  107.9
    ## 113  0   ?        peugot    gas   std four       wagon rwd front  114.2
    ## 114  0   ?        peugot diesel turbo four       wagon rwd front  114.2
    ## 115  0 161        peugot    gas   std four       sedan rwd front  107.9
    ## 116  0 161        peugot diesel turbo four       sedan rwd front  107.9
    ## 117  0 161        peugot    gas turbo four       sedan rwd front  108.0
    ## 118  1 119      plymouth    gas   std  two   hatchback fwd front   93.7
    ## 119  1 119      plymouth    gas turbo  two   hatchback fwd front   93.7
    ## 120  1 154      plymouth    gas   std four   hatchback fwd front   93.7
    ## 121  1 154      plymouth    gas   std four       sedan fwd front   93.7
    ## 122  1 154      plymouth    gas   std four       sedan fwd front   93.7
    ## 123 -1  74      plymouth    gas   std four       wagon fwd front  103.3
    ## 124  3   ?      plymouth    gas turbo  two   hatchback rwd front   95.9
    ## 125  3 186       porsche    gas   std  two   hatchback rwd front   94.5
    ## 126  3   ?       porsche    gas   std  two     hardtop rwd  rear   89.5
    ## 127  3   ?       porsche    gas   std  two     hardtop rwd  rear   89.5
    ## 128  3   ?       porsche    gas   std  two convertible rwd  rear   89.5
    ## 129  1   ?       porsche    gas   std  two   hatchback rwd front   98.4
    ## 130  0   ?       renault    gas   std four       wagon fwd front   96.1
    ## 131  2   ?       renault    gas   std  two   hatchback fwd front   96.1
    ## 132  3 150          saab    gas   std  two   hatchback fwd front   99.1
    ## 133  2 104          saab    gas   std four       sedan fwd front   99.1
    ## 134  3 150          saab    gas   std  two   hatchback fwd front   99.1
    ## 135  2 104          saab    gas   std four       sedan fwd front   99.1
    ## 136  3 150          saab    gas turbo  two   hatchback fwd front   99.1
    ## 137  2 104          saab    gas turbo four       sedan fwd front   99.1
    ## 138  2  83        subaru    gas   std  two   hatchback fwd front   93.7
    ## 139  2  83        subaru    gas   std  two   hatchback fwd front   93.7
    ## 140  2  83        subaru    gas   std  two   hatchback 4wd front   93.3
    ## 141  0 102        subaru    gas   std four       sedan fwd front   97.2
    ## 142  0 102        subaru    gas   std four       sedan fwd front   97.2
    ## 143  0 102        subaru    gas   std four       sedan fwd front   97.2
    ## 144  0 102        subaru    gas   std four       sedan 4wd front   97.0
    ## 145  0 102        subaru    gas turbo four       sedan 4wd front   97.0
    ## 146  0  89        subaru    gas   std four       wagon fwd front   97.0
    ## 147  0  89        subaru    gas   std four       wagon fwd front   97.0
    ## 148  0  85        subaru    gas   std four       wagon 4wd front   96.9
    ## 149  0  85        subaru    gas turbo four       wagon 4wd front   96.9
    ## 150  1  87        toyota    gas   std  two   hatchback fwd front   95.7
    ## 151  1  87        toyota    gas   std  two   hatchback fwd front   95.7
    ## 152  1  74        toyota    gas   std four   hatchback fwd front   95.7
    ## 153  0  77        toyota    gas   std four       wagon fwd front   95.7
    ## 154  0  81        toyota    gas   std four       wagon 4wd front   95.7
    ## 155  0  91        toyota    gas   std four       wagon 4wd front   95.7
    ## 156  0  91        toyota    gas   std four       sedan fwd front   95.7
    ## 157  0  91        toyota    gas   std four   hatchback fwd front   95.7
    ## 158  0  91        toyota diesel   std four       sedan fwd front   95.7
    ## 159  0  91        toyota diesel   std four   hatchback fwd front   95.7
    ## 160  0  91        toyota    gas   std four       sedan fwd front   95.7
    ## 161  0  91        toyota    gas   std four   hatchback fwd front   95.7
    ## 162  0  91        toyota    gas   std four       sedan fwd front   95.7
    ## 163  1 168        toyota    gas   std  two       sedan rwd front   94.5
    ## 164  1 168        toyota    gas   std  two   hatchback rwd front   94.5
    ## 165  1 168        toyota    gas   std  two       sedan rwd front   94.5
    ## 166  1 168        toyota    gas   std  two   hatchback rwd front   94.5
    ## 167  2 134        toyota    gas   std  two     hardtop rwd front   98.4
    ## 168  2 134        toyota    gas   std  two     hardtop rwd front   98.4
    ## 169  2 134        toyota    gas   std  two   hatchback rwd front   98.4
    ## 170  2 134        toyota    gas   std  two     hardtop rwd front   98.4
    ## 171  2 134        toyota    gas   std  two   hatchback rwd front   98.4
    ## 172  2 134        toyota    gas   std  two convertible rwd front   98.4
    ## 173 -1  65        toyota    gas   std four       sedan fwd front  102.4
    ## 174 -1  65        toyota diesel turbo four       sedan fwd front  102.4
    ## 175 -1  65        toyota    gas   std four   hatchback fwd front  102.4
    ## 176 -1  65        toyota    gas   std four       sedan fwd front  102.4
    ## 177 -1  65        toyota    gas   std four   hatchback fwd front  102.4
    ## 178  3 197        toyota    gas   std  two   hatchback rwd front  102.9
    ## 179  3 197        toyota    gas   std  two   hatchback rwd front  102.9
    ## 180 -1  90        toyota    gas   std four       sedan rwd front  104.5
    ## 181 -1   ?        toyota    gas   std four       wagon rwd front  104.5
    ## 182  2 122    volkswagen diesel   std  two       sedan fwd front   97.3
    ## 183  2 122    volkswagen    gas   std  two       sedan fwd front   97.3
    ## 184  2  94    volkswagen diesel   std four       sedan fwd front   97.3
    ## 185  2  94    volkswagen    gas   std four       sedan fwd front   97.3
    ## 186  2  94    volkswagen    gas   std four       sedan fwd front   97.3
    ## 187  2  94    volkswagen diesel turbo four       sedan fwd front   97.3
    ## 188  2  94    volkswagen    gas   std four       sedan fwd front   97.3
    ## 189  3   ?    volkswagen    gas   std  two convertible fwd front   94.5
    ## 190  3 256    volkswagen    gas   std  two   hatchback fwd front   94.5
    ## 191  0   ?    volkswagen    gas   std four       sedan fwd front  100.4
    ## 192  0   ?    volkswagen diesel turbo four       sedan fwd front  100.4
    ## 193  0   ?    volkswagen    gas   std four       wagon fwd front  100.4
    ## 194 -2 103         volvo    gas   std four       sedan rwd front  104.3
    ## 195 -1  74         volvo    gas   std four       wagon rwd front  104.3
    ## 196 -2 103         volvo    gas   std four       sedan rwd front  104.3
    ## 197 -1  74         volvo    gas   std four       wagon rwd front  104.3
    ## 198 -2 103         volvo    gas turbo four       sedan rwd front  104.3
    ## 199 -1  74         volvo    gas turbo four       wagon rwd front  104.3
    ## 200 -1  95         volvo    gas   std four       sedan rwd front  109.1
    ## 201 -1  95         volvo    gas turbo four       sedan rwd front  109.1
    ## 202 -1  95         volvo    gas   std four       sedan rwd front  109.1
    ## 203 -1  95         volvo diesel turbo four       sedan rwd front  109.1
    ## 204 -1  95         volvo    gas turbo four       sedan rwd front  109.1
    ##     X168.80 X64.10 X48.80 X2548  dohc   four X130 mpfi X3.47 X2.68 X9.00
    ## 1     168.8   64.1   48.8  2548  dohc   four  130 mpfi  3.47  2.68  9.00
    ## 2     171.2   65.5   52.4  2823  ohcv    six  152 mpfi  2.68  3.47  9.00
    ## 3     176.6   66.2   54.3  2337   ohc   four  109 mpfi  3.19  3.40 10.00
    ## 4     176.6   66.4   54.3  2824   ohc   five  136 mpfi  3.19  3.40  8.00
    ## 5     177.3   66.3   53.1  2507   ohc   five  136 mpfi  3.19  3.40  8.50
    ## 6     192.7   71.4   55.7  2844   ohc   five  136 mpfi  3.19  3.40  8.50
    ## 7     192.7   71.4   55.7  2954   ohc   five  136 mpfi  3.19  3.40  8.50
    ## 8     192.7   71.4   55.9  3086   ohc   five  131 mpfi  3.13  3.40  8.30
    ## 9     178.2   67.9   52.0  3053   ohc   five  131 mpfi  3.13  3.40  7.00
    ## 10    176.8   64.8   54.3  2395   ohc   four  108 mpfi  3.50  2.80  8.80
    ## 11    176.8   64.8   54.3  2395   ohc   four  108 mpfi  3.50  2.80  8.80
    ## 12    176.8   64.8   54.3  2710   ohc    six  164 mpfi  3.31  3.19  9.00
    ## 13    176.8   64.8   54.3  2765   ohc    six  164 mpfi  3.31  3.19  9.00
    ## 14    189.0   66.9   55.7  3055   ohc    six  164 mpfi  3.31  3.19  9.00
    ## 15    189.0   66.9   55.7  3230   ohc    six  209 mpfi  3.62  3.39  8.00
    ## 16    193.8   67.9   53.7  3380   ohc    six  209 mpfi  3.62  3.39  8.00
    ## 17    197.0   70.9   56.3  3505   ohc    six  209 mpfi  3.62  3.39  8.00
    ## 18    141.1   60.3   53.2  1488     l  three   61 2bbl  2.91  3.03  9.50
    ## 19    155.9   63.6   52.0  1874   ohc   four   90 2bbl  3.03  3.11  9.60
    ## 20    158.8   63.6   52.0  1909   ohc   four   90 2bbl  3.03  3.11  9.60
    ## 21    157.3   63.8   50.8  1876   ohc   four   90 2bbl  2.97  3.23  9.41
    ## 22    157.3   63.8   50.8  1876   ohc   four   90 2bbl  2.97  3.23  9.40
    ## 23    157.3   63.8   50.8  2128   ohc   four   98 mpfi  3.03  3.39  7.60
    ## 24    157.3   63.8   50.6  1967   ohc   four   90 2bbl  2.97  3.23  9.40
    ## 25    157.3   63.8   50.6  1989   ohc   four   90 2bbl  2.97  3.23  9.40
    ## 26    157.3   63.8   50.6  1989   ohc   four   90 2bbl  2.97  3.23  9.40
    ## 27    157.3   63.8   50.6  2191   ohc   four   98 mpfi  3.03  3.39  7.60
    ## 28    174.6   64.6   59.8  2535   ohc   four  122 2bbl  3.34  3.46  8.50
    ## 29    173.2   66.3   50.2  2811   ohc   four  156  mfi  3.60  3.90  7.00
    ## 30    144.6   63.9   50.8  1713   ohc   four   92 1bbl  2.91  3.41  9.60
    ## 31    144.6   63.9   50.8  1819   ohc   four   92 1bbl  2.91  3.41  9.20
    ## 32    150.0   64.0   52.6  1837   ohc   four   79 1bbl  2.91  3.07 10.10
    ## 33    150.0   64.0   52.6  1940   ohc   four   92 1bbl  2.91  3.41  9.20
    ## 34    150.0   64.0   52.6  1956   ohc   four   92 1bbl  2.91  3.41  9.20
    ## 35    163.4   64.0   54.5  2010   ohc   four   92 1bbl  2.91  3.41  9.20
    ## 36    157.1   63.9   58.3  2024   ohc   four   92 1bbl  2.92  3.41  9.20
    ## 37    167.5   65.2   53.3  2236   ohc   four  110 1bbl  3.15  3.58  9.00
    ## 38    167.5   65.2   53.3  2289   ohc   four  110 1bbl  3.15  3.58  9.00
    ## 39    175.4   65.2   54.1  2304   ohc   four  110 1bbl  3.15  3.58  9.00
    ## 40    175.4   62.5   54.1  2372   ohc   four  110 1bbl  3.15  3.58  9.00
    ## 41    175.4   65.2   54.1  2465   ohc   four  110 mpfi  3.15  3.58  9.00
    ## 42    169.1   66.0   51.0  2293   ohc   four  110 2bbl  3.15  3.58  9.10
    ## 43    170.7   61.8   53.5  2337   ohc   four  111 2bbl  3.31  3.23  8.50
    ## 44    155.9   63.6   52.0  1874   ohc   four   90 2bbl  3.03  3.11  9.60
    ## 45    155.9   63.6   52.0  1909   ohc   four   90 2bbl  3.03  3.11  9.60
    ## 46    172.6   65.2   51.4  2734   ohc   four  119 spfi  3.43  3.23  9.20
    ## 47    199.6   69.6   52.8  4066  dohc    six  258 mpfi  3.63  4.17  8.10
    ## 48    199.6   69.6   52.8  4066  dohc    six  258 mpfi  3.63  4.17  8.10
    ## 49    191.7   70.6   47.8  3950  ohcv twelve  326 mpfi  3.54  2.76 11.50
    ## 50    159.1   64.2   54.1  1890   ohc   four   91 2bbl  3.03  3.15  9.00
    ## 51    159.1   64.2   54.1  1900   ohc   four   91 2bbl  3.03  3.15  9.00
    ## 52    159.1   64.2   54.1  1905   ohc   four   91 2bbl  3.03  3.15  9.00
    ## 53    166.8   64.2   54.1  1945   ohc   four   91 2bbl  3.03  3.15  9.00
    ## 54    166.8   64.2   54.1  1950   ohc   four   91 2bbl  3.08  3.15  9.00
    ## 55    169.0   65.7   49.6  2380 rotor    two   70 4bbl     ?     ?  9.40
    ## 56    169.0   65.7   49.6  2380 rotor    two   70 4bbl     ?     ?  9.40
    ## 57    169.0   65.7   49.6  2385 rotor    two   70 4bbl     ?     ?  9.40
    ## 58    169.0   65.7   49.6  2500 rotor    two   80 mpfi     ?     ?  9.40
    ## 59    177.8   66.5   53.7  2385   ohc   four  122 2bbl  3.39  3.39  8.60
    ## 60    177.8   66.5   55.5  2410   ohc   four  122 2bbl  3.39  3.39  8.60
    ## 61    177.8   66.5   53.7  2385   ohc   four  122 2bbl  3.39  3.39  8.60
    ## 62    177.8   66.5   55.5  2410   ohc   four  122 2bbl  3.39  3.39  8.60
    ## 63    177.8   66.5   55.5  2443   ohc   four  122  idi  3.39  3.39 22.70
    ## 64    177.8   66.5   55.5  2425   ohc   four  122 2bbl  3.39  3.39  8.60
    ## 65    175.0   66.1   54.4  2670   ohc   four  140 mpfi  3.76  3.16  8.00
    ## 66    175.0   66.1   54.4  2700   ohc   four  134  idi  3.43  3.64 22.00
    ## 67    190.9   70.3   56.5  3515   ohc   five  183  idi  3.58  3.64 21.50
    ## 68    190.9   70.3   58.7  3750   ohc   five  183  idi  3.58  3.64 21.50
    ## 69    187.5   70.3   54.9  3495   ohc   five  183  idi  3.58  3.64 21.50
    ## 70    202.6   71.7   56.3  3770   ohc   five  183  idi  3.58  3.64 21.50
    ## 71    202.6   71.7   56.5  3740  ohcv  eight  234 mpfi  3.46  3.10  8.30
    ## 72    180.3   70.5   50.8  3685  ohcv  eight  234 mpfi  3.46  3.10  8.30
    ## 73    208.1   71.7   56.7  3900  ohcv  eight  308 mpfi  3.80  3.35  8.00
    ## 74    199.2   72.0   55.4  3715  ohcv  eight  304 mpfi  3.80  3.35  8.00
    ## 75    178.4   68.0   54.8  2910   ohc   four  140 mpfi  3.78  3.12  8.00
    ## 76    157.3   64.4   50.8  1918   ohc   four   92 2bbl  2.97  3.23  9.40
    ## 77    157.3   64.4   50.8  1944   ohc   four   92 2bbl  2.97  3.23  9.40
    ## 78    157.3   64.4   50.8  2004   ohc   four   92 2bbl  2.97  3.23  9.40
    ## 79    157.3   63.8   50.8  2145   ohc   four   98 spdi  3.03  3.39  7.60
    ## 80    173.0   65.4   49.4  2370   ohc   four  110 spdi  3.17  3.46  7.50
    ## 81    173.0   65.4   49.4  2328   ohc   four  122 2bbl  3.35  3.46  8.50
    ## 82    173.2   66.3   50.2  2833   ohc   four  156 spdi  3.58  3.86  7.00
    ## 83    173.2   66.3   50.2  2921   ohc   four  156 spdi  3.59  3.86  7.00
    ## 84    173.2   66.3   50.2  2926   ohc   four  156 spdi  3.59  3.86  7.00
    ## 85    172.4   65.4   51.6  2365   ohc   four  122 2bbl  3.35  3.46  8.50
    ## 86    172.4   65.4   51.6  2405   ohc   four  122 2bbl  3.35  3.46  8.50
    ## 87    172.4   65.4   51.6  2403   ohc   four  110 spdi  3.17  3.46  7.50
    ## 88    172.4   65.4   51.6  2403   ohc   four  110 spdi  3.17  3.46  7.50
    ## 89    165.3   63.8   54.5  1889   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 90    165.3   63.8   54.5  2017   ohc   four  103  idi  2.99  3.47 21.90
    ## 91    165.3   63.8   54.5  1918   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 92    165.3   63.8   54.5  1938   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 93    170.2   63.8   53.5  2024   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 94    165.3   63.8   54.5  1951   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 95    165.6   63.8   53.3  2028   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 96    165.3   63.8   54.5  1971   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 97    170.2   63.8   53.5  2037   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 98    162.4   63.8   53.3  2008   ohc   four   97 2bbl  3.15  3.29  9.40
    ## 99    173.4   65.2   54.7  2324   ohc   four  120 2bbl  3.33  3.47  8.50
    ## 100   173.4   65.2   54.7  2302   ohc   four  120 2bbl  3.33  3.47  8.50
    ## 101   181.7   66.5   55.1  3095  ohcv    six  181 mpfi  3.43  3.27  9.00
    ## 102   184.6   66.5   56.1  3296  ohcv    six  181 mpfi  3.43  3.27  9.00
    ## 103   184.6   66.5   55.1  3060  ohcv    six  181 mpfi  3.43  3.27  9.00
    ## 104   170.7   67.9   49.7  3071  ohcv    six  181 mpfi  3.43  3.27  9.00
    ## 105   170.7   67.9   49.7  3139  ohcv    six  181 mpfi  3.43  3.27  7.80
    ## 106   178.5   67.9   49.7  3139  ohcv    six  181 mpfi  3.43  3.27  9.00
    ## 107   186.7   68.4   56.7  3020     l   four  120 mpfi  3.46  3.19  8.40
    ## 108   186.7   68.4   56.7  3197     l   four  152  idi  3.70  3.52 21.00
    ## 109   198.9   68.4   58.7  3230     l   four  120 mpfi  3.46  3.19  8.40
    ## 110   198.9   68.4   58.7  3430     l   four  152  idi  3.70  3.52 21.00
    ## 111   186.7   68.4   56.7  3075     l   four  120 mpfi  3.46  2.19  8.40
    ## 112   186.7   68.4   56.7  3252     l   four  152  idi  3.70  3.52 21.00
    ## 113   198.9   68.4   56.7  3285     l   four  120 mpfi  3.46  2.19  8.40
    ## 114   198.9   68.4   58.7  3485     l   four  152  idi  3.70  3.52 21.00
    ## 115   186.7   68.4   56.7  3075     l   four  120 mpfi  3.46  3.19  8.40
    ## 116   186.7   68.4   56.7  3252     l   four  152  idi  3.70  3.52 21.00
    ## 117   186.7   68.3   56.0  3130     l   four  134 mpfi  3.61  3.21  7.00
    ## 118   157.3   63.8   50.8  1918   ohc   four   90 2bbl  2.97  3.23  9.40
    ## 119   157.3   63.8   50.8  2128   ohc   four   98 spdi  3.03  3.39  7.60
    ## 120   157.3   63.8   50.6  1967   ohc   four   90 2bbl  2.97  3.23  9.40
    ## 121   167.3   63.8   50.8  1989   ohc   four   90 2bbl  2.97  3.23  9.40
    ## 122   167.3   63.8   50.8  2191   ohc   four   98 2bbl  2.97  3.23  9.40
    ## 123   174.6   64.6   59.8  2535   ohc   four  122 2bbl  3.35  3.46  8.50
    ## 124   173.2   66.3   50.2  2818   ohc   four  156 spdi  3.59  3.86  7.00
    ## 125   168.9   68.3   50.2  2778   ohc   four  151 mpfi  3.94  3.11  9.50
    ## 126   168.9   65.0   51.6  2756  ohcf    six  194 mpfi  3.74  2.90  9.50
    ## 127   168.9   65.0   51.6  2756  ohcf    six  194 mpfi  3.74  2.90  9.50
    ## 128   168.9   65.0   51.6  2800  ohcf    six  194 mpfi  3.74  2.90  9.50
    ## 129   175.7   72.3   50.5  3366 dohcv  eight  203 mpfi  3.94  3.11 10.00
    ## 130   181.5   66.5   55.2  2579   ohc   four  132 mpfi  3.46  3.90  8.70
    ## 131   176.8   66.6   50.5  2460   ohc   four  132 mpfi  3.46  3.90  8.70
    ## 132   186.6   66.5   56.1  2658   ohc   four  121 mpfi  3.54  3.07  9.31
    ## 133   186.6   66.5   56.1  2695   ohc   four  121 mpfi  3.54  3.07  9.30
    ## 134   186.6   66.5   56.1  2707   ohc   four  121 mpfi  2.54  2.07  9.30
    ## 135   186.6   66.5   56.1  2758   ohc   four  121 mpfi  3.54  3.07  9.30
    ## 136   186.6   66.5   56.1  2808  dohc   four  121 mpfi  3.54  3.07  9.00
    ## 137   186.6   66.5   56.1  2847  dohc   four  121 mpfi  3.54  3.07  9.00
    ## 138   156.9   63.4   53.7  2050  ohcf   four   97 2bbl  3.62  2.36  9.00
    ## 139   157.9   63.6   53.7  2120  ohcf   four  108 2bbl  3.62  2.64  8.70
    ## 140   157.3   63.8   55.7  2240  ohcf   four  108 2bbl  3.62  2.64  8.70
    ## 141   172.0   65.4   52.5  2145  ohcf   four  108 2bbl  3.62  2.64  9.50
    ## 142   172.0   65.4   52.5  2190  ohcf   four  108 2bbl  3.62  2.64  9.50
    ## 143   172.0   65.4   52.5  2340  ohcf   four  108 mpfi  3.62  2.64  9.00
    ## 144   172.0   65.4   54.3  2385  ohcf   four  108 2bbl  3.62  2.64  9.00
    ## 145   172.0   65.4   54.3  2510  ohcf   four  108 mpfi  3.62  2.64  7.70
    ## 146   173.5   65.4   53.0  2290  ohcf   four  108 2bbl  3.62  2.64  9.00
    ## 147   173.5   65.4   53.0  2455  ohcf   four  108 mpfi  3.62  2.64  9.00
    ## 148   173.6   65.4   54.9  2420  ohcf   four  108 2bbl  3.62  2.64  9.00
    ## 149   173.6   65.4   54.9  2650  ohcf   four  108 mpfi  3.62  2.64  7.70
    ## 150   158.7   63.6   54.5  1985   ohc   four   92 2bbl  3.05  3.03  9.00
    ## 151   158.7   63.6   54.5  2040   ohc   four   92 2bbl  3.05  3.03  9.00
    ## 152   158.7   63.6   54.5  2015   ohc   four   92 2bbl  3.05  3.03  9.00
    ## 153   169.7   63.6   59.1  2280   ohc   four   92 2bbl  3.05  3.03  9.00
    ## 154   169.7   63.6   59.1  2290   ohc   four   92 2bbl  3.05  3.03  9.00
    ## 155   169.7   63.6   59.1  3110   ohc   four   92 2bbl  3.05  3.03  9.00
    ## 156   166.3   64.4   53.0  2081   ohc   four   98 2bbl  3.19  3.03  9.00
    ## 157   166.3   64.4   52.8  2109   ohc   four   98 2bbl  3.19  3.03  9.00
    ## 158   166.3   64.4   53.0  2275   ohc   four  110  idi  3.27  3.35 22.50
    ## 159   166.3   64.4   52.8  2275   ohc   four  110  idi  3.27  3.35 22.50
    ## 160   166.3   64.4   53.0  2094   ohc   four   98 2bbl  3.19  3.03  9.00
    ## 161   166.3   64.4   52.8  2122   ohc   four   98 2bbl  3.19  3.03  9.00
    ## 162   166.3   64.4   52.8  2140   ohc   four   98 2bbl  3.19  3.03  9.00
    ## 163   168.7   64.0   52.6  2169   ohc   four   98 2bbl  3.19  3.03  9.00
    ## 164   168.7   64.0   52.6  2204   ohc   four   98 2bbl  3.19  3.03  9.00
    ## 165   168.7   64.0   52.6  2265  dohc   four   98 mpfi  3.24  3.08  9.40
    ## 166   168.7   64.0   52.6  2300  dohc   four   98 mpfi  3.24  3.08  9.40
    ## 167   176.2   65.6   52.0  2540   ohc   four  146 mpfi  3.62  3.50  9.30
    ## 168   176.2   65.6   52.0  2536   ohc   four  146 mpfi  3.62  3.50  9.30
    ## 169   176.2   65.6   52.0  2551   ohc   four  146 mpfi  3.62  3.50  9.30
    ## 170   176.2   65.6   52.0  2679   ohc   four  146 mpfi  3.62  3.50  9.30
    ## 171   176.2   65.6   52.0  2714   ohc   four  146 mpfi  3.62  3.50  9.30
    ## 172   176.2   65.6   53.0  2975   ohc   four  146 mpfi  3.62  3.50  9.30
    ## 173   175.6   66.5   54.9  2326   ohc   four  122 mpfi  3.31  3.54  8.70
    ## 174   175.6   66.5   54.9  2480   ohc   four  110  idi  3.27  3.35 22.50
    ## 175   175.6   66.5   53.9  2414   ohc   four  122 mpfi  3.31  3.54  8.70
    ## 176   175.6   66.5   54.9  2414   ohc   four  122 mpfi  3.31  3.54  8.70
    ## 177   175.6   66.5   53.9  2458   ohc   four  122 mpfi  3.31  3.54  8.70
    ## 178   183.5   67.7   52.0  2976  dohc    six  171 mpfi  3.27  3.35  9.30
    ## 179   183.5   67.7   52.0  3016  dohc    six  171 mpfi  3.27  3.35  9.30
    ## 180   187.8   66.5   54.1  3131  dohc    six  171 mpfi  3.27  3.35  9.20
    ## 181   187.8   66.5   54.1  3151  dohc    six  161 mpfi  3.27  3.35  9.20
    ## 182   171.7   65.5   55.7  2261   ohc   four   97  idi  3.01  3.40 23.00
    ## 183   171.7   65.5   55.7  2209   ohc   four  109 mpfi  3.19  3.40  9.00
    ## 184   171.7   65.5   55.7  2264   ohc   four   97  idi  3.01  3.40 23.00
    ## 185   171.7   65.5   55.7  2212   ohc   four  109 mpfi  3.19  3.40  9.00
    ## 186   171.7   65.5   55.7  2275   ohc   four  109 mpfi  3.19  3.40  9.00
    ## 187   171.7   65.5   55.7  2319   ohc   four   97  idi  3.01  3.40 23.00
    ## 188   171.7   65.5   55.7  2300   ohc   four  109 mpfi  3.19  3.40 10.00
    ## 189   159.3   64.2   55.6  2254   ohc   four  109 mpfi  3.19  3.40  8.50
    ## 190   165.7   64.0   51.4  2221   ohc   four  109 mpfi  3.19  3.40  8.50
    ## 191   180.2   66.9   55.1  2661   ohc   five  136 mpfi  3.19  3.40  8.50
    ## 192   180.2   66.9   55.1  2579   ohc   four   97  idi  3.01  3.40 23.00
    ## 193   183.1   66.9   55.1  2563   ohc   four  109 mpfi  3.19  3.40  9.00
    ## 194   188.8   67.2   56.2  2912   ohc   four  141 mpfi  3.78  3.15  9.50
    ## 195   188.8   67.2   57.5  3034   ohc   four  141 mpfi  3.78  3.15  9.50
    ## 196   188.8   67.2   56.2  2935   ohc   four  141 mpfi  3.78  3.15  9.50
    ## 197   188.8   67.2   57.5  3042   ohc   four  141 mpfi  3.78  3.15  9.50
    ## 198   188.8   67.2   56.2  3045   ohc   four  130 mpfi  3.62  3.15  7.50
    ## 199   188.8   67.2   57.5  3157   ohc   four  130 mpfi  3.62  3.15  7.50
    ## 200   188.8   68.9   55.5  2952   ohc   four  141 mpfi  3.78  3.15  9.50
    ## 201   188.8   68.8   55.5  3049   ohc   four  141 mpfi  3.78  3.15  8.70
    ## 202   188.8   68.9   55.5  3012  ohcv    six  173 mpfi  3.58  2.87  8.80
    ## 203   188.8   68.9   55.5  3217   ohc    six  145  idi  3.01  3.40 23.00
    ## 204   188.8   68.9   55.5  3062   ohc   four  141 mpfi  3.78  3.15  9.50
    ##     X111 X5000 X21 X27 X13495
    ## 1    111  5000  21  27  16500
    ## 2    154  5000  19  26  16500
    ## 3    102  5500  24  30  13950
    ## 4    115  5500  18  22  17450
    ## 5    110  5500  19  25  15250
    ## 6    110  5500  19  25  17710
    ## 7    110  5500  19  25  18920
    ## 8    140  5500  17  20  23875
    ## 9    160  5500  16  22      ?
    ## 10   101  5800  23  29  16430
    ## 11   101  5800  23  29  16925
    ## 12   121  4250  21  28  20970
    ## 13   121  4250  21  28  21105
    ## 14   121  4250  20  25  24565
    ## 15   182  5400  16  22  30760
    ## 16   182  5400  16  22  41315
    ## 17   182  5400  15  20  36880
    ## 18    48  5100  47  53   5151
    ## 19    70  5400  38  43   6295
    ## 20    70  5400  38  43   6575
    ## 21    68  5500  37  41   5572
    ## 22    68  5500  31  38   6377
    ## 23   102  5500  24  30   7957
    ## 24    68  5500  31  38   6229
    ## 25    68  5500  31  38   6692
    ## 26    68  5500  31  38   7609
    ## 27   102  5500  24  30   8558
    ## 28    88  5000  24  30   8921
    ## 29   145  5000  19  24  12964
    ## 30    58  4800  49  54   6479
    ## 31    76  6000  31  38   6855
    ## 32    60  5500  38  42   5399
    ## 33    76  6000  30  34   6529
    ## 34    76  6000  30  34   7129
    ## 35    76  6000  30  34   7295
    ## 36    76  6000  30  34   7295
    ## 37    86  5800  27  33   7895
    ## 38    86  5800  27  33   9095
    ## 39    86  5800  27  33   8845
    ## 40    86  5800  27  33  10295
    ## 41   101  5800  24  28  12945
    ## 42   100  5500  25  31  10345
    ## 43    78  4800  24  29   6785
    ## 44    70  5400  38  43      ?
    ## 45    70  5400  38  43      ?
    ## 46    90  5000  24  29  11048
    ## 47   176  4750  15  19  32250
    ## 48   176  4750  15  19  35550
    ## 49   262  5000  13  17  36000
    ## 50    68  5000  30  31   5195
    ## 51    68  5000  31  38   6095
    ## 52    68  5000  31  38   6795
    ## 53    68  5000  31  38   6695
    ## 54    68  5000  31  38   7395
    ## 55   101  6000  17  23  10945
    ## 56   101  6000  17  23  11845
    ## 57   101  6000  17  23  13645
    ## 58   135  6000  16  23  15645
    ## 59    84  4800  26  32   8845
    ## 60    84  4800  26  32   8495
    ## 61    84  4800  26  32  10595
    ## 62    84  4800  26  32  10245
    ## 63    64  4650  36  42  10795
    ## 64    84  4800  26  32  11245
    ## 65   120  5000  19  27  18280
    ## 66    72  4200  31  39  18344
    ## 67   123  4350  22  25  25552
    ## 68   123  4350  22  25  28248
    ## 69   123  4350  22  25  28176
    ## 70   123  4350  22  25  31600
    ## 71   155  4750  16  18  34184
    ## 72   155  4750  16  18  35056
    ## 73   184  4500  14  16  40960
    ## 74   184  4500  14  16  45400
    ## 75   175  5000  19  24  16503
    ## 76    68  5500  37  41   5389
    ## 77    68  5500  31  38   6189
    ## 78    68  5500  31  38   6669
    ## 79   102  5500  24  30   7689
    ## 80   116  5500  23  30   9959
    ## 81    88  5000  25  32   8499
    ## 82   145  5000  19  24  12629
    ## 83   145  5000  19  24  14869
    ## 84   145  5000  19  24  14489
    ## 85    88  5000  25  32   6989
    ## 86    88  5000  25  32   8189
    ## 87   116  5500  23  30   9279
    ## 88   116  5500  23  30   9279
    ## 89    69  5200  31  37   5499
    ## 90    55  4800  45  50   7099
    ## 91    69  5200  31  37   6649
    ## 92    69  5200  31  37   6849
    ## 93    69  5200  31  37   7349
    ## 94    69  5200  31  37   7299
    ## 95    69  5200  31  37   7799
    ## 96    69  5200  31  37   7499
    ## 97    69  5200  31  37   7999
    ## 98    69  5200  31  37   8249
    ## 99    97  5200  27  34   8949
    ## 100   97  5200  27  34   9549
    ## 101  152  5200  17  22  13499
    ## 102  152  5200  17  22  14399
    ## 103  152  5200  19  25  13499
    ## 104  160  5200  19  25  17199
    ## 105  200  5200  17  23  19699
    ## 106  160  5200  19  25  18399
    ## 107   97  5000  19  24  11900
    ## 108   95  4150  28  33  13200
    ## 109   97  5000  19  24  12440
    ## 110   95  4150  25  25  13860
    ## 111   95  5000  19  24  15580
    ## 112   95  4150  28  33  16900
    ## 113   95  5000  19  24  16695
    ## 114   95  4150  25  25  17075
    ## 115   97  5000  19  24  16630
    ## 116   95  4150  28  33  17950
    ## 117  142  5600  18  24  18150
    ## 118   68  5500  37  41   5572
    ## 119  102  5500  24  30   7957
    ## 120   68  5500  31  38   6229
    ## 121   68  5500  31  38   6692
    ## 122   68  5500  31  38   7609
    ## 123   88  5000  24  30   8921
    ## 124  145  5000  19  24  12764
    ## 125  143  5500  19  27  22018
    ## 126  207  5900  17  25  32528
    ## 127  207  5900  17  25  34028
    ## 128  207  5900  17  25  37028
    ## 129  288  5750  17  28      ?
    ## 130    ?     ?  23  31   9295
    ## 131    ?     ?  23  31   9895
    ## 132  110  5250  21  28  11850
    ## 133  110  5250  21  28  12170
    ## 134  110  5250  21  28  15040
    ## 135  110  5250  21  28  15510
    ## 136  160  5500  19  26  18150
    ## 137  160  5500  19  26  18620
    ## 138   69  4900  31  36   5118
    ## 139   73  4400  26  31   7053
    ## 140   73  4400  26  31   7603
    ## 141   82  4800  32  37   7126
    ## 142   82  4400  28  33   7775
    ## 143   94  5200  26  32   9960
    ## 144   82  4800  24  25   9233
    ## 145  111  4800  24  29  11259
    ## 146   82  4800  28  32   7463
    ## 147   94  5200  25  31  10198
    ## 148   82  4800  23  29   8013
    ## 149  111  4800  23  23  11694
    ## 150   62  4800  35  39   5348
    ## 151   62  4800  31  38   6338
    ## 152   62  4800  31  38   6488
    ## 153   62  4800  31  37   6918
    ## 154   62  4800  27  32   7898
    ## 155   62  4800  27  32   8778
    ## 156   70  4800  30  37   6938
    ## 157   70  4800  30  37   7198
    ## 158   56  4500  34  36   7898
    ## 159   56  4500  38  47   7788
    ## 160   70  4800  38  47   7738
    ## 161   70  4800  28  34   8358
    ## 162   70  4800  28  34   9258
    ## 163   70  4800  29  34   8058
    ## 164   70  4800  29  34   8238
    ## 165  112  6600  26  29   9298
    ## 166  112  6600  26  29   9538
    ## 167  116  4800  24  30   8449
    ## 168  116  4800  24  30   9639
    ## 169  116  4800  24  30   9989
    ## 170  116  4800  24  30  11199
    ## 171  116  4800  24  30  11549
    ## 172  116  4800  24  30  17669
    ## 173   92  4200  29  34   8948
    ## 174   73  4500  30  33  10698
    ## 175   92  4200  27  32   9988
    ## 176   92  4200  27  32  10898
    ## 177   92  4200  27  32  11248
    ## 178  161  5200  20  24  16558
    ## 179  161  5200  19  24  15998
    ## 180  156  5200  20  24  15690
    ## 181  156  5200  19  24  15750
    ## 182   52  4800  37  46   7775
    ## 183   85  5250  27  34   7975
    ## 184   52  4800  37  46   7995
    ## 185   85  5250  27  34   8195
    ## 186   85  5250  27  34   8495
    ## 187   68  4500  37  42   9495
    ## 188  100  5500  26  32   9995
    ## 189   90  5500  24  29  11595
    ## 190   90  5500  24  29   9980
    ## 191  110  5500  19  24  13295
    ## 192   68  4500  33  38  13845
    ## 193   88  5500  25  31  12290
    ## 194  114  5400  23  28  12940
    ## 195  114  5400  23  28  13415
    ## 196  114  5400  24  28  15985
    ## 197  114  5400  24  28  16515
    ## 198  162  5100  17  22  18420
    ## 199  162  5100  17  22  18950
    ## 200  114  5400  23  28  16845
    ## 201  160  5300  19  25  19045
    ## 202  134  5500  18  23  21485
    ## 203  106  4800  26  27  22470
    ## 204  114  5400  19  25  22625

``` r
column_names <- c(
         'symboling',
         'normalized_losses',
         'make',
         'fuel_type',
         'aspiration',
         'num_of_doors',
         'body_style',
         'drive_wheels',
         'engine_location',
         'wheel_base',
         'length',
         'width',
         'height',
         'curb_weight',
         'engine_type',
         'num_of_cylinders',
         'engine_size',
         'fuel_system',
         'bore',
         'stroke',
         'compression_ratio',
         'horsepower',
         'peak_rpm',
         'city_mpg',
         'highway_mpg',
         'price')

col_types <- cols(col_double(),
              col_double(),
              col_character(),
              col_character(),
              col_character(),
              col_character(),
              col_character(),
              col_character(),
              col_character(),
              col_double(),
              col_double(),
              col_double(),
              col_double(),
              col_integer(),
              col_character(),
              col_character(),
              col_integer(),
              col_character(),
              col_double(),
              col_double(),
              col_double(),
              col_integer(),
              col_integer(),
              col_integer(),
              col_integer(),
              col_integer()
              )

dat <- read_csv('imports-85.data', column_names, col_types)
```

    ## Warning in rbind(names(probs), probs_f): number of columns of result is not
    ## a multiple of vector length (arg 1)

    ## Warning: 57 parsing failures.
    ## row # A tibble: 5 x 5 col     row               col expected actual              file expected   <int>             <chr>    <chr>  <chr>             <chr> actual 1     1 normalized_losses a double      ? 'imports-85.data' file 2     2 normalized_losses a double      ? 'imports-85.data' row 3     3 normalized_losses a double      ? 'imports-85.data' col 4     6 normalized_losses a double      ? 'imports-85.data' expected 5     8 normalized_losses a double      ? 'imports-85.data'
    ## ... ................. ... ........................................................... ........ ........................................................... ...... ........................................................... .... ........................................................... ... ........................................................... ... ........................................................... ........ ...........................................................
    ## See problems(...) for more details.

``` r
str("imports-85.data, vec.len = 1")
```

    ##  chr "imports-85.data, vec.len = 1"

``` r
dat
```

    ## # A tibble: 205 x 26
    ##    symboling normalized_losses        make fuel_type aspiration
    ##        <dbl>             <dbl>       <chr>     <chr>      <chr>
    ##  1         3                NA alfa-romero       gas        std
    ##  2         3                NA alfa-romero       gas        std
    ##  3         1                NA alfa-romero       gas        std
    ##  4         2               164        audi       gas        std
    ##  5         2               164        audi       gas        std
    ##  6         2                NA        audi       gas        std
    ##  7         1               158        audi       gas        std
    ##  8         1                NA        audi       gas        std
    ##  9         1               158        audi       gas      turbo
    ## 10         0                NA        audi       gas      turbo
    ## # ... with 195 more rows, and 21 more variables: num_of_doors <chr>,
    ## #   body_style <chr>, drive_wheels <chr>, engine_location <chr>,
    ## #   wheel_base <dbl>, length <dbl>, width <dbl>, height <dbl>,
    ## #   curb_weight <int>, engine_type <chr>, num_of_cylinders <chr>,
    ## #   engine_size <int>, fuel_system <chr>, bore <dbl>, stroke <dbl>,
    ## #   compression_ratio <dbl>, horsepower <int>, peak_rpm <int>,
    ## #   city_mpg <int>, highway_mpg <int>, price <int>

3) Technical Questions about importing data (10 pts)
====================================================

Answer the following questions (using your own words). You do NOT need to include any commands.
-----------------------------------------------------------------------------------------------

a. If you don’t provide a vector of column names, what happens to the column names of the imported data when you simply invoke read.csv('imports-85.data')?
-----------------------------------------------------------------------------------------------------------------------------------------------------------

-   It will show you the info of first column on the header.

b. If you don’t provide a vector of column names, what happens to the column names of the imported data when you invoke read.csv('imports-85.data', header = FALSE)?
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   You will have a list of vectors on the header. ex. V1, V2, etc.

c. When using the reading table functions, if you don’t specify how missing values are codified, what happens to the data type of those columns that contain '?', e.g. price or num\_of\_doors?
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   It shows "NA"

d. Say you import imports-85.data in two different ways. In the first option you import the data without specifying the data type of each column. In the second option you do specify the data types. You may wonder whether both options return a data frame of the same memory size. You can actually use the function object.size() that provides an estimate of the memory that is being used to store an R object. Why is the data frame imported in the first option bigger (in terms of bytes) than the data frame imported in the second option?
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   If we do not specify the data types, the r will download each data, eg. 4 MB. Otherwise, r combines the same data type from each column and download it as a whole, the total storage will be the same as download one data, 4MB.

e. Say the object dat is the data frame produced when importing imports-85.data. What happens to the data values if you convert dat as an R matrix?
---------------------------------------------------------------------------------------------------------------------------------------------------

-   Logical and factor columns are converted to integers. Any other column which is not numeric (according to is.numeric) is converted by as.numeric or, for S4 objects, as(, "numeric"). If all columns are integer (after conversion) the result is an integer matrix, otherwise a numeric (double) matrix.

4) Practice base plotting (10 pts)
==================================

``` r
#histogram of price with colored bars.

hist(dat$price, main = "Histogram for price", xlab = "price", ylab = "Count", col = "yellow")
```

![](hw01-molly-li_files/figure-markdown_github/unnamed-chunk-4-1.png)

``` r
#boxplot of horsepower in horizontal orientation.
boxplot(dat$horsepower,  main = "Horsepower", col = "blue", horizontal = T)
```

![](hw01-molly-li_files/figure-markdown_github/unnamed-chunk-5-1.png)

``` r
#barplot of the frequencies of body_style, arranged in decreasing order.
bodystyle <- dat$body_style
bodystyle.freq <- table(bodystyle)
print(bodystyle.freq)
```

    ## bodystyle
    ## convertible     hardtop   hatchback       sedan       wagon 
    ##           6           8          70          96          25

``` r
barplot(sort(bodystyle.freq, decreasing = TRUE), main = "Frequence of Body Style", col="green")
```

![](hw01-molly-li_files/figure-markdown_github/unnamed-chunk-6-1.png)

``` r
# stars() plot of vehicles with turbo aspiration, using only variables wheel-base,length, width, height, and price.
stars(dat[dat$aspiration == 'turbo', c(10:13,26)])
```

![](hw01-molly-li_files/figure-markdown_github/unnamed-chunk-7-1.png)

5) Summaries (10 pts)
=====================

``` r
#a. What is the mean price of fuel_type gas cars? And what is the mean price of fuel_type diesel cars? (removing missing values)
price_gascar <- dat$price[dat$fuel_type =="gas"]
print(price_gascar)
```

    ##   [1] 13495 16500 16500 13950 17450 15250 17710 18920 23875    NA 16430
    ##  [12] 16925 20970 21105 24565 30760 41315 36880  5151  6295  6575  5572
    ##  [23]  6377  7957  6229  6692  7609  8558  8921 12964  6479  6855  5399
    ##  [34]  6529  7129  7295  7295  7895  9095  8845 10295 12945 10345  6785
    ##  [45]    NA    NA 11048 32250 35550 36000  5195  6095  6795  6695  7395
    ##  [56] 10945 11845 13645 15645  8845  8495 10595 10245 11245 18280 34184
    ##  [67] 35056 40960 45400 16503  5389  6189  6669  7689  9959  8499 12629
    ##  [78] 14869 14489  6989  8189  9279  9279  5499  6649  6849  7349  7299
    ##  [89]  7799  7499  7999  8249  8949  9549 13499 14399 13499 17199 19699
    ## [100] 18399 11900 12440 15580 16695 16630 18150  5572  7957  6229  6692
    ## [111]  7609  8921 12764 22018 32528 34028 37028    NA  9295  9895 11850
    ## [122] 12170 15040 15510 18150 18620  5118  7053  7603  7126  7775  9960
    ## [133]  9233 11259  7463 10198  8013 11694  5348  6338  6488  6918  7898
    ## [144]  8778  6938  7198  7738  8358  9258  8058  8238  9298  9538  8449
    ## [155]  9639  9989 11199 11549 17669  8948  9988 10898 11248 16558 15998
    ## [166] 15690 15750  7975  8195  8495  9995 11595  9980 13295 12290 12940
    ## [177] 13415 15985 16515 18420 18950 16845 19045 21485 22625

``` r
mean(price_gascar,na.rm=TRUE)
```

    ## [1] 12916.41

``` r
#b.What is the make of the car with twelve num_of_cylinders?
dat$make[dat$num_of_cylinders == "twelve"]
```

    ## [1] "jaguar"

diselcar &lt;- filter('imports-85.data', dat*m**a**k**e*, *d**a**t*fuel\_type == "diesel") count(dat$fuel\_type =="diesel", na.rm=TRUE) bodystyle &lt;- dat$body\_style bodystyle.freq &lt;- table(bodystyle) print(bodystyle.freq) barplot(sort(bodystyle.freq, decreasing = TRUE), main = "Frequence of Body Style", col="green") print(dieselcar)

``` r
#c. What is the make that has the most diesel cars?
dieselcar <- dat$make[dat$fuel_type =="diesel"]
diesel.freq <- table(dieselcar)
print(diesel.freq)
```

    ## dieselcar
    ##         mazda mercedes-benz        nissan        peugot        toyota 
    ##             2             4             1             5             3 
    ##    volkswagen         volvo 
    ##             4             1

``` r
head(sort(diesel.freq, decreasing = T),1)
```

    ## peugot 
    ##      5

``` r
#d. What is the price of the car with the largest amount of horsepower?
maxhorsepower <- max(dat$horsepower, na.rm=TRUE)
maxhorsepower
```

    ## [1] 288

``` r
price <- dat$price
price[maxhorsepower]
```

    ## [1] NA

``` r
#e. What is the bottom 10th percentile of city_mpg?
quantile(dat$city_mpg, .90)
```

    ##  90% 
    ## 31.6

``` r
#f. What is the top 10th percentile of highway_mpg?
quantile(dat$highway_mpg, .90)
```

    ## 90% 
    ##  38

``` r
#g. What is the median price of those cars in the bottom 10th percentile of city_mpg?
x <- quantile(dat$city_mpg, 0:.10)
median(x)
```

    ## [1] 13

6) Technical Questions about data frames (10 pts)
=================================================

Answer the following questions (using your own words). You do NOT need to include any commands.
-----------------------------------------------------------------------------------------------

a. What happens when you use the dollar $ operator on a data frame, attempting to use the name of a column that does not exist? For example: dat$xyz where there is no column named xyz.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

``` r
dat$xyz
```

    ## Warning: Unknown or uninitialised column: 'xyz'.

    ## NULL

-   It will say: "Unknown or uninitialised column: 'xyz'.NULL"

b. Which of the following commands fails to return the vector mpg which is a column in the built-in data rfame mtcars:
----------------------------------------------------------------------------------------------------------------------

1.  mtcars$mpg
2.  mtcars\[ ,1\]
3.  mtcars\[\[1\]\]
4.  mtcars\[ ,mpg\]
5.  mtcars\[\["mpg"\]\]
6.  mtcars$"mpg"
7.  mtcars\[ ,"mpg"\]

-   The forth one.

c. Based on your answer for part (b), what is the reason that makes such command to fail?
-----------------------------------------------------------------------------------------

-   "Error in .subset(x, j) : invalid subscript type 'list'"

d. Can you include an R list as a “column” of a data frame? YES or NO, and why.
-------------------------------------------------------------------------------

-   No. If a list or data frame or matrix is passed to ‘data.frame’ it is as if each component or column had been passed as a separate argument (except for matrices of class ‘"model.matrix"’ and those protected by ‘I’)

e. What happens when you apply as.list() to a data frame? e.g. as.list(mtcars)
------------------------------------------------------------------------------

``` r
as.list(mtcars)
```

    ## $mpg
    ##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2
    ## [15] 10.4 10.4 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4
    ## [29] 15.8 19.7 15.0 21.4
    ## 
    ## $cyl
    ##  [1] 6 6 4 6 8 6 8 4 4 6 6 8 8 8 8 8 8 4 4 4 4 8 8 8 8 4 4 4 8 6 8 4
    ## 
    ## $disp
    ##  [1] 160.0 160.0 108.0 258.0 360.0 225.0 360.0 146.7 140.8 167.6 167.6
    ## [12] 275.8 275.8 275.8 472.0 460.0 440.0  78.7  75.7  71.1 120.1 318.0
    ## [23] 304.0 350.0 400.0  79.0 120.3  95.1 351.0 145.0 301.0 121.0
    ## 
    ## $hp
    ##  [1] 110 110  93 110 175 105 245  62  95 123 123 180 180 180 205 215 230
    ## [18]  66  52  65  97 150 150 245 175  66  91 113 264 175 335 109
    ## 
    ## $drat
    ##  [1] 3.90 3.90 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 3.92 3.07 3.07 3.07
    ## [15] 2.93 3.00 3.23 4.08 4.93 4.22 3.70 2.76 3.15 3.73 3.08 4.08 4.43 3.77
    ## [29] 4.22 3.62 3.54 4.11
    ## 
    ## $wt
    ##  [1] 2.620 2.875 2.320 3.215 3.440 3.460 3.570 3.190 3.150 3.440 3.440
    ## [12] 4.070 3.730 3.780 5.250 5.424 5.345 2.200 1.615 1.835 2.465 3.520
    ## [23] 3.435 3.840 3.845 1.935 2.140 1.513 3.170 2.770 3.570 2.780
    ## 
    ## $qsec
    ##  [1] 16.46 17.02 18.61 19.44 17.02 20.22 15.84 20.00 22.90 18.30 18.90
    ## [12] 17.40 17.60 18.00 17.98 17.82 17.42 19.47 18.52 19.90 20.01 16.87
    ## [23] 17.30 15.41 17.05 18.90 16.70 16.90 14.50 15.50 14.60 18.60
    ## 
    ## $vs
    ##  [1] 0 0 1 1 0 1 0 1 1 1 1 0 0 0 0 0 0 1 1 1 1 0 0 0 0 1 0 1 0 0 0 1
    ## 
    ## $am
    ##  [1] 1 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 0 0 0 0 0 1 1 1 1 1 1 1
    ## 
    ## $gear
    ##  [1] 4 4 4 3 3 3 3 4 4 4 4 3 3 3 3 3 3 4 4 4 3 3 3 3 3 4 5 5 5 5 5 4
    ## 
    ## $carb
    ##  [1] 4 4 1 1 2 1 4 2 2 4 4 3 3 3 4 4 4 1 2 1 1 2 2 4 2 1 2 2 4 6 8 2

-   as.list attempts to coerce its argument to a list. For functions, this returns the concatenation of the list of formal arguments and the function body. For expressions, the list of constituent elements is returned. as.list is generic, and as the default method calls as.vector(mode = "list") for a non-list, methods for as.vector may be invoked. as.list turns a factor into a list of one-element factors. Attributes may be dropped unless the argument already is a list or expression. (This is inconsistent with functions such as as.character which always drop attributes, and is for efficiency since lists can be expensive to copy.)

f. Consider the command: abc &lt;- as.list(mtcars). What function(s) can you use to convert the object abc into a data frame?
-----------------------------------------------------------------------------------------------------------------------------

-   I can use 'data.frame(abc)' function

7) Correlations of quantitative variables (10 pts)
==================================================

``` r
qdat <- na.omit(dat)
qdat <- select(qdat, 
         wheel_base,
         length,
         width,
         height,
         curb_weight,
         engine_size,
         bore,
         stroke,
         compression_ratio,
         horsepower,
         peak_rpm,
         city_mpg,
         highway_mpg,
         price)
qdat
```

    ## # A tibble: 160 x 14
    ##    wheel_base length width height curb_weight engine_size  bore stroke
    ##         <dbl>  <dbl> <dbl>  <dbl>       <int>       <int> <dbl>  <dbl>
    ##  1       99.8  176.6  66.2   54.3        2337         109  3.19   3.40
    ##  2       99.4  176.6  66.4   54.3        2824         136  3.19   3.40
    ##  3      105.8  192.7  71.4   55.7        2844         136  3.19   3.40
    ##  4      105.8  192.7  71.4   55.9        3086         131  3.13   3.40
    ##  5      101.2  176.8  64.8   54.3        2395         108  3.50   2.80
    ##  6      101.2  176.8  64.8   54.3        2395         108  3.50   2.80
    ##  7      101.2  176.8  64.8   54.3        2710         164  3.31   3.19
    ##  8      101.2  176.8  64.8   54.3        2765         164  3.31   3.19
    ##  9       88.4  141.1  60.3   53.2        1488          61  2.91   3.03
    ## 10       94.5  155.9  63.6   52.0        1874          90  3.03   3.11
    ## # ... with 150 more rows, and 6 more variables: compression_ratio <dbl>,
    ## #   horsepower <int>, peak_rpm <int>, city_mpg <int>, highway_mpg <int>,
    ## #   price <int>

``` r
cor(qdat)
```

    ##                   wheel_base     length      width      height curb_weight
    ## wheel_base         1.0000000  0.8719680  0.8159350  0.55876376   0.8105069
    ## length             0.8719680  1.0000000  0.8391841  0.50515596   0.8703550
    ## width              0.8159350  0.8391841  1.0000000  0.29840309   0.8706493
    ## height             0.5587638  0.5051560  0.2984031  1.00000000   0.3693631
    ## curb_weight        0.8105069  0.8703550  0.8706493  0.36936307   1.0000000
    ## engine_size        0.6504878  0.7266664  0.7800176  0.11650514   0.8888474
    ## bore               0.5804840  0.6490592  0.5750480  0.26150092   0.6466403
    ## stroke             0.1640120  0.1160491  0.1928910 -0.09536437   0.1716913
    ## compression_ratio  0.2939676  0.1889678  0.2615303  0.23743151   0.2265128
    ## horsepower         0.5145069  0.6667260  0.6787789  0.03226392   0.7885094
    ## peak_rpm          -0.2924905 -0.2391043 -0.2359063 -0.25123623  -0.2620855
    ## city_mpg          -0.5766354 -0.7168766 -0.6621225 -0.19455902  -0.7595379
    ## highway_mpg       -0.6082698 -0.7178312 -0.6893674 -0.22164557  -0.7871670
    ## price              0.7347888  0.7603228  0.8433157  0.24750024   0.8938095
    ##                   engine_size        bore       stroke compression_ratio
    ## wheel_base          0.6504878  0.58048403  0.164011960        0.29396760
    ## length              0.7266664  0.64905924  0.116049120        0.18896778
    ## width               0.7800176  0.57504802  0.192891028        0.26153025
    ## height              0.1165051  0.26150092 -0.095364375        0.23743151
    ## curb_weight         0.8888474  0.64664028  0.171691317        0.22651275
    ## engine_size         1.0000000  0.59733622  0.296693139        0.14356771
    ## bore                0.5973362  1.00000000 -0.105464066        0.01921597
    ## stroke              0.2966931 -0.10546407  1.000000000        0.24089481
    ## compression_ratio   0.1435677  0.01921597  0.240894808        1.00000000
    ## horsepower          0.8098548  0.55710740  0.149314989       -0.16289361
    ## peak_rpm           -0.2872601 -0.31584138 -0.008568987       -0.41872632
    ## city_mpg           -0.6958896 -0.58561823 -0.021380833        0.27951325
    ## highway_mpg        -0.7113644 -0.58672907 -0.013974079        0.22244152
    ## price               0.8417248  0.53489078  0.158798229        0.21094844
    ##                    horsepower     peak_rpm    city_mpg highway_mpg
    ## wheel_base         0.51450686 -0.292490530 -0.57663540 -0.60826982
    ## length             0.66672597 -0.239104336 -0.71687663 -0.71783122
    ## width              0.67877892 -0.235906329 -0.66212250 -0.68936743
    ## height             0.03226392 -0.251236231 -0.19455902 -0.22164557
    ## curb_weight        0.78850942 -0.262085506 -0.75953792 -0.78716702
    ## engine_size        0.80985478 -0.287260069 -0.69588958 -0.71136436
    ## bore               0.55710740 -0.315841384 -0.58561823 -0.58672907
    ## stroke             0.14931499 -0.008568987 -0.02138083 -0.01397408
    ## compression_ratio -0.16289361 -0.418726319  0.27951325  0.22244152
    ## horsepower         1.00000000  0.074931817 -0.83717978 -0.82797250
    ## peak_rpm           0.07493182  1.000000000 -0.05493781 -0.03437238
    ## city_mpg          -0.83717978 -0.054937813  1.00000000  0.97199680
    ## highway_mpg       -0.82797250 -0.034372382  0.97199680  1.00000000
    ## price              0.75858227 -0.173970057 -0.69009981 -0.71831440
    ##                        price
    ## wheel_base         0.7347888
    ## length             0.7603228
    ## width              0.8433157
    ## height             0.2475002
    ## curb_weight        0.8938095
    ## engine_size        0.8417248
    ## bore               0.5348908
    ## stroke             0.1587982
    ## compression_ratio  0.2109484
    ## horsepower         0.7585823
    ## peak_rpm          -0.1739701
    ## city_mpg          -0.6900998
    ## highway_mpg       -0.7183144
    ## price              1.0000000

``` r
Q <- cor(qdat)
head(round(Q,2))
```

    ##             wheel_base length width height curb_weight engine_size bore
    ## wheel_base        1.00   0.87  0.82   0.56        0.81        0.65 0.58
    ## length            0.87   1.00  0.84   0.51        0.87        0.73 0.65
    ## width             0.82   0.84  1.00   0.30        0.87        0.78 0.58
    ## height            0.56   0.51  0.30   1.00        0.37        0.12 0.26
    ## curb_weight       0.81   0.87  0.87   0.37        1.00        0.89 0.65
    ## engine_size       0.65   0.73  0.78   0.12        0.89        1.00 0.60
    ##             stroke compression_ratio horsepower peak_rpm city_mpg
    ## wheel_base    0.16              0.29       0.51    -0.29    -0.58
    ## length        0.12              0.19       0.67    -0.24    -0.72
    ## width         0.19              0.26       0.68    -0.24    -0.66
    ## height       -0.10              0.24       0.03    -0.25    -0.19
    ## curb_weight   0.17              0.23       0.79    -0.26    -0.76
    ## engine_size   0.30              0.14       0.81    -0.29    -0.70
    ##             highway_mpg price
    ## wheel_base        -0.61  0.73
    ## length            -0.72  0.76
    ## width             -0.69  0.84
    ## height            -0.22  0.25
    ## curb_weight       -0.79  0.89
    ## engine_size       -0.71  0.84

``` r
corrplot(Q,method = "circle")
```

![](hw01-molly-li_files/figure-markdown_github/unnamed-chunk-20-1.png)

``` r
corrplot(Q, method="pie")
```

![](hw01-molly-li_files/figure-markdown_github/unnamed-chunk-21-1.png)

-   stoke and compression\_ration has weak correlation to other variables.
-   the value on the diagonal is always 1
-   wheel\_base,length,width,height have strong positive correlation to each other.

8) Principal Components Analysis (20 pts)
=========================================

8.1) Run PCA (10 pts)
---------------------

``` r
pca_prcomp <- prcomp(qdat, scale. = T)
```

``` r
pca_prcomp3 <- head(pca_prcomp, 3)
pca_prcomp3
```

    ## $sdev
    ##  [1] 2.7877785 1.4353835 1.1488991 0.9385966 0.7507065 0.6243506 0.5241135
    ##  [8] 0.4737293 0.3843980 0.3492757 0.2998213 0.2937309 0.2144806 0.1503868
    ## 
    ## $rotation
    ##                           PC1          PC2         PC3          PC4
    ## wheel_base        -0.30414371  0.211310013 -0.09415847  0.234487488
    ## length            -0.32775090  0.096513446 -0.10681058  0.160062864
    ## width             -0.32325931  0.094918950  0.08695568  0.033079835
    ## height            -0.13393851  0.313134277 -0.47106351  0.540152912
    ## curb_weight       -0.34666229  0.055665587  0.04615370 -0.009493307
    ## engine_size       -0.31805462 -0.006972666  0.23751543 -0.231771453
    ## bore              -0.25708194  0.002145653 -0.26026951 -0.377057383
    ## stroke            -0.05648547  0.128296076  0.71587568  0.270830147
    ## compression_ratio -0.04611922  0.583788762  0.21338515  0.015968804
    ## horsepower        -0.29809775 -0.286229246  0.14663363 -0.076284275
    ## peak_rpm           0.08373681 -0.468290240  0.12181328  0.588678102
    ## city_mpg           0.30125223  0.312866081  0.08197010 -0.042975753
    ## highway_mpg        0.30737793  0.281140948  0.08369655 -0.049875176
    ## price             -0.32216367  0.020028049  0.12611220 -0.016001166
    ##                           PC5         PC6         PC7          PC8
    ## wheel_base        -0.03522414  0.13189463 -0.46746093  0.055315054
    ## length            -0.03640047  0.11670965 -0.22423928 -0.049604988
    ## width              0.20301349  0.02764555 -0.48091176 -0.002776756
    ## height            -0.25786301 -0.15027748  0.40207143  0.205461974
    ## curb_weight        0.09406323 -0.09435765  0.15306176  0.064657121
    ## engine_size       -0.02975826 -0.14548042  0.20612602  0.301216845
    ## bore              -0.20304113  0.77067478  0.17504121  0.049371705
    ## stroke            -0.57506390  0.14908725  0.03831736 -0.046151118
    ## compression_ratio  0.47862262  0.16091965  0.35074632 -0.452837336
    ## horsepower         0.06460409 -0.02547713  0.30945895  0.183326522
    ## peak_rpm           0.39217408  0.43025959  0.10383557  0.098412258
    ## city_mpg           0.12447554  0.14454813 -0.05644298  0.473662204
    ## highway_mpg        0.06622193  0.16962917 -0.08083300  0.501087191
    ## price              0.31801810 -0.19510195  0.03076616  0.359135267
    ##                           PC9        PC10        PC11         PC12
    ## wheel_base        -0.06975630  0.59314260 -0.08859111 -0.433484255
    ## length             0.60550514  0.03915668 -0.04822413  0.613483955
    ## width             -0.07500281 -0.72774426  0.13396290 -0.218478461
    ## height            -0.07763488 -0.22856738  0.03119482 -0.083655918
    ## curb_weight        0.04870638  0.06493122  0.23615930  0.008869773
    ## engine_size        0.11077125  0.16363049  0.65077155 -0.060894832
    ## bore              -0.21990601 -0.07131892 -0.01973085  0.043235994
    ## stroke            -0.12387312 -0.07131900 -0.09732254  0.071255256
    ## compression_ratio  0.05322752  0.04849412 -0.04032946 -0.060889415
    ## horsepower         0.43909007 -0.09533899 -0.53577483 -0.418063185
    ## peak_rpm          -0.03410220  0.03923762  0.22123035  0.023375556
    ## city_mpg           0.08547226 -0.02027388  0.02673828 -0.109164932
    ## highway_mpg        0.23005158 -0.05076520 -0.07949434  0.077606348
    ## price             -0.53054099  0.08752792 -0.37028743  0.416285575
    ##                           PC13         PC14
    ## wheel_base        -0.049793497 -0.062109677
    ## length            -0.081801545  0.158102799
    ## width             -0.052306141 -0.030392402
    ## height            -0.104685453 -0.013710991
    ## curb_weight        0.870123280 -0.097948096
    ## engine_size       -0.408582823 -0.013946664
    ## bore               0.001483278  0.006601558
    ## stroke             0.049840939  0.023127007
    ## compression_ratio -0.128226116 -0.035430450
    ## horsepower        -0.050395981  0.037851602
    ## peak_rpm          -0.021217272 -0.016714806
    ## city_mpg           0.142185704  0.705904140
    ## highway_mpg        0.023241023 -0.676624791
    ## price             -0.102002892  0.024046137
    ## 
    ## $center
    ##        wheel_base            length             width            height 
    ##         98.235625        172.319375         65.596250         53.878750 
    ##       curb_weight       engine_size              bore            stroke 
    ##       2459.450000        119.093750          3.298437          3.237312 
    ## compression_ratio        horsepower          peak_rpm          city_mpg 
    ##         10.145125         95.875000       5116.250000         26.506250 
    ##       highway_mpg             price 
    ##         32.068750      11427.681250

``` r
eigenvalues <- pca_prcomp3$sdev^2
head(eigenvalues,3)
```

    ## [1] 7.771709 2.060326 1.319969

8.2) PCA plot of vehicles, and PCA plot of variables (10 pts)
-------------------------------------------------------------

``` r
#Use the first two components to graph a scatterplot of the vehicles (do not use "ggplot2" functions).
qdat <- na.omit(dat)
loadings <- pca_prcomp$rotation
```

``` r
plot(pca_prcomp$x[, 1], pca_prcomp$x[, 2], xlab = 'PC1', ylab = 'PC2', main = 'PC Plot with Vehicles')
```

![](hw01-molly-li_files/figure-markdown_github/unnamed-chunk-25-1.png)

-   PC1 and PC2 are weakly correlated.
