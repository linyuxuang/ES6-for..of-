# ES6-for..of-
遍历对象的属性值

     for..of循环首先会向被访问对象请求一个迭代器对象,然后通过调用迭代器对象的next() 方法来遍历所有返回值


             注意：数组内部有@@iterator，因此for..of可以直接应用在数组上，
              我们使用内置的@@iterator的来手动遍历数组，

             我们看看他们是怎么工作的
            var arr=[1,2,3];
            var it=arr[Symbol.iterator]();
             console.log(it.next())  //{value: 1, done: false}
             console.log(it.next())  //{value: 1, done: false}
             console.log(it.next())  //{value: 1, done: false}
             console.log(it.next())  //{value: undefined, done: true}
    
  
  
  
  
          和数组不同的，普通的对象没有内置的@@iterator,所有无法自动完成for..of遍历，

               我们来给对象遍历属性值
              var obj2={
                   a:90,
                   b:89
              }      
                 Object.defineProperty(obj2,Symbol.iterator,{
                         value:function(){
                           var o=this;
                           console.log(o)
                           var index=0;
                           var obj=Object.keys(o);
                            return{
                                 next:function(){
                                    return{
                                         value:o[obj[index++]],
                                         done:(index>obj.length)
                                    }     
                                 }
                            }  
                         }
                 })

                  for(var v of obj2){
                      console.log(v);   // 90  89       
                  }

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
