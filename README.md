# 程序填空十一练

题目背景：HX是一只建兰-->杭二中的巨魔小猴。

## 小猴传球

难度：◇

n（2≤n≤1000）只HX，编号0~n-1，从小到大逆时针围成一圈坐，0号HX顺时针一位为n-1号HX。开始时，0号HX有2个球。每一轮，每个球都有2/3概率被逆时针传递给相邻HX，1/3概率被顺时针传递给相邻HX。求m（0≤m≤1000）轮后p号HX拿球数的期望。

提示：假设知道k-1轮中每只HX拿球数的期望，则第k轮的期望应该这样算……

```vbscript
Private Sub Monkey_Click()
    Dim n As Long, m As Long, p As Long, f(0 To 2000) As Double
    ...'省略读入n,m,p的代码
    ____1____
    For i = 1 To m
        For j = 0 To n - 1
            ____2____
        Next
        For j = 0 To n - 1
            f(j + n) = f(j)
        Next
    Next
    Text1.text=Str(____3____)
End Sub
```

## 小猴排序

难度：◆

HX藐视时间复杂度为O(n^2)的冒泡排序，他想掌握一种O(nlogn)的归并排序。归并排序有如下思想：

1.只含一个数的序列是有序的。

2.对于含两个及以上数的序列，将其一分为二分别排序，然后合并两个有序序列。

读入数字总数n，序列a()并将其升序排序输出至Text1。

```vbscript
Dim a(1 To 1000000) As Long, b(1 To 1000000) As Long, n As Long
Private Sub Monkey_Click()
    ...'省略读入n,a()的代码
    Monkey_King 1, n
    Text2.Text = ""
    For i = 1 To n
        Text1.Text = Str(a(i)) + Text1.Text
    Next
End Sub
Private Sub Monkey_King(l As Long, r As Long)
    If ____1____ Then Exit Sub
    Dim m As Long, t As Long, i As Long, j As Long, k As Long
    m = (l + r) \ 2: Monkey_King l, m: Monkey_King m + 1, r
    Do While ____2____
        If ____3____ Then
            b(k) = a(i): i = i + 1
        Else
            b(k) = a(j): j = j + 1
        End If
        k = k + 1
    Loop
    Do While i <= m
        b(k) = a(i): i = i + 1: k = k + 1
    Loop
    Do While j <= r
        b(k) = a(j): j = j + 1: k = k + 1
    Loop
    For i = l To r
        ____4____
    Next
End Sub
```

## 小猴排队

难度：◆◇

n只HX排成一排，第i只HX身高a(i)。对于i<j且a(i)>a(j)这样挡住后方视线的情况，HX们都不愿看到，他们想知道目前存在多少对i，j满足该情况。

虽然HX知道该答案等于冒泡排序使a()升序的交换次数，但HX藐视时间复杂度为O(n^2)的冒泡排序，他想通过一种O(nlogn)的归并排序算出答案。

提示：先做“小猴排序”。

```vbscript
Dim a(1 To 1000000) As Long, b(1 To 1000000) As Long, n As Long, ans As Long
Private Sub Monkey_Click()
    ...'省略读入n,a()的代码
    Monkey_King 1, n
    Text1.Text = Str(ans)
End Sub
Private Sub Monkey_King(l As Long, r As Long)
    If l >= r Then Exit Sub
    Dim m As Long, t As Long, i As Long, j As Long, k As Long
    m = (l + r) \ 2
    ____1____
    Do While i <= m And j <= r
        If a(i) ____2____ a(j) Then
            b(k) = a(i): i = i + 1
        Else
            b(k) = a(j)
            ____3____
        End If
        k = k + 1
    Loop
    Do While i <= m
        b(k) = a(i): i = i + 1: k = k + 1
    Loop
    Do While j <= r
        ____4____
    Loop
    For i = l To r
        a(i) = b(i)
    Next
End Sub
```

## 小猴的长度

难度：◆◇

Unreal 5引擎发布了，HX迫不及待地用它给自己建了个模。但他的建模水平很可惜，只能建由n个点n-1条边构成的火柴人HX，每条边有其边长，如下图：

