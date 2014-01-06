
::

    演算法原理：
        如果要將 n 個盤子從 source_stack 移動到 dest_stack，勢必先將 n-1 個盤子先從 source_stack 移動
        到 temp_stack，所以至少會有三根柱子。

        n 盤移動 a to b 的部分演算法是一樣的，假設一個 function 所做的事情就是這件事，並命名為 move。

        簡單來說就是：
            如果要完成 n 塔從 source_stack 移動到 dest_stack，必定要先完成 n-1 塔從 source_stack 移動
            到 temp 再把 source_stack 塔的最底下那塊移動到 dest_stack，再把 n-1 塔移動到 dest_stack。

        演算法推算
            1 塔的時候即：
                source to dest


            2 塔的時候即：
                source to temp (1塔的演算法, 從 source to temp))
                    ...
                source to dest
                    ...
                temp to dest (1塔演算法, 從 temp to dest)


            3 塔的時候即：
                source to temp (2塔演算法, 從 source to temp))
                    ...
                source to dest
                    ...
                temp to dest (2塔演算法, 從 temp to dest)


            4~n 塔的時候同理。
                source to temp (3塔演算法, 從 source to temp)
                    ...
                source to dest
                    ...
                temp to dest (3塔演算法, 從 temp to dest)


        就可以推算出演算法：
            var move=function(n,source_stack,temp_stack,dest_stack){
                if(n==1){
                    // 如果是一塔的時候
                    console.log('from '+source_stack.toString()+' move to '+dest_stack.toString()+' !');
                }
                else if(n>1){
                    // 將 n-1 塔演算法
                    move(n-1,source_stack,dest_stack,temp_stack);

                    // 將來盤子從編號為 ? 的來源柱移動到編號為 ? 的目的柱
                    console.log('from '+source_stack.toString()+' move to '+dest_stack.toString()+' #');
                    
                    // 再將先前的 n-1 個盤子從 temp_stack 移動到 dest_stack
                    move(n-1,temp_stack,source_stack,dest_stack);
                }
            }

        這個演算法由兩個部分組成：
            1. 把 n 個盤子從 (a 透過暫存器 b 移動到 c )
                => move(n,a,b,c)

            2. 當只有一個盤子的時候直接從 a 移動到 c 即可
                => console.log( 'from '+a.toString()+' move to '+b.toString() );

                that's do(1)(n-1,a,b,c)
                then   do(2)
                then   do(1)(n-1,b,a,c)

                完成！
