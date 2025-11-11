import requests
from bs4 import BeautifulSoup

# 定義需要抓取的網址列表
urls = [
    "https://www.concerngo.com/blog/posts",
    "https://www.concerngo.com/blog/posts/11112025",
    "https://www.concerngo.com/blog/posts/251030-drwu",
    "https://www.concerngo.com/blog/posts/recommended10",
    "https://www.concerngo.com/blog/posts/trend",
    "https://www.concerngo.com/blog/posts/massager-15questions",
    "https://www.concerngo.com/blog/posts/evaluation",
    "https://www.concerngo.com/blog/posts/3style",
    "https://www.concerngo.com/blog/posts/20250912-con-2618",
    "https://www.concerngo.com/blog/posts/250825-con-2618",
    "https://www.concerngo.com/blog/posts/250825-con-7855"
]

# 函數：抓取網頁標題
def get_title(url):
    try:
        response = requests.get(url)
        response.raise_for_status()  # 確保請求成功
        soup = BeautifulSoup(response.content, 'html.parser')
        title = soup.find('title')  # 找到 <title> 標籤
        return title.text if title else "No title found"
    except requests.exceptions.RequestException as e:
        return f"Error fetching {url}: {e}"

# 遍歷每個網址並打印標題
for url in urls:
    title = get_title(url)
    print(f"Title for {url}: {title}")

