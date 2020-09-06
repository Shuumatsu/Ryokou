注意到全加器接受三个输入并产生两个输出，可看作一个3: 2 compressor。Wallace 基于这个性质对乘法运算进行优化。

```
                           a1   a2   a3   a4   a5   a6
X                          b1   b2   b3   b4   b5   b6
------------------------------------------------------
                         a1b6 a2b6 a3b6 a4b6 a5b6 a6b6
                    a1b5 a2b5 a3b5 a4b5 a5b5 a6b5
               a1b4 a2b4 a3b4 a4b4 a5b4 a6b4
          a1b3 a2b3 a3b3 a4b3 a5b3 a6b3
     a1b2 a2b2 a3b2 a4b2 a5b2 a6b2
a1b1 a2b1 a3b1 a4b1 a5b1 a6b1
```

每一列的计算依赖前一列产生的进位，采用类似 Carry Save Adder 的想法，先直接进行计算，待产生进位数据后再加上进位

每三行看作一组，用全加器得到本位和以及进位，将进位数据左移一位

```
                           a1   a2   a3   a4   a5   a6
X                          b1   b2   b3   b4   b5   b6
------------------------------------------------------
                        (a1b6 a2b6 a3b6 a4b6 a5b6 a6b6    =>     
                    a1b5 a2b5 a3b5 a4b5 a5b5 a6b5
               a1b4 a2b4 a3b4 a4b4 a5b4 a6b4)
         (a1b3 a2b3 a3b3 a4b3 a5b3 a6b3
     a1b2 a2b2 a3b2 a4b2 a5b2 a6b2
a1b1 a2b1 a3b1 a4b1 a5b1 a6b1)
```