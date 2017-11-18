# flang - a functional language
# - First 11 euler problems ( https://projecteuler.net/archives ) solved in flang language to show its features
# - flang is a totally functional language. Functions are flang's first class citizens. 
# - It uses postfix instead of infix since I find it easier to understand and write.
# - Features json (very mature) regex (very early alpha)
# - flang itself is written completely in C-language since I prefer totally functional languages.
# - You can use flang as a calculator: ./flang x:'15 7 1 1 + - / 3 * 2 1 1 + + - !'
# language: flang
# version: 0.7
# author: mystikkogames
# email: mystikkogames@protonmail.com

( function :euler_1 ( ) :
    ( $sum 0 = )
    ( $i 1 = )
    ( loop ( $i 1000 < ) :
        ( if ( ( $i 5 % 0 == $i 3 % 0 == or ) :  
            ( $sum $sum $i + = ) )
        )
        ( $i 1 $i + = )
    )
    ( "euler#1: " $sum *join ! )
)

( function :euler_2 ( ) : 
	( $sum 0 = )
	( $a 0 = )
	( $b 1 = )
	( $c 0 = )
	( loop ( $c 4000000 < ) : 
		( $c $a $b + = )	
		( $a $b = )
		( $b $c = )
		( if ( ( $c 2 % 0 == ) : 
            ( $sum $c $sum + = ) )
        )
	)
	( "euler#2: " $sum *join ! )
)

( function :euler_3 ( ) :   
	( $bignum 600851475143 = )
    ( $n 2 = )
    ( $biggest_factor 0 = )
	( loop ( $n $bignum 1 + < ) :
		( if ( ( $n *is_prime $bignum $n % 0 == and ) :
		    ( $bignum $bignum $n / = )
		    ( $biggest_factor $biggest_factor $n *max = )
        ) )
		( $n 1 $n + = )
    )
	( "euler#3: " $biggest_factor *join ! )
)

( function :euler_4 ( ) :   
	( $start1 999 = )
	( $largest 0 = )
    ( loop ( $start1 100 > ) :
		( $start2 999 = )
        ( loop ( $start2 100 > ) :
            ( $res $start2 $start1 * = )
            ( if ( ( $res $largest < ) : ( break_loop ) ) )            
            ( if ( ( $res 0 *char_at $res 5 *char_at == 
                $res 1 *char_at $res 4 *char_at == and 
                $res 2 *char_at $res 3 *char_at == and ) :
                ( $largest $res $largest *max = ) ) )
            ( $start2 $start2 1 - = )
        )
        ( $start1 $start1 1 - = )    
    )
    ( "euler#4: " $largest *join ! )
)

( function :euler_5 ( ) :   
	( $n 0 = )
    # because non-primes are multiples of primes etc: 18=2*3*3 ... 20=2*2*5 ...
    ( $step 2 3 5 7 11 13 17 * * * * * * = ) 
    ( loop ( 1 ) :
        ( $n $step $n + = )
        ( $rmdrs 0 = )
        ( $i 2 = )
        ( loop ( $i 22 < ) :
            ( if ( ( $n $i % 0 != ) : 
                ( $rmdrs 1 = )
                ( break_loop )
            ))
            ( $i $i 1 + = )
        )
        ( if ( ( $rmdrs 0 == ) : ( "euler#5: " $n *join ! ) ( return ) ))
    )
)

# brute force saves the day!
( function :euler_6 ( ) :   
	( $sum_of_squares 0 = )
	( $squares_of_sum 0 = )
    ( $i 1 = )
    ( loop ( $i 101 < ) :
	    ( $sum_of_squares $i $i * $sum_of_squares + = )
	    ( $squares_of_sum $i $squares_of_sum + = )
        ( $i $i 1 + = )
    )
    ( $squares_of_sum $squares_of_sum $squares_of_sum * =  )
    ( "euler#6: " $squares_of_sum $sum_of_squares - *join ! )
)


( function :euler_7 ( ) :   
	( "euler#7: " 10000 *prime_nth *join ! ) # shame on me...
)

