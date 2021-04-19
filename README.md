[学生端助手2](https://github.com/zijunhz/MythwareStudentClientAssistant/releases/tag/2.0)

<html>
<head>
<meta charset="UTF-8">
<title>猜数字</title>
</head>
<script>
	var rule_on_show=0,init1=0,tern=0,ans,first=1,tot=0,pre=0,l=0,flag=0,check=0,G=0,isright=0,lA=0;
	var a=new Array(),b=new Array(),cmp=new Array(),rd=new Array();
	function show_rule(){
		if(rule_on_show==0){
			document.getElementById("rule").innerHTML='规则：<br>通常由两个人玩，一方出数字，一方猜。<br>出数字的人要想好一个没有重复数字的4个数，不能让猜的人知道。<br>猜的人就可以开始猜。每猜一个数字，出数者就要根据这个数字给出几A几B，<br>其中A前面的数字表示位置正确的数的个数，而B前的数字表示数字正确而位置不对的数的个数。<br>如正确答案为 5234，而猜的人猜 5346，则是 1A2B，<br>其中有一个5的位置对了，记为1A，而3和4这两个数字对了，而位置没对，因此记为 2B，<br>合起来就是 1A2B。<br>接着猜的人再根据出题者的几A几B继续猜，直到猜中（即 4A0B）为止。<br>-更新:<br>-  1.猜数机制更新<br>-程序要猜你选的数，回复A和B的个数<br>-括号内为剩余可能性<br>-请手动记录猜数及反馈<br>-若第一次猜结果为0A1B或0A2B程序会因运算量大小卡1-2秒，要耐心等！<br>';
			document.getElementById("rule_bt").innerHTML='隐藏规则&操作说明';
			rule_on_show=1;
		}else{
			document.getElementById("rule").innerHTML='';
			document.getElementById("rule_bt").innerHTML='显示规则&操作说明';
			rule_on_show=0;
		}
	}
	function build(){
		for(var i=0;i<=5;i++)cmp[i]=new Array();
		for(var i=0;i<=9;i++)for(var j=0;j<=9;j++)for(var k=0;k<=9;k++)for(var l=0;l<=9;l++){
			if(i==j||i==k||i==l||j==k||j==l||k==l)continue;
			a[++tot]=i*1000+j*100+k*10+l;
		}
	}
	function init(){
		if(first==1){
			build();first=0;
		}
		for(var i=1;i<=tot;i++)b[i]=1;
		flag=2;check=1;init1=1;tern=0;isright=0;lA=0;
		makeguess();
	}
	function getn(x,n){
		for(var i=1;i<=4-n;i++)x=Math.floor(x/10);
		return x%10;
	}
	function compA(X,Y){
		var x=new Array(),y=new Array(),A=0;
		for(var i=1;i<=4;i++)x[i]=getn(X,i);
		for(var i=1;i<=4;i++)y[i]=getn(Y,i);
		for(var i=1;i<=4;i++)if(x[i]==y[i])A++;
		return A;
	}
	function compB(X,Y){
		var x=new Array(),y=new Array(),B=0;
		for(var i=1;i<=4;i++)x[i]=getn(X,i);
		for(var i=1;i<=4;i++)y[i]=getn(Y,i);
		for(var i=1;i<=4;i++)for(var j=1;j<=4;j++)if(i!=j&&x[i]==y[j])B++;
		return B;
	}
	function sqr(x){
		return x*x;
	}
	function abS(x){
		if(x>=0)return x;return -x;
	}
	function makeguess(){
		tern++;
		if(flag<=1){
				//-----------------------------------------------------------
				if(flag==1&&lA==3){
					G=a[Math.ceil(Math.random()*Math.random()*tot*tot*tot)%tot+1];pre=5040;
				}else{
					var bestans=1e7,ans,ave,cnt;l=0,eps=1e-3;
					pre=0;
					for(var i=1;i<=tot;i++){
						if(b[i]==0)continue;
						pre++;
						for(var j=0;j<=4;j++)for(var k=0;k<=4-j;k++)cmp[j][k]=0;
						for(var j=1;j<=tot;j++)
							if(b[j]==1){
								cmp[compA(a[j],a[i])][compB(a[j],a[i])]++;
							}
						cnt=0;ave=0;
						for(var j=0;j<=4;j++)for(var k=0;k<=4-j;k++)
							if(cmp[j][k]!=0){
								cnt++;ave+=cmp[j][k];
							}
						ave/=cnt;ans=0;
						for(var j=0;j<=4;j++)for(var k=0;k<=4-j;k++)
							if(cmp[j][k]!=0){
								ans+=sqr(ave-cmp[j][k]);
							}
						ans/=cnt;ans-=cnt*1.1;
						if(abS(ans-bestans)<=eps){
							rd[++l]=i;continue;
						}
						if(ans<bestans){
							l=1;rd[1]=i;bestans=ans;
						}
					}
					G=a[rd[Math.ceil(Math.random()*Math.random()*tot*tot*tot)%l+1]];
				}
				//-----------------------------------------------------------
			}else{
				G=a[Math.ceil(Math.random()*Math.random()*tot*tot*tot)%tot+1];pre=5040;
			}
		var t='';
		for(var i=1;i<=4;i++)t=t+String(getn(G,i));
		document.getElementById("inf").innerHTML=String(tern)+': '+t+' ('+String(pre)+')';flag--;
		//document.getElementById("inf").innerHTML=String(l);
	}
	function kill(){
		if(init1==0){
			document.getElementById("inf").innerHTML='未开局';return;
		}
		if(isright==1){
			document.getElementById("inf").innerHTML='共'+String(tern)+'步猜出';init1=0;
			return;
		}
		var gusA=document.getElementById("reA").value,gusB=document.getElementById("reB").value,A,B,ill=0;
		if(isNaN(gusA)||isNaN(gusB)||gusA==''||gusB=='')ill=1;
		else{
			A=Number(gusA);B=Number(gusB);
			if(A<0||B<0||A>4||B>4||A+B>4)ill=1;
		}
		if(ill==1){
				document.getElementById("inf").innerHTML='输入不合法';return;
		}
		lA=A;
		if(A==4){
			document.getElementById("inf").innerHTML='共'+String(tern)+'步猜出';init1=0;
			return;
		}
		var count=0;
		for(var i=1;i<=tot;i++){
			if(b[i]==1&&((compA(a[i],G)!=A||compB(a[i],G)!=B)||a[i]==G))b[i]=0;
			if(b[i]==1)count++;
		}
		if(count==0){
			document.getElementById("inf").innerHTML='输入存在自相矛盾';init1=0;return;
		}
		makeguess();
	}
	function result(){
		isright=1;
		kill();
	}
</script>
<body>
	<h3>猜数游戏辅助vers4.0</h3>
	<p id="rule"></p>
	<button id="rule_bt" type="button" onclick="show_rule()">显示规则&操作说明</button><br>
	<button id="restart" type="button" onclick="init()">重开一局</button><br>
	<button id="right" type="button" onclick="result()">猜对了<br></button>
	<br><br>
	<p id="inf"></p>
	<input id="reA" type="tel">A <input id="reB" type="tel">B<br>
	<button id="submit" type="botton" onclick="kill()">确认无误</button>
</body>
</html>






























































[1](https://paste.ubuntu.com/p/QczrwD5sQM/)
