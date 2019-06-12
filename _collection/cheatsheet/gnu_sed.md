# sed

## 라인 지우기

regex를 잘 써야되는데

일반적인 regex와 다른 경우가 많다.

ex) 2018년도가 포함된 라인을 지우는 경우
```
^.+2018-.+$
^.*2018-.*$

sed -i '/^.*2018-.*$/ d' filename.ext
```


## 문자열 교체

구분자는 적당히 골라서 쓰면된다.
http://를 변경해야하는 경우라면 /보다는 @, # 를 쓰는게 낫겠지

```
sed -i 's/find pattern/to replace/g' filename.ext
sed -i 's@find pattern@to replace@g' filename.ext
sed -i 's#find pattern#to replace#g' filename.ext
```