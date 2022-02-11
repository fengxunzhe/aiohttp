# coding:utf-8
import logging
import time, asyncio, aiohttp

import aiofiles
from lxml import etree
from pypac import get_pac, PACSession


async def main(link, title, semaphore):
    async with semaphore:  # 这里进行执行asyncio.Semaphore，
        async with aiohttp.ClientSession() as session:
            async with session.get(link, proxy="http://172.21.1.30:8080") as resp:
                dict = await resp.text()
                html = etree.HTML(dict)
                result = ""
                for res in html.xpath('//*[@id="content"]/text()'):
                    result = result + res

            async with aiofiles.open("test02\\" + title, mode="w", encoding="utf-8") as f:  # 使用with as
                # 表示用完之后自动关闭，此处是异步存储aiofiles
                await f.write(result.strip())  # 加上await代表写入的时候空闲时间CPU去干其他的

            print("success" + title)


async def run(urls):
    semaphore = asyncio.Semaphore(500)  # 限制并发量为500,这里windows需要进行并发限制，
    # 不然将报错：ValueError: too many file descriptors in select()

    pac = get_pac(url='http://10.18.88.118/proxy.pac')
    st = PACSession(pac)

    logging.captureWarnings(True)
    result = st.get(urls, verify=False)

    result.encoding = result.apparent_encoding  # 获取返回的数据编码进行设置， 不管请求的是那种编码，都不需要自己去判断编码和设置

    html = etree.HTML(result.text)
    tasks = []
    lists = html.xpath('//*[@id="list"]/dl/dd')
    for list in lists:
        link = "".join(list.xpath(".//a/@href"))
        link = f"https://www.23wx.cc/du/164/{book_id}/" + link
        title = "".join(list.xpath(".//a/text()"))
        tasks.append(main(link, title, semaphore))

    await asyncio.wait(tasks)


if __name__ == '__main__':
    book_id = "164856"
    urls = f"https://www.23wx.cc/du/164/{book_id}/"
    loop = asyncio.get_event_loop()
    loop.run_until_complete(run(urls))
    loop.close()
