js for等循环 跳出多层循环
js for 循环 跳出多层循环

复制代码
var a = [1,2,3,4,5,6,7,8]; // 8个数
var b = [11,12,13,14,15,3,16,17]; //8个数

testFor();
console.log('555')

function testFor() {
  for(var k=0;k<a.length;k++){
    console.log('444');
    for(var i=0;i<a.length;i++){
      for(var j=0;j<b.length;j++){
        if( a[i]==b[j] ){
          return false;
        }
        console.log('111');
      }
      console.log('2222');
    }
    console.log('333');
  }
}


输出:
// 1次444
// 8次111
// 1次222
// 8次111
// 1次222
// 5次111
// 1次555    
复制代码
 

可见 return 会直接跳出多层循环,返回调用的方法外部
原因: js里for是没有局部作用域的概念,方法才能一个局部作用域
return将会跳出当前局部作用继续执行下面的方法

注意：
1.这里for循环如果直接放在全局作用域下执行而不被一个方法包裹，
将直接导致写在for后的代码永远不会被执行；

2.如遇到逻辑特别复杂多层循环的时候，会遇到一些迭代器之类的方法，
这种迭代器实现的不同,会出现另一种情况，即不会跳出任何循环，
循环仍然继续，只是当前循环if后的代码不会被执行一次，下一次循环开始时,
仍然会执行if后的代码

如：
var cc = 'xx';

Object.keys(o).forEach(function(key) {
var val = o[key];
if(cc == key){
return false;
}
console.log(key);
});

此外还有
break;
continue;
语句
break 语句跳出循环后，会继续执行该循环之后的代码 (退出循环)
continue continue 语句中断循环中的迭代，如果出现了指定的条件，然后继续循环中的下一个迭代。(跳过当前迭代,进入下次迭代)
这两个语句可以指定label从而可以退出特定的循环
如

复制代码
bbq:
for(var j=0;j<a.length;j++){
    ccc:
    for(var i =0;i<a.length;i++){
        if( i==5 ){
            break bbq; //直接跳出bbq外层循环
        }
    }
}


或者:
function testFor() {
    bbq:
    for(var k=0;k<a.length;k++){
        console.log('444');
        ccc:
        for(var i=0;i<a.length;i++){
            ddd:
            for(var j=0;j<b.length;j++){
                if(j == 2){
                    break;
                }
                console.log('j '+j);
            }
            console.log('i '+i);
       }
       console.log('k '+k);
    }
}    
复制代码
 

 

// 只会每次循环j==2时退出ddd循环然后外面的循环都会继续循环
