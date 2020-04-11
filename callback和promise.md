# callback 和 promise

## 异步callback

回调函数：类型为function的函数参数，callback常用于异步方法的回调，也有的用于同步方法，例如数组中的`forEach`方法：

```javascript
var arr = [1,2,3]
arr.forEach(function(val){
    console.log(val)
})
console.log('finish')

// 1,2,3,finish
```

还有数组的`map`、`filter`、`reduce`方法

常见的异步callback像`setTimeout`中的回调：

```javascript
setTimeout(function (){
    console.log('aaa')
},1000)
console.log('bbb')

// aaa , bbb
```

#### 回调地狱（callback hell）

callback hell：下一步的操作依赖于上一步的结果，上一步的操作又依赖于上上步的结果；层层callback嵌套

```javascript
one(param,function (result1){
    two(result1,function(result2){
        three(result2,function(result3){
            done(result3)
        })
    })
})
```

## Promise

Promise 译为承诺，代表当前没有实现，但在未来的某个时间点会（也可能不会）实现的一件事。例如：我承诺（Promise）在半小时写完作业，如果一切顺利，半小时后提交了，代表这个`promise`实现了（`fullfilled`），但是中间出了什么问题，半小时之后没有顺利提交，那么这个`promise`失败了（`rejected`）：

```javascript
const task = new Promise(function (resolve, reject){
    me.write(function(timeSpent){
        if(timeSpent <= 30){
            resolve()
        }else{
            reject()
        }
    })
})
```

#### 链式调用（promise chaining）

将一串的callback函数用Promise实现，然后链式调用：

```javascript
one(param)
.then((result1)=>{return two(result1)})
.then((result2)=>{return three(result2)})
.then((result3)=>{return done(result3)})
.catch(err=>handleError(err))
```

#### Async/Await

可以用`async/await`转化成更接近同步调用的方式：

```javascript
async function main(){
    try{
        var result1 = await one(param)
        var result2 = await two(result1)
        var result3 = await three(result2)
        done(result3)
    }catch(err){
        handleError(err)
    }
}

main()
```