![小猴的长度](https://s1.ax1x.com/2020/07/17/U6SZRI.png)

任意两个点互相连通，两点间的路径也唯一，两点间的距离为该路径上各边的边长和。求距离两点间距离的最大值。

提示：距离点a最远的点是u，距离点u最远的点是v，可以证明u，v即是距离最远的两个点。

```vbscript
Dim a(1 To 1000000) As Long, ans As Long, u As Long, n As Long
'a(n*(i-1),j)表示i点与j点间边的长度，a(k)≥0，为0则i点与j点间无边
Private Sub Monkey_Click()
    ...'省略读入n,a()的代码
    Monkey_King 1: ____1____
    Text1.Text = Str(ans)
End Sub
Private Sub Monkey_King(start As Long)
    Dim d(1 To 1000000) As Long, b(1 To 1000000) As Long, l As Long, r As Long
    For i = 1 To n
        d(i) = -1
    Next
    d(start) = 0: l = 0: r = 1: b(0) = start: ans = 0
    Do While ____2____
        p = b(l)
        For i = 1 To n
            If ____3____ Then
                d(i) = d(p) + a(n * (p - 1) + i): b(r) = i: r = r + 1
            End If
        Next
        ____4____
    Loop
    For i = 1 To n
        If d(i) > ans Then
            ans = d(i): ____5____
        End If
    Next
End Sub
```

## 小猴喝奶

难度：◆◆

别看HX长这么大，其实他还在喝奶。HX每次需要精准的a升奶，喝多了被奶穿，喝少了会哭。HX有2个杯子，A杯为n升，B杯为m升。每次操作，HX可以将某个杯子倒空，或将某个杯子倒满，或将一个杯子中的奶倒到另一个杯子中直到另一个杯子满了或该杯子空了。初始时HX有两个空杯子，求他能否得到a升奶，若能则输出最少操作数。

提示：若已知使得A杯装i升，B杯装j升的最少操作数，则再经过一次操作可以得到……

```vbscript
Dim f(0 To 1100000) As Long, a As Long, n As Long, m As Long, x(0 To 1100000) As Long, y(0 To 1100000) As Long, l As Long, r As Long, xx As Long, yy As Long
'f((m + 1) * i + j)表示使A杯装i升，B杯装j升的最少操作数
Private Sub Monkey_Click()
    ...'省略读入a,n,m的代码
    For i = 0 To (n + 1) * (m + 1) - 1
        f(i) = -1
    Next
    ____1____:r = 1
    Do While l < r
        If x(l) = a Or y(l) = a Then
            Text1.Text = "HX can get his milk within" + Str(f((m + 1) * x(l) + y(l))) + " steps."
            Exit Sub
        End If
        For i = 1 To 6
            doit i, x(l), y(l)
            If ____2____ Then
                x(r) = xx: y(r) = yy: r = r + 1: f((m + 1) * xx + yy) = f((m + 1) * x(l) + y(l)) + 1
            End If
        Next
        ____3____
    Loop
    Text1.Text = "HX,GG."
End Sub
Private Sub doit(t As Long, x As Long, y As Long) '进行操作，得到新的杯子状态并存至xx，yy
    If t = 1 Then xx = 0: yy = 0
    If t = 2 Then xx = x: yy = 0
    If t = 3 Then xx = n: yy = y
    If t = 4 Then xx = x: yy = m
    If t = 5 Then xx = max(____4____): yy = min(____5____)
    If t = 6 Then xx = min(____6____): yy = max(0, x + y - n)
End Sub
Private Function max(a As Long, b As Long) As Long
    max = a
    If a < b Then max = b
End Function
Private Function min(a As Long, b As Long) As Long
    min = a
    If a > b Then min = b
End Function
```

## 小猴拿石子

难度：◆◆

有2堆石子，X堆有n块，Y堆有m块。有2只HX轮流拿石子，每只HX每次能从X堆拿a(i)块，或从Y堆拿b(j)块（i≤aa，j≤bb，a(i)>0，b(j)>0）。若不能继续拿（没有石子或者剩余石子数目和允许的拿走数目都不相等）则输。输入n,m,aa,bb,a(),b()，假设HX非常聪明，判断先手必胜/必输。

提示：假如已知X堆剩i块，Y堆剩j块时先手必输，可以从X堆中拿z块，则X堆剩i+z块，Y堆剩j块的先手必……

```vbscript
Private Sub Monkey_Click()
    ...'省略读入n,m,aa,bb,a(),b()的代码
    Dim f(0 To 1100000) As Boolean 'f((m+1)*i+j)表示X和Y堆分别剩下i和j块石子时，先手是否必胜
    For i = 0 To n
        For j = 0 To m
            If ____1____ Then
                For k = 1 To aa
                    If i + a(k) <= n Then f((m + 1) * (i + a(k)) + j) = True
                Next
                For k = 1 To bb
                    If j + b(k) <= m Then ____2____
                Next
            End If
        Next
    Next
    Text1.Text = "先手必胜"
    If ____3____ Then Text1.Text = "先手必输"
End Sub
```

## 小猴悬挂

难度：◆◆

光滑水平桌面上有n个小洞，第i个洞的坐标为(a(i),b(i))，-1000≤a(i)≤1000，-1000≤b(i)≤1000，每个小洞穿有一根轻绳，下端系有质量为m(i)的HX，上端在桌上与其他轻绳有一个共同打结处，轻绳足够长。求打结处的平衡坐标，精度0.01。

提示：先将打结处随意放在一处，让其向受力方向移动一段距离，重复这个过程并使每次移动的距离变为上一次的0.97倍，就可以……

```vbscript
Private Sub Monkey_Click()
    Dim a(1 To 1000) As Double, b(1 To 1000) As Double, m(1 To 1000) As Double, x As Double, y As Double, d As Double, xf As Double, yf As Double, dx As Double, dy As Double, xy As Double
    ...'省略读入n,a(),b(),m()的代码
    d = ____1____ '考虑程序正确性和运行效率，选填A.30 B.300，理由：____2____
    Do While d > 0.001
        For i = 1 To n
            dx = a(i) - x: dy = b(i) - y: xy = sqrt(dx ^ 2 + dy ^ 2)
            ____3____
        Next
        xy = sqrt(xf ^ 2 + yf ^ 2): x = x + d * xf / xy: y = y + d * yf / xy
        d=d*0.97: ____4____
    Loop
    Text1.Text = Str(x) + Str(y)
End Sub
```

## 小猴和无限迷宫

难度：◆◆

HX被困在一无限迷宫中，无限迷宫由无数个**相同**的长n宽m的长方形区块上下左右相邻拼接而成（也就是说，如果HX在某个区块的第1列第k行，并向左走，则他会走到该区块左侧的区块的第n列第k行；如果HX在某个区块的第k列第m行，并向下走，则他会走到该区块下方的区块的第k列第1行。以此类推）。每个区块中1*1的方格是路或者墙。每个区块坐标为(a,b)的方格上有逃离传送门；HX可以选择出生在任意区块坐标为(c,d)的方格上，保证该方格为路。注意，坐标的表示格式为（长，宽）。HX可以向上下左右移动，求HX能否逃离，若能则输出最小移动格数。

提示：若已知到达(i,j)的最小移动格数，则再走一格可以到达……

```vbscript
Dim dx(1 To 4) As Long, dy(1 To 4) As Long, f(0 To 1000010) As Long, x(0 To 1000010) As Long, y(0 To 1000010) As Long, l As Long, r As Long, a As Long, b As Long, c As Long, d As Long, n As Long, m As Long, map(0 To 1000010) As Boolean
'f(m * (i - 1) + j)表示到达每个区块坐标(i,j)的方格的最小移动格数，map(m * (i - 1) + j)表示每个区块坐标(i,j)的方格是否为路
Private Sub Monkey_Click()
    ...'省略读入map,a,b,c,d,n,m的代码
    dx(1) = 0: dx(2) = 0: dx(3) = 1: dx(4) = -1: dy(1) = 1: dy(2) = -1: dy(3) = 0: dy(4) = 0
    For i = 1 To n * m
        f(i) = -1
    Next
    f(m * (c - 1) + d) = 0: l = 0: r = 1: x(0) = c: y(0) = d
    Do While ____1____
        xxx = x(l): yyy = y(l): l = l + 1
        For i = 1 To 4
            ____2____
            If map(m * (xx - 1) + yy) And f(m * (xx - 1) + yy) = -1 Then
                ____3____
                f(m * (xx - 1) + yy) = f(m * (xxx - 1) + yyy) + 1
            End If
        Next
    Loop
    Text1.Text = "HX can escape within" + Str(f(m * (a - 1) + b)) + " steps."
    If ____4____ Then Text1.Text = "HX,GG."
End Sub
```

## 小猴买游戏

难度：◆◆

Steam夏促了！HX有1000元钱，他的愿望单里有200款游戏，第i款价格a(i)，每款游戏只能买一次。求HX最多能花费多少钱，并求该情况下它买了哪些游戏，并按游戏编号升序输出。保证使花费最大的方案唯一。

提示：假如已知能在前i-1款游戏中花费j元，第i款游戏价格为k，且j+k≤1000，那么就能在前i款游戏中花费……

```vbscript
Private Sub Monkey_Click()
    Dim f(0 To 1000) As Boolean, game(0 To 1000) As Long, a(1 To 200) As Long, max As Long
    ...'省略读入a()的代码
    ____1____
    For i = 1 To 200
        For j = ____2____
            If f(j - a(i)) Then
                f(j) = True:____3____
                If j > max Then max = j
            End If
        Next
    Next
    Text1.Text = Str(max): i = max: s = ""
    Do While i > 0
        s = Str(b(i)) + s
        ____4____
    Loop
    Text1.Text = Text1.Text + s
End Sub
```

## 小猴的二叉树

难度：◆◆◇

HX有棵二叉树，满足如下性质：对于任一结点（编号为P），其左子树（如存在）中的最大结点编号为U，则U<P；右子树（如存在）中的最小结点编号为V，则P<V。

以下图为例对二叉树进行遍历：先序遍历（先父结点，再左子树，再右子树）为6,3,1,2,5,4,9,7,8,10；中序遍历（先左子树，再父结点，再右子树）为1,2,3,4,5,6,7,8,9,10；后序遍历（先左子树，再右子树，再父结点）为2,1,4,5,3,8,7,10,9,6。

很显然，一对正确的先、中序遍历能唯一确定一棵二叉树。以下图的先、中序为例：先序遍历开头（6）即为父结点，则中序遍历中父结点左侧（1,2,3,4,5）为左子树，右侧（7,8,9,10）为右子树，而左右子树又可以各通过同样的方法再分为左子树、父结点、右子树；以左子树为例，其先序遍历（3,1,2,5,4）开头（3）为父结点，中序遍历中父结点左侧（1,2）为左子树，右侧（4,5）为右子树……

![小猴的二叉树](https://s1.ax1x.com/2020/07/16/UrYmeU.png)

给出HX的二叉树的先、中序遍历，求其后序遍历。

提示：HX的二叉树的中序遍历具有的特征是……

```vbscript
Dim ans(1 To 100010) As Long, anscnt As Long, a(1 To 100010) As Long, b(1 To 100010) As Long, n As Long
Private Sub Monkey_Click()
    ...'省略读入n,a(),b()的代码,a()记录先序,b()记录中序
    Monkey_King 1, n, 1, n
    For i = 1 To n
        List1.AddItem Str(ans(i))
    Next
End Sub
Private Sub Monkey_King(al As Long, ar As Long, bl As Long, br As Long)
    If al > ar Then Exit Sub
    ____1____: father_pos = find(father): t = father_pos
    Monkey_King al + 1, al + t - bl, bl, t - 1
    Monkey_King ____2____
    ____3____
End Sub
Private Function find(x As Long) As Long
    l = 1: r = n
    Do While True
        m = (l + r) \ 2
        If b(m) = x Then
            find = m: Exit Function
        End If
        If ____4____ Then
            l = m + 1
        Else
            r = m - 1
        End If
    Loop
End Function
```

## 小猴配平方程式

难度：◆◆◆

HX觉得化学太难了，他要写个程序配平化学方程式并约分系数。为降低难度，保证：物质都用化学式表示，如Cu(NO3)2写为CuN2O6；存在唯一配法；约分后各项系数均为2^3×3^3×5^2×7^2的因数；程序运行时不会出现除数为0的情况。

输入：一个字符串，格式类似这样，结尾有一空格（但此例会出现除数为0的情况，因此仅作为格式示范）

```
Cu+HNO3=CuN2O6+NO+H2O
```

输出：若干系数，用空格隔开，格式类似这样

```
3 8 3 2 4
```

提示一：对正实数x四舍五入：Int(x+0.5)

提示二：n（元素种数）与m（物质种数）是有关系的……

提示三：a(i)表示第i种元素；b(n*(i-1)+j)表示第i种物质中j元素的原子个数，若i为生成物则b()取负。

```vbscript
Private Sub Monkey_Click()
    Dim a(1 To 200) As String, n As Long, s As String, b(1 To 40000) As Double, ch As Char, ss As String, m As Long, f As Long, cnt As Long, num As Long, t As Double, sum As Double, ans(1 To 200) As Long, gcd As Long
    s = Text1.Text '统计元素和种数
    For i = 1 To Len(s)
        ch = Mid(s, i, 1)
        If "a" <= ch And ch <= "z" Then
            ss = ss + ch
        Else
            If check(ss) Then
                n = n + 1: a(n) = ss
            End If
            ss = ch
            If ____1____ Then ss = ""
        End If
    Next
    ____2____
    For i = 1 To Len(s) '统计每种物质
        ch = Mid(s, i, 1)
        If "a" <= ch And ch <= "z" Then
            ss = ss + ch
        ElseIf "0" <= ch And ch <= "9" Then
            cnt = cnt * 10 + Val(ch)
        Else
            num = search(ss)
            If cnt = 0 Then cnt = 1
            ____3____
            ss = ""
            If "A" <= ch And ch <= "Z" Then ss = ch
            If ch = "=" Then ____4____
            If ch = "+" Then m = m + 1
            cnt = 0
        End If
    Next
    For i = 1 To n - 1 '高斯消元解多元一次方程组
        For j = i + 1 To n
            t = b(n * (i - 1) + j) / b(n * (i - 1) + i)
            For k = i To m
                b(n * (k - 1) + j) = b(n * (k - 1) + j) - t * b(n * (k - 1) + i)
            Next
        Next
    Next
    ans(m)=____5____
    For i = n To 1 Step -1
        sum = 0
        For j = i + 1 To m
            sum = sum + b(n * (j - 1) + i) * ans(j)
        Next
        ans(i)=____6____
    Next
    gcd = ans(1)
    For i = 2 To m
        gcd = ggcd(gcd, ans(i))
    Next
    Text2.Text = ""
    For i = 1 To m
        Text2.Text = Text2.Text + ____7____
    Next
End Sub
Private Function check(s As String) '判断是否是新元素
    check = True
    If s = "" Then check = False
    For i = 1 To n
        If Not check Then Exit For
        If a(i) = s Then check = False
    Next
End Function
Private Function search(s As String) '查找元素
    For i = 1 To n
        If a(i) = s Then search = i: Exit For
    Next
End Function
Private Function ggcd(a As Long, b As Long) '求a,b的最大公约数
    Dim t As Long
    If (b > a) Then t = b: b = a: a = t
    If b = 0 Then ggcd = a: Exit Function
    ggcd = ggcd(b, a Mod b)
End Function
```

---

# 程序填空十一练答案

## 1.小猴传球

```vbscript
1. f(n)=2
2. f(j)=f((j+n-1)Mod n + n)2/3+f((j+1)Mod n + n)/3
3. f(p+n)
```

## 2.小猴排序

```vbscript
1. l>=r
2. i<=m And j<=r
3. a(i)>a(j)
4. a(i)=b(i)
```

## 3.小猴排队

```vbscript
1. Monkey_King l,m:Monkey_King m+1,r
2. <=
3. j=j+1:ans=ans+m-i+1
4. b(k)=a(j):j=j+1:k=k+1
```

## 4.小猴的长度

```vbscript
1. Monkey_King u
2. l<r
3. d(i)=-1 And a(n*(p-1)+i)>0
4. l=l+1
5. u=i
```

## 5.小猴喝奶

```vbscript
1. f(0)=0
2. f((m+1)*xx+yy)=-1
3. l=l+1
4. 0,x+y-m
5. m,x+y
6. n,x+y
```

## 6.小猴拿石子

```vbscript
1. Not f((m+1)*i+j)
2. f((m+1)*i+j+b(k))=True
3. Not f((m+1)*n+m)
```

## 7.小猴悬挂

```vbscript
1. B
2. A选项首项30公比0.97的等差数列求和小于1000√2
3. xf=xf+m(i)*dx/xy:yf=yf+m(i)*dy/xy
4. xf=0:yf=0
```

## 8.小猴和无限迷宫

```vbscript
1. f(m*(a-1)+b)=-1 And l<r
2. xx=(xxx+dx(i)+n-1) Mod n + 1:yy=(yyy+dy(i)+m-1) Mod m + 1
3. x(r)=xx:y(r)=yy:r=r+1
4. f(m*(a-1)+b)=-1
```

## 9.小猴买游戏

```vbscript
1. f(0)=True
2. 1000 To a(i) Step -1
3. b(j)=i
4. i=i-a(b(i))
```

## 10.小猴的二叉树

```vbscript
1. father=a(al)
2. al+t-bl+1,ar,t+1,br
3. anscnt=anscnt+1:ans(anscnt)=father
4. x>b(m)
```

## 11.小猴配平方程式

```vbscript
1. ch<"A" Or "Z"<ch
2. m=1:f=1
3. b(n*(m-1)+num)=cnt*f
4. f=-1:m=m+1
5. 2^3*3^3*5^2*7^2
6. Int(-sum/b(n*(i-1)+i)+0.5)
7. Str(ans(i)\gcd)
```
