# 정확한 숫자 계산

double, 오차가 있다.
decimal은 없나? 계산한번 하고나면 오차가 생긴다.

결론부터 5/3을 어떻게 표현 할 것인가
1.6666666666666 ??
1.667 ??

Fraction(numerator, denominator)
Fraction(5, 3)

val d0 = Fraction(5, 3)
val d1 = Fraction(7, 5)

d0 + d1 = Fraction(46, 15)
d0 - d1 = Fraction(4, 15)
d0 / d1 = Fraction(25, 35)
d0 * d1 = Fraction(35, 15)

d0.simple() = 1.6666
d0.simple(precise) : Decimal
d0.simple(5) = 1.66667
d0.simple(5) = 1.66667
d0.double() = e*??

## DB 저장
jpa같은거 쓸경우

numerator = 5
denominator = 3
simple = 1.6667

