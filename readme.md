# SyncFunc 函数顺序执行 #

----------

这个小东西可以保证js函数按顺序执行，并且支持设置每个函数的回调以及所有函数执行完成后的总回调。

使用实例：

	//函数f1
    function f1(cb){
		setTimeout(function(){
            console.log('f1 func 延迟3000');
            cb();
        }, 3000);
	}

	//函数f2
    function f2(cb){
		setTimeout(function(){
            console.log('f2 func 延迟2000');
            cb();
        }, 2000);
	}

	//函数f3
    function f3(cb){
		setTimeout(function(){
            console.log('f3 func 延迟1000');
            cb();
        }, 1000);
	}

	// 调用
	var sf = new SyncFunc([
		{
            func: f1,
            cb: function(cb){
                setTimeout(function(){
                    console.log('f1 func 的回调函数  延迟1000');
                    cb();
                }, 1000);
            }
        },
        {
            func: f2,
            cb: function(cb){
                setTimeout(function(){
                    console.log('f2 func 的回调函数  延迟2000');
                    cb();
                }, 2000)
            }
        },
        {
            func: f3,
            cb: function(cb){
                setTimeout(function(){
                    console.log('f3 func 的回调函数  延迟3000');
                    cb();
                }, 3000)
            }
        }
    ], function(d){
        console.log('总的回调函数 over');
    });

    sf.fire();

