# Additive-fraction-decomposition

Additive fraction decomposition

    如：1/2=1/4+1/4.找出所有方案。
    
    输入：Ｎ  Ｍ	Ｎ为要分解的分数的分母
    
		Ｍ为分解成多少项
    
【参考程序】

program fenshifenjie;

const  nums=5;

var

   t,m,dep:integer;
   
   n,maxold,max,j:longint;
   
   path:array[0..nums] of longint;
   
   maxok,p:boolean;
   
   sum,sum2:real;
   
procedure print;

var i:integer;

begin

	  t:=t+1;
    
	  if maxok=true then begin maxold:=path[m];maxok:=false;end;
    
	  write ('NO.',t);
    
	  for i:=1 to m do write(' ',path[i]:4); writeln;
    
	  if path[1]=path[m] then begin writeln('Ok!   total:',t:4);readln;halt;end;
    
end;


procedure input;

begin

	  writeln ('input N:'); readln(n);
    
	  writeln ('input M(M<=',nums:1,'):'); readln(m);
    
	  if (n<=0) or (m<=0) or (m>4) or (n>maxlongint)
    
		   then begin writeln('Invalid Input!');readln;halt;end;
       
end;

function sum1(ab:integer):real;

var a,b,c,d,s1,s2:real;

    i:integer;
    
begin

	 if ab=1  then
   
	      sum1:=1/path[1]
        
	 else
   
	      begin
        
		  a:=path[1];
      
		  b:=1	     ;
      
		  c:=path[2];
      
		  d:=1;
      
		  for i:=1 to ab-1 do
      
		       begin
           
			  s2:=(c*b+a*d);
        
			  s1:=(a*c);
        
			  a:=s1;
        
			  b:=s2;
        
			  c:=path[i+2];
        
		       end;
           
		  sum1:=s2/s1;
      
	       end;
         
end;

procedure back;

begin

	  dep:=dep-1;
    
	  if dep<=m-2 then max:=maxold;
    
	  sum:=sum-1/path[dep];
    
	  j:=path[dep];
    
end;

procedure find;

begin

   repeat
   
	 dep:=dep+1;
   
	 j:=path[dep-1]-1;
   
	 p:=false;
   
	   repeat
     
	    j:=j+1;
      
	    if (dep<>m) and (j<=max) then
      
	       if (sum+1/j) >=1/n then p:=false
         
		     else  begin
         
			   p:=true;
         
			   path[dep]:=j;
         
			   sum:=sum+1/path[dep];
         
			   end
         
	       else if j>max then back;
         
	    if dep=m then begin
      
	       path[dep]:=j;
         
	       sum2:=sum1(m);
         
	       if (sum2)>1/n then p:=false;
         
	       if (sum2)=1/n then begin     print;
         
					    max:=j;
              
					    back;
              
					    end;
              
	       if (sum2<1/n) then back;
         
	       if (j>=max)   then back;
         
	       end;
         
      until p
      
   until dep=0;
   
end;

begin

     INPUT;
     
     maxok:=true;
     
     for t:=0 to m do  path[t]:=n;
     
     
     dep:=0; t:=0; sum:=0;
     
     max:=maxlongint;
     
     find;
     
     readln;
     
end.