( function :euler_8 ( ) :   
	( $str  "73167176531330624919225119674426574742355349194934"
            "96983520312774506326239578318016984801869478851843"
            "85861560789112949495459501737958331952853208805511"
            "12540698747158523863050715693290963295227443043557"
            "66896648950445244523161731856403098711121722383113"
            "62229893423380308135336276614282806444486645238749"
            "30358907296290491560440772390713810515859307960866"
            "70172427121883998797908792274921901699720888093776"
            "65727333001053367881220235421809751254540594752243"
            "52584907711670556013604839586446706324415722155397"
            "53697817977846174064955149290862569321978468622482"
            "83972241375657056057490261407972968652414535100474"
            "82166370484403199890008895243450658541227588666881"
            "16427171479924442928230863465674813919123162824586"
            "17866458359124566529476545682848912883142607690042"
            "24219022671055626321111109370544217506941658960408"
            "07198403850962455444362981230987879927244284909188"
            "84580156166097919133875499200524063689912560717606"
            "05886116467109405077541002256983155200055935729725"
            "71636269561882670428252483600823257530420752963450"
            *join *join *join *join *join *join *join 
            *join *join *join *join *join *join *join *join *join 
            *join *join *join = )
    ( $len $str *length = )
    ( $i 0 = )
    ( $maximum 0 = )
    ( loop ( $i 13 + $len < ) :
        ( $j 1 = )
        ( $product $str $i *char_at = )
        ( loop ( $j 13 < ) :
            ( $product $str $i $j + *char_at $product * = )
            ( $j 1 $j + = )
        )
        ( $maximum $product $maximum *max = )
        ( $i $i 1 + = )
    )
	( "euler#8: " $maximum *join ! )
)

( function :euler_9 ( ) :   
    ( $a 1 = )
    ( loop ( $a 1000 < ) :
        ( $b $a 1 + = )
        ( loop ( $b 1000 < ) :
                ( $c $b 1 + = )
                ( $sum1 $a $a * $b $b * + = )
                ( $sum2 1000 $a $b + - *pow2 = )
                ( if ( ( $sum2 $sum1 > $sum1 $sum2 == and ) : 
                        ( "euler#9: " 1000 $a $b + - $a $b * * *join ! )
                        ( return )
        
                ) )      
            ( $b $b 1 + = )
        )
        ( $a $a 1 + = )
    )
)

# in brute force we trust!
( function :euler_10 ( ) :   
    ( $i 0 = )
    ( $sum 0 = )
    ( $prime 0 = )
    ( loop ( $prime 2000000 < ) :
        ( $sum $prime $sum + = )
        ( $prime $i *prime_nth = ) 
        ( $i $i 1 + = )
    )
    ( "euler#10: " $sum *join ! )
)

