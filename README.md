# 程序填空三练

## 小猴喝奶

难度：◆◆◇

别看HX长这么大，其实他还在喝奶。HX每次需要精准的a升奶，喝多了被奶穿，喝少了会哭。HX有2个杯子，A杯为n升，B杯为m升。每次操作，HX可以将某个杯子倒空，或将某个杯子倒满，或将一个杯子中的奶倒到另一个杯子中直到另一个杯子满了或该杯子空了。初始时HX有两个空杯子，求他能否得到a升奶，若能则输出最少操作数。

```vbscript
Dim f(0 To 1100000) As Long, a As Long, n As Long, m As Long, x(0 To 1100000) As Long, y(0 To 1100000) As Long, l As Long, r As Long, xx As Long, yy As Long
'f((m + 1) * i + j)表示使A杯装i升，B杯装j升的最小次数
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
Private Sub doit(t As Long, x As Long, y As Long)
    If t = 1 Then xx = 0: yy = 0
    If t = 2 Then xx = x: yy = 0
    If t = 3 Then xx = n: yy = y
    If t = 4 Then xx = x: yy = m
    If t = 5 Then xx = max(____4____): yy = min(____5____)
    If t = 6 Then xx = min(____6____): yy = max(0, x + y - n)
End Sub
Private Function max(a As Long, b As Long) As Long
    max = a
    If (a < b) Then max = b
End Function
Private Function min(a As Long, b As Long) As Long
    min = a
    If (a > b) Then min = b
End Function
```

## 小猴和无限迷宫

难度：◆◆◇

HX被困在一无限迷宫中，无限迷宫由无数个**相同**的长n宽m的长方形区块上下左右相邻拼接而成（也就是说，如果HX在某个区块的第1列第k行，并向左走，则他会走到该区块左侧的区块的第n列第k行；如果HX在某个区块的第k列第m行，并向下走，则他会走到该区块下方的区块的第k列第1行。以此类推）。每个区块中1*1的方格是路或者墙。每个区块坐标为(a,b)的方格上有逃离传送门；HX可以选择出生在任意区块坐标为(c,d)的方格上，保证该方格为路。注意，坐标的表示格式为（长，宽）。HX可以向上下左右移动，求HX能否逃离，若能则输出最小移动格数。

```vbscript
Dim dx(1 To 4) As Long, dy(1 To 4) As Long, f(0 To 1000010) As Long, x(0 To 1000010) As Long, y(0 To 1000010) As Long, l As Long, r As Long, a As Long, b As Long, c As Long, d As Long, n As Long, m As Long, map(0 To 1000010) As Boolean
'f (m * (i - 1) + j)表示到达每个区块坐标(i,j)的方格的最小格数，map (m * (i - 1) + j)表示每个区块坐标(i,j)的方格是否为路
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

## 小猴的二叉树

难度：◆◆◆

HX有棵二叉树，满足如下性质：对于任一结点（编号为P），其左子树（如存在）中的最大结点编号为U，则U<P；右子树（如存在）中的最小结点编号为V，则P<V。

以下图为例对二叉树进行遍历：先序遍历（先父结点，再左子树，再右子树）为6,3,1,2,5,4,9,7,8,10；中序遍历（先左子树，再父结点，再右子树）为1,2,3,4,5,6,7,8,9,10；后序遍历（先左子树，再右子树，再父结点）为2,1,4,5,3,8,7,10,9,6。

很显然，一对正确的先、中序遍历能唯一确定一棵二叉树。以下图的先、中序为例：先序遍历开头（6）即为父结点，则中序遍历中父结点左侧（1,2,3,4,5）为左子树，右侧（7,8,9,10）为右子树，而左右子树又可以各通过同样的方法再分为左子树、父结点、右子树；以左子树为例，其先序遍历（3,1,2,5,4）开头（3）为父结点，中序遍历中父结点左侧（1,2）为左子树，右侧（4,5）为右子树……

![image-20200716181105452](C:\Users\杨子骏\AppData\Roaming\Typora\typora-user-images\image-20200716181105452.png)

给出HX的二叉树的先、中序遍历，求其后序遍历。

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

