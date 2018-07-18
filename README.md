# setTimeout

```js
    for (var i = 1;i <= 5;i ++) {
        setTimeout(function timer() {
            console.log(i)
        },i * 1000)
    }

```

```js
    for(var i = 0;i<5;i ++) {
        (function(i){
            setTimeout(function timer() {
            console.log(i)
            }, i * 1000);
        })(i);
    }



    var loop = function (i) {
        setTimeout(function timer() {
            console.log(i);  
        }, i*1000);
    };
    for (var i = 1;i <= 5; i++) {
        loop(i);
    }


    const sleep = (timeountMS) => new Promise((resolve) => {
        setTimeout(resolve, timeountMS);
    });
    
    (async () => {
    for (var i = 0; i < 5; i++) {
        await sleep(1000);
        console.log(new Date, i);
    }
    })();

```

```js
    console.log('global')

    setTimeout(function () {
        console.log('timeout1')
    new Promise(function (resolve) {
        console.log('timeout1_promise')
        resolve()
    }).then(function () {
        console.log('timeout1_then')
    })
    },2000)

    for (var i = 1;i <= 5;i ++) {
    setTimeout(function() {
        console.log(i)
    },i*1000)
        console.log(i)
    }

    new Promise(function (resolve) {
        console.log('promise1')
    resolve()
    }).then(function () {
        console.log('then1')
    })

    setTimeout(function () {
    console.log('timeout2')
    new Promise(function (resolve) {
        console.log('timeout2_promise')
        resolve()
    }).then(function () {
        console.log('timeout2_then')
    })
    }, 1000)

    new Promise(function (resolve) {
        console.log('promise2')
    resolve()
    }).then(function () {
        console.log('then2')
    })

```

- 执行顺序

```js

    async function async1() {
        console.log("async1 start");
        await  async2();
        console.log("async1 end");
    }
    async function async2() {
        console.log( 'async2');
    }
    console.log("script start");
    setTimeout(function () {
        console.log("settimeout");
    },0);
    async1();
    new Promise(function (resolve) {
        console.log("promise1");
        resolve();
    }).then(function () {
        console.log("promise2");
    });
    console.log('script end');

```

```js

function debounce(func, delay) {
    var timeout;
    return function(e) {
        console.log("清除",timeout,e.target.value)
        clearTimeout(timeout);
        var context = this, args = arguments
        console.log("新的",timeout, e.target.value)
        timeout = setTimeout(function(){
          console.log("----")
          func.apply(context, args);
        },delay)
    };
};
 
var validate = debounce(function(e) {
    console.log("change", e.target.value, new Date-0)
}, 380);
 
document.querySelector("input").addEventListener('input', validate);

```

```js
function throttle(fn, threshhold) {
    var timeout
    var start = new Date;
    var threshhold = threshhold || 160
    return function () {
    
    var context = this, args = arguments, curr = new Date() - 0
    clearTimeout(timeout)
    if(curr - start >= threshhold){
        console.log("now", curr, curr - start)
        fn.apply(context, args)
        start = curr
    }else{
            timeout = setTimeout(function(){
                fn.apply(context, args)
            }, threshhold);
        }
    }
    }
    var mousemove = throttle(function(e) {
        console.log(e.pageX, e.pageY)
    });

 document.querySelector("#panel").addEventListener('mousemove', mousemove);

```