( function :euler_11 ( ) :   
    (
    $str
    "08 02 22 97 38 15 00 40 00 75 04 05 07 78 52 12 50 77 91 08"
    "49 49 99 40 17 81 18 57 60 87 17 40 98 43 69 48 04 56 62 00"
    "81 49 31 73 55 79 14 29 93 71 40 67 53 88 30 03 49 13 36 65"
    "52 70 95 23 04 60 11 42 69 24 68 56 01 32 56 71 37 02 36 91"
    "22 31 16 71 51 67 63 89 41 92 36 54 22 40 40 28 66 33 13 80"
    "24 47 32 60 99 03 45 02 44 75 33 53 78 36 84 20 35 17 12 50"
    "32 98 81 28 64 23 67 10 26 38 40 67 59 54 70 66 18 38 64 70"
    "67 26 20 68 02 62 12 20 95 63 94 39 63 08 40 91 66 49 94 21"
    "24 55 58 05 66 73 99 26 97 17 78 78 96 83 14 88 34 89 63 72"
    "21 36 23 09 75 00 76 44 20 45 35 14 00 61 33 97 34 31 33 95"
    "78 17 53 28 22 75 31 67 15 94 03 80 04 62 16 14 09 53 56 92"
    "16 39 05 42 96 35 31 47 55 58 88 24 00 17 54 24 36 29 85 57"
    "86 56 00 48 35 71 89 07 05 44 44 37 44 60 21 58 51 54 17 58"
    "19 80 81 68 05 94 47 69 28 73 92 13 86 52 17 77 04 89 55 40"
    "04 52 08 83 97 35 99 16 07 97 57 32 16 26 26 79 33 27 98 66"
    "88 36 68 87 57 62 20 72 03 46 33 67 46 55 12 32 63 93 53 69"
    "04 42 16 73 38 25 39 11 24 94 72 18 08 46 29 32 40 62 76 36"
    "20 69 36 41 72 30 23 88 34 62 99 69 82 67 59 85 74 04 36 16"
    "20 73 35 29 78 31 90 01 74 31 49 71 48 86 81 16 23 57 05 54"
    "01 70 54 71 83 51 54 69 16 92 33 48 61 43 52 01 89 19 67 48"
    *join *join *join *join *join *join *join *join *join *join
    *join *join *join *join *join *join *join *join *join *remove_whitespace = 
    )  
    ( $x 0 = )
    ( $maximum 0 = )
    ( loop ( $x 16 < ) :
        ( $y 0 = )  
        ( loop ( $y 16 < ) :
            ( $pnt $x 2 * $y 40 * + = )
            ( $product_x
                $str $pnt *char_at $str $pnt 1 + *char_at *join
                $str $pnt 2 + *char_at $str $pnt 3 + *char_at *join
                $str $pnt 4 + *char_at $str $pnt 5 + *char_at *join
                $str $pnt 6 + *char_at $str $pnt 7 + *char_at *join
                * * * = 
            )
            ( $product_y 
                $str $pnt *char_at $str $pnt 1 + *char_at *join
                $str $pnt 40 + *char_at $str $pnt 41 + *char_at *join
                $str $pnt 80 + *char_at $str $pnt 81 + *char_at *join
                $str $pnt 120 + *char_at $str $pnt 121 + *char_at *join
                * * * = 
            )
            ( $product_diagonal 
                $str $pnt *char_at $str $pnt 1 + *char_at *join
                $str $pnt 42 + *char_at $str $pnt 43 + *char_at *join
                $str $pnt 84 + *char_at $str $pnt 85 + *char_at *join
                $str $pnt 126 + *char_at $str $pnt 127 + *char_at *join
                * * * = 
            )
            ( $maximum $product_x $maximum *max = )
            ( $maximum $product_y $maximum *max = )
            ( $maximum $product_diagonal $maximum *max = )
            ( $y $y 1 + = ) 
        )
        ( $x $x 1 + = )
    )
    # this fucker goes the other way so I have a special case for it
    ( $x 4 = )
    ( loop ( $x 20 < ) :
        ( $y 0 = )  
        ( loop ( $y 16 < ) :
            ( $pnt $x 2 * $y 40 * + = )
            ( $product_diagonal 
                # a little bit of mental gymnaustic and your mind transforms 2D easily to 1D
                $str $pnt *char_at $str $pnt 1 + *char_at *join
                $str $pnt 38 + *char_at $str $pnt 39 + *char_at *join
                $str $pnt 76 + *char_at $str $pnt 77 + *char_at *join
                $str $pnt 114 + *char_at $str $pnt 115 + *char_at *join
                * * * = 
            )   
            ( $maximum $product_diagonal $maximum *max = )
            ( $y $y 1 + = ) 
        )
        ( $x $x 1 + = )
    )
    ( "euler#11: " $maximum *join ! )
)

# I'll do more if I find time...

# results on my computer
# euler#1: 233168
# euler#2: 4613732
# euler#3: 6857
# euler#4: 906609
# euler#5: 232792560
# euler#6: 25164150
# euler#7: 104743
# euler#8: 23514624000
# euler#9: 31875000
# euler#10: 142913828922
# euler#11: 70600674
( function :main ( ) :
    ( :euler_1 ) # 233168
    ( :euler_2 ) # 4613732
    ( :euler_3 ) # 6857
    ( :euler_4 ) # 906609
    ( :euler_5 ) # 232792560
    ( :euler_6 ) # 25164150
    ( :euler_7 ) # 104743
    ( :euler_8 ) # 23514624000
    ( :euler_9 ) # 31875000
    ( :euler_10 ) # 142913828922
    ( :euler_11 ) # 70600674
)

