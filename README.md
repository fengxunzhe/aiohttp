# aiohttp
单线程异步协程爬虫

记录学习异步协程爬虫

######  python3.7以后 asyncio.run  替代了  以下

    # loop = asyncio.get_event_loop()
    # loop.run_until_complete(run(urls))
    # loop.close()
    
    asyncio.run(run(urls))

######  python3.7以后
    await asyncio.wait(tasks)

    # asyncio.create_task() 把任务加入队列   后面统一使用asyncio.wait(task)把任务加入列表
    
    
######  关键字  async代表该函数是协程函数
                await  后 +  IO操作、task对象、协程对象   如: await asyncio.wait(tasks)

######  协程对象执行流程
        aync def demo：
            pass
         
        DM = demo()
        DM得到的是协程对象，并不会去执行函数的内容，通过  asyncio.run(demo()) 函数执行协程流程

###### await 就是等待得到结果后再去执行下面的
        aync def demo：
            
            await other()
            此处是等待other函数执行完毕后才会去执行下面的other2
            await other2()
        
###### task任务的两种方式
        1、task = {
            asycio.createtask(fun(),arvg),   #  中途加入单个任务
            asycio.createtask(fun2(),arvg)
        }
        2、tasks = []
        tasks01 = {                                #  一次性加入任务
            task.append(fun())
        }      
        await asyncio.wait(tasks)
        
        
