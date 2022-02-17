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
                await  后 +  IO操作、task任务   如: await asyncio.wait(tasks)
